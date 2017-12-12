---
layout: default
title:  "Installer VNC viewer sur Ubuntu 16.04"
date:   2017-05-17 18:30:00 +0200
categories: [Linux, Ubuntu, VNC, Terminal] 
tags :  [Linux, Ubuntu, VNC, Terminal]
---

# Installation automatique de VNC Viewer

Pour installer le client VNC Viewer, il faut se rendre à la page :
<a href="https://www.realvnc.com/download/vnc/linux/" title="Real VNC Connect" target="_blank"> https://www.realvnc.com/download/vnc/linux/</a>
Puis télécharger le .tar.gz, et ouvrir le .deb via l'installeur d'application.



<h3>Installation manuelle de Real VNC Viewer</h3>
Il arrive que l'application que l'on souhaite utiliser ne soit pas disponible dans la logithèque ubuntu. Au quel cas, nous allons alors l'installer manuellement




Vous pouvez trouver la derniere version de Real VNC viewer à l'adresse <a href="https://www.realvnc.com/download/viewer/linux/" title="Real VNC" target="_blank">https://www.realvnc.com/download/viewer/linux/ </a>

Nous allons télécharger le fichier via le terminal, la copier dans le dossier /opt/VNC, et le rendre executable en changeant les droits.

```BASH
wget https://www.realvnc.com/download/file/viewer.files/VNC-Viewer-6.1.0-Linux-x64.gz
gunzip VNC-Viewer-6.1.0-Linux-x64.gz
sudo mkdir /opt/VNC
sudo mv VNC-Viewer-6.1.0-Linux-x64 /opt/VNC/
sudo chmod 755 /opt/VNC/VNC-Viewer-6.1.0-Linux-x64
sudo mv VNC-Viewer-6.1.0-Linux-x64 VNC-Viewer-6.10
```


## Créer un .desktop pour l'application d 
L'application peut s'éxecuter directement depuis son répertoire, mais il peut etre interressant de pouvoir l'excecuter depuis n'importe quel endroit. Nous allons pour cela créer ".desktop" 

1. Au préalable, il faudra trouver l'icone RealVNC sur Internet, la télécharger et la copier dans le dossier VNC précédemment créé, que nous nommerons Icon-VNC-Viewer.png)

2. Créer un fichier .desktop :

```
[Desktop Entry]
nano VNC-Viewer-6.10.desktop
```
 et y insérer les lignes suivantes :
```
[Desktop Entry]
Name=VNC-Viewer-6.10
Exec=/opt/VNC/VNC-Viewer-6.10
Icon=/opt/VNC/Icon-VNC-Viewer.png
Type=Application
Categories=VNC;Utility;
```

Il faudra ensuite placer le fichier . desktop dans le dossier `/usr/share/applications` ou bien `~/.local/share/applications/`
```
sudo cp VNC-Viewer-6.10.desktop /usr/share/applications/
```





