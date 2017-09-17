---
layout: default
title:  "Héritage Multiple : le problème du diamant en C++"
date:   2015-12-18 8:30:00 +0200
categories: Programmation C++ 
tag: Programmation C++ 
---

# Héritage Multiple : le problème du diamant en C++

En programmation objet,  lorsque l’on a affaire à un héritage multiple tel que les parents de la fille hérite du même parent :

![diagrammeHeritageMultiple]({{site.url}}/assets/images/categories/programmation/cplusplus/problemeDuDiamant.png)


Cela peut poser poser problème à la instanciation de la classe fille car son constructeur va faire appel aux constructeurs de Mere 1 , 2 qui eux même vont faire appel à celui de la classe GrandMere. Le compilateur va cracher une erreur du type : error request for member « … » is ambiguous . En effet, ce dernier ne saura pas par qui passer ( Mere 1 ou Mere 2) pour accéder au constructeur de GrandMere.

Afin de résoudre cette ambiguité appelée :  » le problème du diamant ». Il est possible de déclarer les classes Mere 1, 2 comme classes virtuelles de GrandMere. Dans ce sens , la classe fille va récupérer les méthodes et l’héritage de ses parents ( et donc de la grand Mère) sans que ces derniers ne fassent appel à leur constructeur.

 

L’exemple qui suit reprend cette idée, les classes Mere 1 et Mere 2 , on alors deux fonctions propres que la classe fille peut appeler. Les attributs proviennent quand à eux de la classe GM. ( Remarque dans cette exemple , les classes sont déclarées à l’avance dans les .h, les includes des classes sont appelées dans les .cpp pour éviter le problème de dépendance circulaire.

Nous avons donc :

GM.h :

```C++
#ifndef GM_H
#define GM_H
#include <string>
using namespace std;
class GM{
public :
int age;
string nom;
};
#endif

```

GM.cpp (le fichier est vide mais par défaut les constructeurs sont appelés automatiquement) :

```C++
#include "GM.h"
```


Mere1.h :

```C++
#ifndef Mere1_H
#define Mere1_H
#include "GM.h"
class Mere1: virtual public GM{
 
public :
void affiche_nom();
};
#endif
```

Mere1.cpp :

```C++
#include "GM.h"
#include "Mere1.h"
#include <iostream>
using namespace std;
 
void Mere1::affiche_nom(){
cout<< "Nom : "<<nom<<endl;
}
```

Mere2.h :
```C++
#ifndef Mere2_H
#define Mere2_H
#include "GM.h"
 
class Mere1;
 
class Mere2: virtual public GM{
public :
void affiche_age(Mere1);
};
 
#endif
```

Mere2.cpp :
```C++
#include "GM.h"
#include "Mere2.h"
#include "Mere1.h"
#include <iostream>
using namespace std;
 
void Mere2::affiche_age(Mere1 M1){
cout<< "Age :"<<age<<endl;
}
```

Fille.h :
```C++
#ifndef Fille_H
#define Fille_H
 #include "Mere2.h"
#include "Mere1.h"
 
class Fille: public Mere1,public Mere2{
 };
#endif
```

Fille.cpp :

```C++
#include "Fille.h"
```


main.cpp :

```C++
#include <iostream>
#include <fstream>
#include <string>
#include "GM.h"
#include "Mere1.h"
#include "Mere2.h"
#include "Fille.h"
using namespace std;
class GM;
class Mere1;
class Mere2;
class Fille;
 
int main(){
 
Fille f;
f.age=12;
f.nom="dupond";
 f.Mere1::affiche_nom();
f.Mere2::affiche_age(f);
return 0;
}
```

et le Makefile :

```C++
CC = g++
GLIBS=  #
CFLAGS =-Wall -c -g
LIBS = #
 
#========Regle pour clean , efface les fichiers indesirables pour un nouveau build====================================================================
 
cleanDebug: clean
cleanRelease: clean
clean:
    rm -rf  *.o *.bin
 
 
all :   herit
 
 
GM.o    :   GM.cpp
    $(CC)   $(CFLAGS)   $(GLIBS)    $(LIBS) GM.cpp
Mere1.o :   Mere1.cpp
    $(CC)   $(CFLAGS)   $(GLIBS)    $(LIBS) Mere1.cpp
Mere2.o :   Mere2.cpp
    $(CC)   $(CFLAGS)   $(GLIBS)    $(LIBS) Mere2.cpp
Fille.o :   Fille.cpp
    $(CC)   $(CFLAGS)   $(GLIBS)    $(LIBS) Fille.cpp
 
main.o  :   main.cpp
    $(CC)   $(CFLAGS)   $(GLIBS)    $(LIBS) main.cpp
 
herit   :   GM.o    Mere1.o Mere2.o Fille.o     main.o 
    $(CC)   $(LFLAGS)    GM.o   Mere1.o Mere2.o Fille.o     main.o      -o  herit   $(GLIBS)
```