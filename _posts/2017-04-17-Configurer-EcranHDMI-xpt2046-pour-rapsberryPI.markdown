---
layout: post
title:  "Configurer l'ecran HDMI 5 pouces avec touche controller XPT2046 pour Rapsberry Pi"
date:   2017-04-17 10:37:00 +0200
categories: raspberry pi raspbian
---
Configurer l'ecran HDMI 5 pouces xpt2046 pour rapsberry pi


L'ecran tactile HDMI 5" 800x480 TFT Display with XPT2046 Touch Controller s'installe sans pilote, il suffit de le brancher. 
Vous constaterez alors que la résolution n'est pas correcte : l'ecran actif n'occupe pas toute la dalle, et la fonction tactile n'est pas active.
Il faut aller modifier le fichier config.txt présent dans le répertoire {% highlight ruby %}/boot/config.txt{% endhighlight %}





[source][source]
[source]: https://www.jeffgeerling.com/blog/2016/review-elecrow-hdmi-5-800x480-tft-display-xpt2046-touch-controller
