---
layout: post
title:  "Configurer l'écran HDMI 5 pouces avec touche controller XPT2046 pour Rapsberry Pi"
date:   2017-04-17 10:37:00 +0200
categories: raspberry pi raspbian
---
Configurer l'ecran HDMI 5 pouces xpt2046 pour rapsberry pi


L'ecran tactile HDMI 5" 800x480 TFT Display with XPT2046 Touch Controller fonctionne sans pilote, il suffit de le brancher. 
Vous constaterez alors que la résolution n'est pas correcte : l'ecran actif n'occupe pas toute la dalle, et la fonction tactile n'est pas active.
Il faudra aller modifier le fichier config.txt présent dans le répertoire {% highlight ruby %}/boot/config.txt{% endhighlight %}

Modifier la résolution de l'écran :

Dans le fichier config.txt, modifier les lignes suivantes :

{% highlight ruby %}
# uncomment if you get no picture on HDMI for a default "safe" mode
#hdmi_safe=1

# uncomment this if your display has a black border of unused pixels visible
# and your display can output without overscan
disable_overscan=0

# uncomment if hdmi display is not detected and composite is being output
#hdmi_force_hotplug=1

# uncomment to force a specific HDMI mode (this will force VGA)
hdmi_group=2
hdmi_mode=1
hdmi_mode=87
hdmi_cvt=800 480 60 6 0 0 0
{% endhighlight %}

Redemarrer ensuite la rapsberry. LA résolution 800x480 devrait etre effective.


Rendre l'écran tactile :

Etape 1 :

{% highlight ruby %}
sudo apt-get update
sudo apt-get -y install xinput-calibrator
{% endhighlight %}

Etape 2 :
Ajouter les lignes suivantes à la fin du fichier config.txt modifié précédemment :
{% highlight ruby %}
# Enable touchscreen on Elecrow HDMI interface.
dtparam=spi=on
dtparam=i2c_arm=on
dtoverlay=ads7846,cs=1,penirq=25,penirq_pull=2,speed=50000,keep_vref_on=0,swapxy=0,pmax=255,xohms=150,xmin=200,xmax=3900,ymin=200,ymax=3900
dtoverlay=w1-gpio-pullup,gpiopin=4,extpullup=1
{% endhighlight %}


Pour utiliser un clavier tactile, il faut installer le paquet xvkbd:
{% highlight ruby %}
sudo apt-get install -y xvkbd
{% endhighlight %}


 
BUG:
Problème de calibration sous raspbien Jessie
L'écran tactile n'est pas bien calibré malgré les installations.
 
Une solution est donnée :
 
 [https://www.raspberrypi.org/forums/viewtopic.php?f=44&t=173993&p=1112311#p1112311](https://www.raspberrypi.org/forums/viewtopic.php?f=44&t=173993&p=1112311#p1112311)
 
 Il faut réinstaller les drivers de l'ecran en suivant les instructions du git :
 [https://github.com/goodtft/LCD-show](https://github.com/goodtft/LCD-show)
 
La procédure : 
 
{% highlight ruby %}
##
git clone https://github.com/goodtft/LCD-show.git
chmod -R 755 LCD-show
cd LCD-show/
##
sudo ./LCD5-show
##
sudo apt-get install xserver-xorg-input-evdev
sudo cp -rf /usr/share/X11/xorg.conf.d/10-evdev.conf /usr/share/X11/xorg.conf.d/45-evdev.conf
sudo reboot
{% endhighlight %}
 
 
A voir : 

- [Wiki](http://www.raspberrypiwiki.com/index.php/Touchscreen_calibration)

- [Source-Officielle](https://www.elecrow.com/wiki/index.php?title=HDMI_Interface_5_Inch_800x480_TFT_Display)


- [Aussi](https://www.jeffgeerling.com/blog/2016/review-elecrow-hdmi-5-800x480-tft-display-xpt2046-touch-controller)

