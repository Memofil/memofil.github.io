---
layout: default
title:  "Installer X2go Server sous Débian 9"
date:   2017-12-08 10:25:00 +0200
categories: Debian 
tags : [Debian, VNC]
---

# Installer  X2goServer pour Débian 9

## Installer l'environnemnet de bureau xcfe
```
sudo apt-get install xfce4
sudo apt-get install task-xfce-desktop
```

## Installation X2goServer : Préalables
```
sudo apt install dirmngr
sudo apt-key adv --recv-keys --keyserver keys.gnupg.net E1F958385BFE2B6E
```
```
sudo editor /etc/apt/sources.list.d/x2go.list
```
```
# X2Go Repository (release builds)
deb http://packages.x2go.org/debian stretch extras main
# X2Go Repository (sources of release builds)
deb-src http://packages.x2go.org/debian stretch extras main

# X2Go Repository (nightly builds)
#deb http://packages.x2go.org/debian stretch extras heuler
# X2Go Repository (sources of nightly builds)
#deb-src http://packages.x2go.org/debian stretch extras heuler
```

## Installation de x2goServer


```
sudo apt-get install x2goserver x2goserver-xsession
```

## Installation du client X2goClient 

```
sudo apt-get install x2goclient
```

1. Ouvrir X2go
2. hote en local : 192.168.VOTRE.IP
3. utilisateur : username ( sur le serveur debian)
4. Type de session : XCFE


## Configurer le firewall pour limiter les accès

Installer UFW [(Uncomplicated FireWall)](https://wiki.ubuntu.com/UncomplicatedFirewall#Basic_Usage){:target="_blank"} :

```
sudo apt-get install ufw
```

Pour connaitre l'état d'activité du FireWall :

```
sudo ufw status verbose
sudo ufw disable # desactive si actif
```


Configurer le firewall tel qu'il refuse toutes les connexions entrantes et autorise les sortantes

```
sudo ufw default deny incoming
sudo ufw default allow outgoing

```


Autoriser l'accès par le port 22 :


```
sudo ufw allow 22
```

Activer le FireWall :

    sudo ufw enable
## Liens ## 
+ [https://www.digitalocean.com/community/tutorials/how-to-set-up-a-remote-desktop-with-x2go-on-debian-8](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-remote-desktop-with-x2go-on-debian-8){:target="_blank"}
