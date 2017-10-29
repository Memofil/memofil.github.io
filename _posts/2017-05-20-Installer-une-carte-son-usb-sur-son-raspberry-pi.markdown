---
layout: default
title:  "Installer une carte son USB sur Raspberry PI - Raspbian 8"
date:   2017-05-20 00:09:36 +0200
categories: Raspberry 
tags : Raspberry Carte Son USB Raspbian
---

<h3>Préalable</h3>

<ul>
<li>

{% highlight ruby %}
#Pour les utilitaires usb
sudo apt-get install usbutils
#Pour l'encodage MP3
sudo apt-get install lame
{% endhighlight %}

</li>

<li> Attention passage obligé : Bug pour les processeurs ARM sous Raspian Jessie. il est necessaire d'installer la version précédente --> <a href ="http://stackoverflow.com/questions/24629915/multiple-files-created-by-arecord" target="_blanck">voir </a> . 
{% highlight ruby %}
#Pour les utilitaires usb
sudo apt-get install usbutils
#Pour l'encodage MP3
sudo apt-get install lame
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
arecord --device=plughw:1,0 --format S16_LE --rate 44100 -d 30 30s.wav
{% endhighlight %}


ou encore : 
{% highlight ruby %}
arecord --device=plughw:1,0 --format S16_LE --rate 44100 -d 30 --use-strftime %Y-%m-%d-%H-%M-%v.wav
{% endhighlight %}

Pour lire l'Enregistrement :

{% highlight ruby %}
aplay --device=plughw:1,0 test.wav
{% endhighlight %}



Sources :

<ul>
    <li>
    <a href="http://www.alsa-project.org/main/index.php/Matrix:Module-usb-audio" target="_blanck">Le site officiel du pilote audio</a>
    </li>
    <li>
    <a href="http://www.oodlestechnologies.com/blogs/Record-Audio-on-Raspberry-Pi-3-using-audio-sound-card" target="_blanck">http://www.oodlestechnologies.com/blogs/Record-Audio-on-Raspberry-Pi-3-using-audio-sound-card</a>
    </li>
    <li>
    <a href="https://raspberrypi.stackexchange.com/questions/40831/how-do-i-configure-my-sound-for-jasper-on-raspbian-jessie">https://raspberrypi.stackexchange.com/questions/40831/how-do-i-configure-my-sound-for-jasper-on-raspbian-jessie</a>
    </li>
    
</ul>
