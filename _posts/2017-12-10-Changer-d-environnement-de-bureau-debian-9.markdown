---
layout: default
title:  "Changer d'environnement de bureau sous Débian 9"
date:   2017-12-08 10:25:00 +0200
categories: Debian 
tags : [Debian, Display Manager, Gnome, Xcfe, Kde]
---

# Changer d'environnement de bureau sous Débian 9

Sous Debian 9 , Le __display manager__ `Gdm` ne propose pas de pouvoir changer d'environnement de bureau au démmarrage.
Pour cela , il faut passer par `lightdm`


```
sudo dpkg-reconfigure lightdm
```
Choisir lightdm et redemmarrer l'ordinateur. Vous pouvez ensuite choisir entre les différents environnement que vous avez installés ( Gnome, Cinnamon, KDE, Xcfe ) 

## Liens ## 
+ [http://support.system76.com/articles/desktop-environment/](http://support.system76.com/articles/desktop-environment/){:target="_blank"}
