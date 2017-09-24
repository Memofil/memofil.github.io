---
layout: default
title:  "Utiliser le GPIO de son raspberry pi"
date:   2017-06-18 18:30:00 +0200
categories: raspberry GPIO Terminal 
---
 ![Les "Pins" ou broches d'un Raspberry Pi ]({{site.url}}/assets/images/posts/raspberry-pi/gpio-pins.jpg)
<h1> Qu'est que le GPIO ? </h1>

 Les ports GPIO ou  General Purpose Input/Output  ([Wikipedia](https://fr.wikipedia.org/wiki/General_Purpose_Input/Output)), sont les ports d'entrée et de sortie sous forme de broches du raspberry
 


 Ils permettent de communiquer avec d'autres circuits électroniques, pour allumer tout simplement une LED, controler des cerveaux moteurs ou encore communiquer avec une carte arduino.
 Les exemples d'utilisation ne manquent pas : 
 
 * [https://thepihut.com/blogs/raspberry-pi-tutorials/27968772-turning-on-an-led-with-your-raspberry-pis-gpio-pins](https://thepihut.com/blogs/raspberry-pi-tutorials/27968772-turning-on-an-led-with-your-raspberry-pis-gpio-pins){:target="_blank"}
 
 * [http://razzpisampler.oreilly.com/ch05.html](http://razzpisampler.oreilly.com/ch05.html){:target="_blank"}
 

# Comment utiliser le GPIO de son Raspberry pi 

Le nombre de broches est différents selon les modèles et toutes les broches ne sont pas des gpios, il y a aussi des broches pour alimentations 5V,3.3 V et des masses broches, il va etre donc necessaire de les identifier. 
Voici un schéma de connection pour le modèle RPI3 que j'utilise : 

![Raspberry Pi 3 Model B REv 1]({{site.url}}/assets/images/posts/raspberry-pi/GPIO-Schema-PI-3-modelB-Rev1-elements.png)
 Raspberry Pi 3 Model B Rev 1 (40-pin)
 
 Le coté gauche du dessin est celui qui donne vers l'interieur du RPI et le coté droit est celui proche du bord.

-----------------

Sur ce site intéractif : [https://pinout.xyz/](https://pinout.xyz/#) , vous pouvez trouver des informations sur les fonctionalités des broches et les connections qu'il faut réaliser pour différents composants électroniques


## Communiquer avec sa framboise ##

Il n'est pas necessaire de savoir coder en [Assembler](https://fr.wikipedia.org/wiki/Assembleur){:target="_blank"}  pour communiquer avec les machines. Il existe en effet une librairie ( écrite en C ) pour ça : [WiringPI](http://wiringpi.com/){:target="_blank"}.
Il est alors possible d'écrire nativement C/C++  dans d'autres langages comme java ou Python via des programmes de déléguation (["Wrappers"]( https://fr.wikipedia.org/wiki/Fonction_wrapper){:target="_blank"}). On retiendra : 

* [Pi4J](http://pi4j.com/index.html){:target="_blank"} : Une librairie  pour programmer en java

* [WiringPI-extension](https://github.com/WiringPi){:target="_blank"}  : Wrappers pour python, perl, ruby ou encore php 

Je vous conseille vivement de lire le site [http://wiringpi.com/](http://wiringpi.com/){:target="_blank"} qui apporte beaucoup plus d'informations que ce résumé.


### Activer les ports GPIO ###
Les ports ne sont pas activés par défaut, il faut alors taper :
```SHELL 
sudo raspi-config
```
et activer :
* Activer l'interface ARM I2C ( [Inter Integrated Circuit ](https://fr.wikipedia.org/wiki/I2C){:target="_blank"} ). En deux mots, I2C est un [bus informatique](https://fr.wikipedia.org/wiki/Bus_informatique){:target="_blank"} ), permettant la communication entre le processseur du Rapsberry Pi et les composants électoniques connectés par les GPIO et qui doivent eux aussi utiliser cette norme.
* Activer l'interface SPI ( [Serial Port interface](https://fr.wikipedia.org/wiki/Serial_Peripheral_Interface){:target="_blank"} )www, comme I2C est un bus de communication avec ses propres particularités.

Faites ensuite un `sudo reboot` et pour tester si les deux bus sont bien activés, tapez ensuite :
``` SHELL
lsmod | grep i2c_
lsmod | grep spi
```
Si I2C et SPI sont bien actifs, vous devriez alors voir s'afficher la liste des modules qui les utilisent.

Enfin, I2C dispose d'un paquet d'utilitaires necessaire à installer ( si il n'est pas déja présent) :
```SHELL
sudo apt-get install -y i2c-tools
```
Grace à ces utilitaires, on pourra notamment connaitre la présence ou non d'un dispositif sur les ports GPIO :
```SHELL
i2cdetect -y 1
```

* Activer l'interface UART ([Universal Asynchronous Receiver Transmitter](https://fr.wikipedia.org/wiki/UART){:target="_blank"}). L'UART est un port de communication parrallèle et asynchrone. Beaucoup de composants vont utiliser ce service pour communiquer avec le PI. Cependant, depuis la version 3 de la rapsberry, la configuration de ce port est un peu plus compliqué : le protocole n'est pas totalement libre car la fonction blutooth du RPI 3 l'utilise en partie, ce que peut jouer sur les performances.([Voir l'explication claire du site framboise314 ](http://www.framboise314.fr/le-port-serie-du-raspberry-pi-3-pas-simple/){:target="_blank"}). Pour activer l'UART, la configuration simple mais non optimale consiste à ajouter la ligne `enable_uart=1` à la fin du fichier `/boot/config.txt`


### Démarrer un montage électronique avec sa raspberry ###

* Afin de réaliser un montage electronique, on utilise généralement une breadboard qui va nous permettre de faire des tests plus aisément. Une breakout board et une nappe sont aussi fortement recommandées pour réduire les chocs électrostatiques.
* Il est aussi fortement conseiller de protéger les GPIOs des surtensions et courts circuit qui peuvent apparaitre à la suite des manipulations effectuées. Il est en effet très facile de griller son rapsberry puisque les pins GPIO sont directement branchés au coeur de la carte de mere de la famboise. PLusieurs méthodes de protection (Zener Diode Protection,Transistor Switch,Transistor Logic Shifters,...) sont énoncées à cette adresse : [GPIO Protection Circuits](http://elinux.org/RPi_Tutorial_EGHS:GPIO_Protection_Circuits){:target="_blank"} ou encore sur ce forum [Protection board](https://www.raspberrypi.org/forums/viewtopic.php?f=45&t=24540){:target="_blank"}. La solution la plsu communément utilisé pour le prototypage est de mettre une resistance 1K Ohm en série entre les pins du RPI et la carte électronique que l'on souhaite utiliser. En cas de court-circuit, la resistance protègera les pins d'une surtension. ( voir [ici](http://www.linuxembedded.fr/2014/07/electronique-simple-pour-gpio/){:target="_blank"} ou encore [la](https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=132953) {:target="_blank"}


## Vidéos sur le Raspberry Pi et l'électronique ##

<iframe width="560" height="315" src="https://www.youtube.com/embed/9Qumu2h8FjY" frameborder="0" allowfullscreen></iframe>


## Sources : ##

*  [https://www.raspberrypi.org/documentation/usage/gpio/](https://www.raspberrypi.org/documentation/usage/gpio/){:target="_blank"} 
*  [http://elinux.org/RPi_Low-level_peripherals](http://elinux.org/RPi_Low-level_peripherals){:target="_blank"} 
*  [https://learn.sparkfun.com/tutorials/raspberry-pi-spi-and-i2c-tutorial](https://learn.sparkfun.com/tutorials/raspberry-pi-spi-and-i2c-tutorial){:target="_blank"} 
*  [http://deusyss.developpez.com/tutoriels/RaspberryPi/PythonEtLeGpio/](http://deusyss.developpez.com/tutoriels/RaspberryPi/PythonEtLeGpio/){:target="_blank"} 
*  [https://spellfoundry.com/2016/05/29/configuring-gpio-serial-port-raspbian-jessie-including-pi-3/](https://spellfoundry.com/2016/05/29/configuring-gpio-serial-port-raspbian-jessie-including-pi-3/){:target="_blank"} 

