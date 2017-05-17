---
layout: post
title:  "Se connecter à son Raspberry Pi par internet avec VNC Viewer"
date:   2017-05-17 18:30:00 +0200
categories: Raspberry Pi Ubuntu VNC Linux Terminal 
---

<h3>Préalable</h3>
Il est necessaire que VNC soit activé sur le Raspberry Pi, pour cela il faut se rendre sur la page de configuration des interfaces :
{% highlight ruby %}
sudo raspi-config
{% endhighlight %}
Il faut connaitre l'IP publique de la connexion internet à laquelle le Raspi est attaché (du type 98.562.74.14). Vous pouvez la connaitre via le site <a href="www.whatismyip.com/fr/" title="whatismyip" target="_blank">www.whatismyip.com/fr/</a> ). Vous devez connaitre aussi l'IP locale de son Raspberry dans le réseau ( du type 192.168.0.XX).
Enfin, il faut ouvrir les ports necessaires au niveau de votre routeur. Dans le cas d'une freebox, Se connecter à son compte Freebox et se rendre à la page : Ma Freebox > Configurer mon routeur > Redirections / Baux DHCP

VNC utilise par défaut le port 5900, nous configurons la redirection alors comme :
{% highlight ruby %}
Port externe : 1234
Protocole : TCP 
IP DE DESTINATION : 192.168.X.XXX 
Port interne : 5900
{% endhighlight %}



<h3>Utiliser VNC Viewer</h3>
Vous avez toutes les informations necessaires pour vous connecter, ainsi, lancer VNC Viewer.
Puis Fichier > Nouvelle Connexion

il suffit alors de renseigner les infos suivantes :
{% highlight ruby %}
VNC Server : 98.562.74.14:1234
Nom: NomDelaConnexion( celui que vous souhaitez voir afficher sur VNC)
{% endhighlight %}

Quand vous vous connecterai pour la premiere fois, VNC vous demandera le nom de votre serveur, dans notre cas "pi" , ainsi que le mot de passe associé.
