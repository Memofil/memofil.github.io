---
layout: default
title:  "Demarrer un Arduino Uno avec un pc"
date:   2017-06-26 8:30:00 +0200
categories: Arduino 
tag: Arduino Uno Ubuntu
---

# Démarrer une Arduino Uno avec un pc
![Schema pinout - Arduino Uno Rev 3.]({{ site.url }}/assets/images/categories/arduino/Arduino-Uno-Rev3-photo.jpg)
L'Arduino Uno est une carte electronique possedant un ["microcontrôleur"](https://fr.wikipedia.org/wiki/Arduino){:targer="_blank"} et différent ports GPIO permettant de créer differents circuits électronique pilotable depuis un ordinateur .

[->Vers la documentation Officielle](https://www.arduino.cc/en/Guide/ArduinoUno){:target="_blank"}

## Comment se connecter au Arduino Uno depuis Windows 10? ## 

1. Brancher l'Arduino Uno via USB, Windows 10 devrait detecter le périphérique etinstaller automatiquement les pilotes .

2. Installer Arduino IDE : [https://www.arduino.cc/en/Main/Software](https://www.arduino.cc/en/Main/Software){:target="_blank"}


Source :
 * [Guide d'installation Officiel (Anglais)](https://www.arduino.cc/en/Guide/Windows){:target="_blank"}

 
## Comment se connecter au Arduino Uno depuis Ubuntu? ## 
Deux choix s'offre à nous: 
### 1. Installer le paquet arduino  et arduino-mk (pour controler l'arduino avec le terminal ) depuis les dépots d'Ubuntu ###
```Shell
sudo apt-get install arduino
sudo apt-get install arduino-mk
```
### 2. Télécharger et installer Arduino IDE depuis le site Officiel ###

Comme pour windows, il est possible de récupérer la dernière version de l'IDE d'arduino depuis [le site officiel](https://www.arduino.cc/en/Guide/Linux){:target="blank"}

Je vous conseille la deuxième solution car le depot sur Ubuntu est un peu ancien.

## Schéma des pins ##

![Schema pinout - Arduino Uno Rev 3.]({{ site.url }}/assets/images/categories/arduino/Arduino-Uno-Rev3-pinout.jpg)

Source : 
* [Documentation  Arduino avec Ubuntu](https://doc.ubuntu-fr.org/arduino){:target="_blank"}

## Video de présentation et premiers montages## 

<iframe width="560" height="315" src="https://www.youtube.com/embed/xTXjsC78RSQ?list=PLT6rF_I5kknPf2qlVFlvH47qHvqvzkknd" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/qNI8Ast1kqA" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/9uwxvq-try4" frameborder="0" allowfullscreen></iframe>

## Sources : ##
* [À la découverte de l'Arduino Uno](http://www.epingle.info/?p=3764){:target="_blanck"}
