---
layout: post
title:  "Une IP statique pour son Raspberry PI sous Rapsbian 8 (Jessie)"
date:   2017-05-15 12:30:00 +0200
categories: raspberry Raspbian Jessie
---

Il peut etre très utile d'avoir une IP Statique pour son Raspberry, notamment si l'on souhaite s'y connecter à distance.

Il faut tout d'abord récupérer des informations sur la connexion , notamment connaitre l'adresse de la porte du routeur. Ainsi il faut taper :

{% highlight ruby %}
ip route | grep default | awk '{print $3}'
{% endhighlight %}
On obtient alors une adresse du type :
{% highlight ruby %}
192.168.0.254
{% endhighlight %}




Nous pouvons ensuite configurer l'IP statique. Pour cela, il faut modifier le fichier "dhcpcd.conf" :

{% highlight ruby %}
sudo nano /etc/dhcpcd.conf
{% endhighlight %}

Ajouter les lignes suivant à la fin du fichier :
{% highlight ruby %}
#Allouer une IP STATIQUE
interface eth0
static ip_address=192.168.1.80/24
static routers=192.168.0.254
static domain_name_servers=208.67.222.222,208.67.220.220
interface wlan0
static ip_address=192.168.1.81/24
static routers=192.168.0.254
static domain_name_servers=208.67.222.222,208.67.220.220

{% endhighlight %}

<strong>Remarques: </strong>
 - Noter que l'on peut configurer un adresse ip statique différente selon que l'on soit connecté par cable ethernet ou bien wifi
 - Ne pas oublier /24 à la fin de l'adresse choisie.
 - La création de l'IP fixe a corrompu l'acces à internet de la raspberry pi ( apparement sur Jessie uniquement, Wheezy ne serait pas concerné -> voir  .
 Une solution est de modifié le DNS de sortie avec un nameserver google 8.8.8.8 ou openDNS 208.67.222.222 :
 
<h4><strong>Sources:</strong></h4>
 
<a href="https://raspberrypi.stackexchange.com/questions/37920/how-do-i-set-up-networking-wifi-static-ip-address">how-do-i-set-up-networking-wifi-static-ip-address</a>
<a href="https://www.raspberrypi.org/forums/viewtopic.php?f=36&t=127183" target="_Blanck">https://www.raspberrypi.org/forums/viewtopic.php?f=36&t=127183</a>
