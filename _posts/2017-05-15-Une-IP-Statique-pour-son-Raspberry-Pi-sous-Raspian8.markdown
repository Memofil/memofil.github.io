---
layout: default
title:  "Une IP statique pour son Raspberry PI sous Rapsbian 8 (Jessie)"
date:   2017-05-15 12:30:00 +0200
categories: [Raspberry, Raspbian, Jessie]
tags : [Raspberry, Raspbian, Jessie]
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

<h3>1) Modifier le fichier "dhcpcd.conf" </h3>

{% highlight ruby %}
sudo nano /etc/dhcpcd.conf
{% endhighlight %}

Ajouter les lignes suivant à la fin du fichier :
{% highlight ruby %}
#Allouer une IP STATIQUE
interface eth0
static ip_address=192.168.1.80/24
static routers=192.168.0.254
static domain_name_servers=208.67.222.222 208.67.220.220
interface wlan0
static ip_address=192.168.1.81/24
static routers=192.168.0.254
static domain_name_servers=208.67.222.222 208.67.220.220

{% endhighlight %}

<h3>2) Modifier le fichier "interfaces" </h3>

{% highlight ruby %}
sudo nano /etc/network/interfaces
{% endhighlight %}

tel que : 

{% highlight ruby %}
# interfaces(5) file used by ifup(8) and ifdown(8)

# Please note that this file is written to be used with dhcpcd
# For static IP, consult /etc/dhcpcd.conf and 'man dhcpcd.conf'

# Include files from /etc/network/interfaces.d:
source-directory /etc/network/interfaces.d

auto lo
iface lo inet loopback

auto eth0
allow-hotplug eth0

iface eth0 inet manual

auto wlan0
allow-hotplug wlan0
iface wlan0 inet manual
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

auto wlan1
allow-hotplug wlan1
iface wlan1 inet manual
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

{% endhighlight %}


Enfin il faut faire un <code>sudo reboot</code> ou bien (plus rapide) <code>sudo systemctl daemon-reload</code>.

<strong>Remarques: </strong>
 - Noter que l'on peut configurer un adresse ip statique différente selon que l'on soit connecté par cable ethernet ou bien wifi
 - Ne pas oublier /24 à la fin de l'adresse choisie.
 - static domain_name_server peut prendre différentes valeures, il y a le nameserver google 8.8.8.8 ou encore openDNS 208.67.222.222
 
<h4><strong>Sources:</strong></h4>
 <ul>
 <li>
<a href="https://raspberrypi.stackexchange.com/questions/37920/how-do-i-set-up-networking-wifi-static-ip-address">how-do-i-set-up-networking-wifi-static-ip-address</a>
</li>
<li>
<a href="https://www.raspberrypi.org/forums/viewtopic.php?f=36&t=127183" target="_Blanck">https://www.raspberrypi.org/forums/viewtopic.php?f=36&t=127183</a>
</li>
</ul>


Remarques :

Après la configuration, il arrive que la connection internet soit perdue bien que la raspi soit visible sur le réseau. L'erreur provient généralement d'une mauvaise configuration du fichier interface. 
Dans mon cas précis, sans avoir pris le temps de comprendre, il y a [une autre option de configuration](https://elinux.org/Configuring_a_Static_IP_address_on_your_Raspberry_Pi){:target="_blank"} qui fonctionne mieux que celle dessus ( que je conserve le temps de comprendre les différences) :

Dans le fichier `/etc/network/interface`, on ajoute les lignes suivantes :

```
auto lo

iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp

```


