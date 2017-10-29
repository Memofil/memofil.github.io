---
layout: default
title:  "Se connecter à une Time Capsule via Raspberry Pi"
date:   2017-05-17 18:30:00 +0200
categories: Raspberry
tags: Raspberry Pi Raspbian 8 Time Capsule Ubuntu VNC Linux Terminal
---

<h3>Pour une Raspberry Pi sous raspbian Jessie</h3>

<h3>Préalable</h3>
<ul>
<li>Vérifier via le gestionnaire de paquets synaptic que les paquets smbclient et smbfs sont bien installés.
Dans le cas contraire, les installer via synaptic ou bien :
{% highlight ruby %}
sudo apt-get install smbclient
sudo apt-get install cifs-utils
{% endhighlight %}

</li>
<li>Vérifier que le nom de votre Time Capsule est bien celui que vous pensez etre associé à l'adresse IP. Dans le cas, ou le nom est " TimeCapsule" :

{% highlight ruby %}
sudo apt-get install samba-common-bin
nmblookup TimeCapsule
{% endhighlight %}
Vous devriez avoir: 
{% highlight ruby %}
192.168.0.17 TimeCapsule<00>
{% endhighlight %}
</li>

<li>Créer un répertoire pour accueillir le point de montage

{% highlight ruby %}
sudo mkdir /media/Capsule
{% endhighlight %}
</li>

<li>Connaitre le nom du disque de la Time Capsule, Dans mon cas : DATA. Vous pouvez le trouver via utilitaire Airport Mac ou Windows, c'est le nom du sous répertoire auquel vous accédez une fois connecté.
</li>


<h3>Monter la Time Capsule</h3>

{% highlight ruby %}
sudo mount //192.168.0.17/DATA -o'sec=ntlm' /media/Capsule
{% endhighlight %}

ou bien 
{% highlight ruby %}
sudo mount //192.168.0.17/DATA -o'sec=ntlm' /media/Capsule -o password="MotDePasseCapsule"
{% endhighlight %}




<h3> Monter la Time Capsule de manière permanente sans afficher le mot de passe </h3>


Il va falloir editer le fichier '/etc/fstab' en ajoutant un lien exterieur vers un fichier contenant le mot passe que l'on aura protégé en 'root'.
{% highlight ruby %}
sudo nano /etc/.fstab_credentials
{% endhighlight %}
et insérer :
{% highlight ruby %}
username=TimeCapsule
password=MotDePasseCapsule
{% endhighlight %}

puis réduire les droits :
{% highlight ruby %}
sudo chown root.root /etc/.fstab_credentials 
sudo chmod 400 /etc/.fstab_credentials 
{% endhighlight %}

<h4> Editer le fichier fstab </h4>
 Insérer à la fin du fichier "/etc/fstab": 
 {% highlight ruby %}
//192.168.0.17/DATA /home/pi/media/Capsule cifs credentials=/etc/.fstab_credentials,file_mode=0777,dir_mode=0777,uid=pi,gid=pi,forceuid,forcegid,sec=ntlm,iocharset=utf8 0 0

{% endhighlight %}


Enfin, il va falloir  activer l'option "Wait for network" :

Préférences > Raspberry Pi Configuration >  Network at Boot




Sources :

<a href="http://blog.martinshouse.com/2014/09/mounting-apple-time-capsule-share-from.html" target="_blanck">http://blog.martinshouse.com/2014/09/mounting-apple-time-capsule-share-from.html</a>

<a herf ="https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=179046" target="_blanck">https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=179046</a>
