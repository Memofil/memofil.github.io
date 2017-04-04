---
layout: post
title:  "Installer Bash pour Windows 10, Ruby et Jekyll!"
date:   2017-04-01 00:09:36 +0200
categories: jekyll update ash windows 10 wsl
---
Ajouter Bash, Ruby et Jekill sur windows 10

Comment installer la version Bash d'Ubuntu sur windows 10 :

https://msdn.microsoft.com/en-us/commandline/wsl/install_guide

1. Aller dans Parametres> Mise à jour et sécurité > Pour les développeurs  : Activer le mode developpeur ( l'ordinateur va devoir redemarrer et installer de nouveaux packages
2. Aller dans la barre de recherche et tapez : fonctionalités windows ( vers la page : Activer ou désactiver les fonctionnalités windows )
3. Activer Sous-systeme Windows pour linux ( et redémarrer)
4. Dans la barre windows, taper bash, et sélectionner l'appli Bash.exe. Windows va ouvrir un terminal et proposer d'installer ubuntu sur windows, taper o pour confirmer.
5. Entrer un nom d'utilisateur et un mot de passe pour ubuntu
6. Enjoy Bash pour ubuntu est installé. 


Désintaller Bash pour windows
1. ouvrir un terminal cmd.exe
2.lxrun /uninstall

Comment installer Ruby  ?

1. Lancer Bash pour Ubuntu en tapant Bash dans la barre de recherche windows
2. taper :
{% highlight ruby %}
sudo apt-get update
sudo apt-get install ruby-full
{% endhighlight %}

Erreurs possibles:
1. Sous Bash , sudo apt-get update ne marche pas : Failed to fetch
Solution : Désactiver le firewall ( zonealarm , etc..)



