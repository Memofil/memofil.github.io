---
layout: default
title:  "Gtkmm : DrawingArea à l’interieur d’une Gtk::Grid"
date:   2015-12-17 8:30:00 +0200
categories: Programmation C++ GTKmm
tag: Programmation C++ GTKmm
---

# Gtkmm : DrawingArea à l’interieur d’une Gtk::Grid

Lorsque l’on souhaite afficher à la fois une zone de dessin ( DrawingArea) et des boutons, il faut passer par les containers ( Hbox, table, Grid) , car ce sont tous les deux des Gtk::Window. Dans ce cas, nous allons utiliser la Gtk::Grid. Les boutons et la zone de dessin seront des membres d’une classe gtkBox qui herite de gtk::Window

Pour la zone de dessin, nous créons la classe cairoDrawing, avec :

cairoDrawing.cpp:

```
#include "cairoDrawing.h"
#include <ctime>
#include <cmath>
#include <cairomm/context.h>
#include <glibmm/main.h>


cairoDrawing::cairoDrawing(){
set_size_request (300, 200);
}

cairoDrawing::~cairoDrawing()
{
}

bool cairoDrawing::on_draw(const Cairo::RefPtr<Cairo::Context>& cr)
{
  Gtk::Allocation allocation = get_allocation();
  const int width = allocation.get_width();
  const int height = allocation.get_height();

  // coordinates for the center of the window
  int xc, yc;
  xc = width / 2;
  yc = height / 2;

  cr->set_line_width(10.0);

  // draw red lines out from the center of the window
  cr->set_source_rgb(0.8, 0.0, 0.0);
  cr->move_to(0, 0);
  cr->line_to(xc, yc);
  cr->line_to(0, height);
  cr->move_to(xc, yc);
  cr->line_to(width, yc);
  cr->stroke();

  return true;
}

```


cairoDrawing.h

```C++
#ifndef CAIRODRAWING_H
#define CAIRODRAWING_H

#include <gtkmm.h>
#include <gtkmm/drawingarea.h>

class cairoDrawing : public Gtk::DrawingArea
{
public:
  cairoDrawing();
  virtual ~cairoDrawing();

protected:
  //Override default signal handler:
  bool on_draw(const Cairo::RefPtr<Cairo::Context>& cr) override;
};

#endif // GTKMM_EXAMPLE_cairoDrawing_H

```
la classe gtkBox qui contient la zone de dessin et les boutons :

```C++
#include <iostream>
#include "gtkBox.h"

gtkBox::gtkBox()
: m_button_1("button 1"),
  m_button_2("button 2"),
  m_button_quit("Quit")
{
  set_title("Gtk::Grid");
  set_border_width(12);

  add(m_grid);

  m_grid.attach(m_Draw,0,0,2,2);
//  m_Viewer.show();
  m_grid.add(m_button_1);
  m_grid.attach_next_to(m_button_2, m_button_1, Gtk::POS_BOTTOM, 1, 1);
  m_grid.attach_next_to(m_button_quit, m_button_2, Gtk::POS_BOTTOM, 1, 1);


  m_button_1.signal_clicked().connect(
    sigc::bind<Glib::ustring>( sigc::mem_fun(*this,
      &gtkBox::on_button_numbered), "button 1") );
  m_button_2.signal_clicked().connect(
    sigc::bind<Glib::ustring>( sigc::mem_fun(*this,
      &gtkBox::on_button_numbered), "button 2") );

  m_button_quit.signal_clicked().connect(sigc::mem_fun(*this,
    &gtkBox::on_button_quit) );

  show_all_children();
}

gtkBox::~gtkBox()
{
}

void gtkBox::on_button_quit()
{
  hide();
}

void
gtkBox::on_button_numbered(const Glib::ustring& data)
{
  std::cout << data << " was pressed" << std::endl;
}
```


gtkBox.h : 

```C++
#ifndef GTKMM_gtkBox_H
#define GTKMM_gtkBox_H

#include "cairoDrawing.h"

class gtkBox : public Gtk::Window
{
public:
  gtkBox();
  virtual ~gtkBox();

private:

  void on_button_quit();
  void on_button_numbered(const Glib::ustring& data);

  
  Gtk::Grid m_grid;
  Gtk::Button m_button_1, m_button_2, m_button_quit;
  cairoDrawing m_Draw;
};

#endif /* GTKMM_gtkBox_H */
```


Dans le main nous allons pouvoir appeler notre nouvelle classe :
main.cpp :
```
#include <iostream>
#include "gtkBox.h"
#include <gtkmm/application.h>


using namespace std;

int main(int argc, char** argv)
{
  auto app = Gtk::Application::create(argc, argv, "org.gtkmm.example");
  gtkBox window;
  return app->run(window);

}
```

Enfin ces fichiers peuvent se compiler l’aide du makefile suivant :
Makefile :

```
CC = g++ -std=c++11
GLIBS=  `pkg-config --libs gtkmm-3.0 `	
CFLAGS =  -c `pkg-config --cflags gtkmm-3.0 `
LFLAGS =   `pkg-config --cflags gtkmm-3.0 `

cleanRelease: clean
clean:
	rm -rf *.eps *.pdf gnuplot  *.o *.bin

all :	GtkmmExample

cairoDrawing.o	: cairoDrawing.cpp
	$(CC)	$(CFLAGS)	$(GLIBS)	 cairoDrawing.cpp
gtkBox.o	: gtkBox.cpp
	$(CC)	$(CFLAGS)	$(GLIBS)	 gtkBox.cpp
main.o	:	main.cpp
	$(CC)	$(CFLAGS)	$(GLIBS)	main.cpp

GtkmmExample	: cairoDrawing.o gtkBox.o main.o	
	$(CC)	$(LFLAGS)	cairoDrawing.o gtkBox.o main.o	-o	GtkmmExample	$(GLIBS)
```