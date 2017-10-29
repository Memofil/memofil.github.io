---
layout: default
title:  "Comment brancher et utiliser le module A7 GPS/GPRS/GSM d'AI-THINKER  sur son raspberry pi"
date:   2017-07-30 13:30:00 +0200
categories: Raspberry GPIO A7
tags : Raspberry GPIO A7
---
## Comment brancher et utiliser le module A7 AI-THINKER GPS/GPRS/GSMI sur son Raspberry Pi ? ## 
 ![Le module A20 - AI-Thinker ]({{site.url}}/assets/images/posts/raspberry-pi/A20-AI-THINKER-module/A20-AI-THINKER-GPRS-GSM-WIFI-module-with-antenna.jpg)
## Qu'est que le module A7 AI-THINKER ? ##

Le module A7 du fabriquant chinois AI-THINKER, est un carte electronique permettant d'apporter une connection GPRS et un récepteur GPS à un rapsberry pi ou encore une carte arduino. Elle dispose donc de deux antennes, la grande étant pour capter envoyer et recevoir le signal GPS et la petite pour le réseau mobile GPRS ( ou 2G+ ).

## Le branchement du module A7 AI-THINKER sur les ports GPIO de la framboise ##

Brancher son rapsberry au module A7 est finalement la partie la moins triviale. Du fait, de l'absence de manuel mais aussi de la quasi-inexistance d'informations sur des sujets de même nature.

La communication entre rpi et le module A7 va se faire à travers les pins UARTs. Il faut alors brancher le pin UART_TXD ( Transmitter ) du module sur le pin UART_RXD ( Receiver) du raspberry, de même le pin UART_RXD du module se branchera sur le pin UART_TXD du raspberry. Pour le Raspberry 3, UART0_TXD est accessible via le GPIO 14 , et UART0_TXD via le GPIO 15  [(voir..)](http://elinux.org/RPi_Low-level_peripherals){:target="_blanck"}.

## Communiquer avec le module A7 ##

### Utiliser AT commands ###
Attention à ne pas confondre les commandes AT pour ATTention et le programme at sous unix ([https://en.wikipedia.org/wiki/At_(Unix)](https://en.wikipedia.org/wiki/At_(Unix)){:target="_blanck"} )

Pour avoir plus d'infos sur AT commands :
* [https://www.codeproject.com/Articles/85636/Introduction-to-AT-commands-and-its-uses](https://www.codeproject.com/Articles/85636/Introduction-to-AT-commands-and-its-uses){:target="_blanck"}
* [https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=158856&p=1032763#p1032763](https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=158856&p=1032763#p1032763){:target="_blanck"}
* [http://www.thegeekstuff.com/2013/05/modem-at-command/](http://www.thegeekstuff.com/2013/05/modem-at-command/){:target="_blanck"}




### Préalable ###

Installer Minicom qui va nous permettre d'envoyer des messages AT : 
```SHELL
sudo apt-get install minicom
```


### Exemples d'appel ###

```SHELL
sudo apt-get install at
```


## Sources : ##
* [http://www.electrodragon.com/w/GSM_GPRS_A6_Module#A7_Pin_Definitions](http://www.electrodragon.com/w/GSM_GPRS_A6_Module#A7_Pin_Definitions){:target="_blanck"}
* [https://github.com/SensorsIot/A6-GSM-Module](https://github.com/SensorsIot/A6-GSM-Module){:target="_blanck"}

* [https://raymondtunning.wordpress.com/2016/09/08/a20-the-new-gprsgsm-product/](https://raymondtunning.wordpress.com/2016/09/08/a20-the-new-gprsgsm-product/){:target="_blanck"}

*  [https://learn.adafruit.com/adafruit-ultimate-gps-on-the-raspberry-pi/using-uart-instead-of-usb](https://learn.adafruit.com/adafruit-ultimate-gps-on-the-raspberry-pi/using-uart-instead-of-usb){:target="_blanck"}
