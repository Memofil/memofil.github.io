---
layout: post
title:  "Installer une carte son USB sur Raspberry PI - Raspbian 8"
date:   2017-05-20 00:09:36 +0200
categories: Carte Son USB Raspberry Raspbian
---

<h3>Préalable</h3>
<ul>
<li>
Verifier que les utilitaires usb sont bien installés:
{% highlight ruby %}
sudo apt-get install usbutils
{% endhighlight %}

</li>

</ul>


<h3>Compatibilité des cartes sons</h3>
Les cartes sons usb générique sont bien reconnus par la Raspberry Pi sous Raspbian Jessie. 
Dans mon cas, J'ai une carte son achetée 2 euros sur un site chinois qui marche très bien.

Verifier que le son fonctionne : 
{% highlight ruby %}
speaker-test -Dhw:1,0 -c2 -twav
{% endhighlight %}



Si vous rencontrez des problemes, vous pouvez suivre un petit tuto de verification très rapide : 
<a href="http://www.instructables.com/id/Use-USB-Sound-Card-in-Raspberry-Pi/" target="_blanck">http://www.instructables.com/id/Use-USB-Sound-Card-in-Raspberry-Pi/</a>




<h3>Enregistrement sonore avec la Raspberry</h3>

{% highlight ruby %}
arecord --device=plughw:1,0 --format S16_LE --rate 44100 -c1 test.wav
{% endhighlight %}

Pour lire l'Enregistrement :

{% highlight ruby %}
aplay --device=plughw:1,0 test.wav
{% endhighlight %}


http://www.oodlestechnologies.com/blogs/Record-Audio-on-Raspberry-Pi-3-using-audio-sound-card
https://raspberrypi.stackexchange.com/questions/40831/how-do-i-configure-my-sound-for-jasper-on-raspbian-jessie


Lien vers le site officiel du pilote audio  :

<a href="http://www.alsa-project.org/main/index.php/Matrix:Module-usb-audio" target="_blanck">http://www.alsa-project.org/main/index.php/Matrix:Module-usb-audio</a>