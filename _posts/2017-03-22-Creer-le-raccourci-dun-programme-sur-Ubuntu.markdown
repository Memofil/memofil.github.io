---
layout: default
title:  "Créer le raccourci d’un programme sur Ubuntu 16.04"
date:   2017-03-22 18:30:00 +0200
categories: Linux Ubuntu
tag: Linux Ubuntu Shell
---

# Créer le raccourci d’un programme sur Ubuntu 16.04

Pour créer un icone personalisé  vous devez connaître le chemin qui mene à l'application et à l'image qui servira d'icone

1. Depuis le dossier personnel, se déplacer dans le répertoire caché `./local/share/applications`
2. Créer un fichier `.desktop`  et copier - coller le code suivant:

```SHELL

[Desktop Entry]
Version=1.0
Type=Application
Terminal=true
Categories=GNOME;GTK;


Exec= Nom_DE_LEXECUTABLE -a

# nom du lanceur
Name=Nom_De_Lappli( si different de l'executable)

# icône à appliquer au lanceur
Icon=/home/chemin_vers_licon/icon.xpm

#Permet de ne pas lancer le terminal
Terminal=false

```
3. le rendre executable : 

```
chmod +x .desktop
```
## Créer un lien symbolique

Dans le cas où l'application ne peut pas être appelée  par le terminal sans être dans son propre répertoire , il faudra créer un lien symbolique :

```SHELL
sudo ln -s /home/username/chemin_vers_l_application /usr/bin
```

## Ou ajouter le répertoire eclipse aux chemins globaux via `export PATH`


Dans `.profile`, ajouter : 

```
## mon_Application path variable
export PATH=$PATH:/home/user/chemin/de/mon_Application/
```
