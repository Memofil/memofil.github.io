---
layout: post
title:  "Configurer la connexion wifi de son raspberry pi sous Raspbian 8"
date:   2017-05-15 12:30:00 +0200
categories: raspberry Raspbian Terminal 
---

Afin de configurer la connexion wifi de son raspberry pi, 

1)Quels sont les réseaux wifi détectés ?
{% highlight ruby %}
sudo aptsudo iwlist wlan0 scan | grep ESSID
{% endhighlight %}

2)On verifie que notre réseau est bien dans la liste

3)On modifie le fichier de configuration  : 
{% highlight ruby %}
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
{% endhighlight %}
en y ajoutant les informations "network{...}" telles que:

{% highlight ruby %}
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=GB

network={
        ssid="Mon_réseau"
        psk="MonMotDePasse"
        key_mgmt=WPA-PSK
        priority=10
}
{% endhighlight %}

Si l'on dispose de plusieurs accès wifi, le réseau prioritaire est sélectionné via la variable " priority" sera celui ayant le chiffre le plus élevé.

Pour des questions de sécurité évidentes ( avec un sudo automatique, n'importe qui ayant acces à la raspberry pi peut découvrir tous les mots de passe associés aux réseaux WIFI), on peut ne pas vouloir renseigner son mot de passe en clair, il faut alors utiliser une version cryptée de son mot de passe via la passphrase. Dans le terminal, taper :

{% highlight ruby %}
wpa_passphrase Mon_réseau
{% endhighlight %}
Le terminal vous demandera ensuite de renseigner le mot de passe associé au réseau wifi

Remarque : Mon_réseau ne doit pas comporter d'espace et doit faire au moins 8 caractères, sinon la création de la passphrase ne sera pas possible. Il faut donc changer le nom dans ce cas, sous peine d'avoir ce message d'erreur :

{% highlight ruby %}
wpa_passphrase Mon réseau
Passphrase must be 8..63 characters
{% endhighlight %}

Si tout se passe bien vous devriez avoir la nouvelle configuration "sécurisée" qui s'imprime dans le terminal :
{% highlight ruby %}
network={
	ssid="Mon_réseau"
	#psk="MonMotDePasse" 
	psk=c29d0ef9bd513bfd4af645a852194bded003d99b948c6713276ed0f5633980eb
}
{% endhighlight %}
Remarque: #psk="MonMotDePasse" est en commentaire, il ne faudra pas oublier à supprimer cette ligne après le copier-coller ( pour éviter que le mot de passe demeure visible), ainsi nous aurons au final une solution sécurisée pour le fichier wpa_supplicant.conf comme :
{% highlight ruby %}
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=GB

network={
        ssid="Mon_réseau"
        psk=c29d0ef9bd513bfd4af645a852194bded003d99b948c6713276ed0f5633980eb
        key_mgmt=WPA-PSK
        priority=10
}
{% endhighlight %}



