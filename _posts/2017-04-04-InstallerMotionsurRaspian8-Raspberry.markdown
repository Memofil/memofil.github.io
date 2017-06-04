---
layout: default
title:  "Installer Motion & MotionEye sur Raspberry - Raspbian 8"
date:   2017-04-01 00:09:36 +0200
categories: Motion Raspberry Raspbian
---

<h3>Préalable</h3>
<ul>
<li>
Il faut s'assurer que le pilote de la caméra soit bien installé. Si la webcam utilisé est la pi camera V2 ( noir ou non), il va falloir activer un pilote présent sur raspbian Jessie mais non actif:
{% highlight ruby %}
echo "bcm2835-v4l2" | sudo tee -a /etc/modules
{% endhighlight %}


</li>
<li> Verifier aussi que ces paquets sont bien installés
{% highlight ruby %}
sudo aptitude install python-tornado python-jinja2 python-imaging motion ffmpeg v4l-utils
{% endhighlight %}
</li>
</ul>


<h3>Installer les dépendances:</h3>
{% highlight ruby %}
wget https://github.com/ccrisan/motioneye/wiki/precompiled/ffmpeg_3.1.1-1_armhf.deb
sudo dpkg -i ffmpeg_3.1.1-1_armhf.deb
sudo apt-get remove libavcodec-extra-56 libavformat56 libavresample2 libavutil54
sudo apt-get install python-pip python-dev curl libssl-dev libcurl4-openssl-dev libjpeg-dev libx264-142 libavcodec56 libavformat56 libmysqlclient18 libswscale3 libpq5
sudo apt-get -f install
{% endhighlight %}

<h3>Installer Motion</h3>
{% highlight ruby %}
sudo wget https://github.com/Motion-Project/motion/releases/download/release-4.0.1/pi_jessie_motion_4.0.1-1_armhf.deb
sudo dpkg -i pi_jessie_motion_4.0.1-1_armhf.deb
{% endhighlight %}

<h3>Installer MotionEye</h3>
{% highlight ruby %}
sudo apt-get install python-pycurl
sudo pip install motioneye
{% endhighlight %}



<h3> Préparer le dossier de configuration</h3>
{% highlight ruby %}
sudo mkdir -p /etc/motioneye
sudo cp /usr/local/share/motioneye/extra/motioneye.conf.sample /etc/motioneye/motioneye.conf
#
sudo mkdir -p /var/lib/motioneye
sudo cp /usr/local/share/motioneye/extra/motioneye.systemd-unit-local /etc/systemd/system/motioneye.service
{% endhighlight %}

<h3>Lancer le service</h3>
{% highlight ruby %}
sudo systemctl daemon-reload
sudo systemctl enable motioneye
sudo systemctl start motioneye
{% endhighlight %}

<h3> Acceder à MotionEye en local depuis le navigateur </h3>

Connaissant l'adresse Ip de votre Raspberry, dans la barre d'adresse entrez simplement :  http://192.168.0.10:8765

<h3> Lancer un script python depuis à MotionEye  "Run a command" </h3>

Il faut créer un script executable qui sera appelé par MotionEye.

1) Créer un script python : <code>nano monScript.py</code>

2) Exemple de script, enregistrement de l'heure et la date des détections : 
{% highlight ruby %}
import time
f = open("/home/pi/motionDetection.log","a")
f.write(time.strftime("%Y-%m-%d %H:%M")+'\n')
f.close()
{% endhighlight %}

3)Rendre le script executable :<code>sudo chmod +x monScript.py</code>

4) Dans la case "Run a command", insérer uniquement l'adresse du script : <code>/home/pi/monScript.py </code>



Source :

<a href="https://github.com/ccrisan/motioneyeos/wiki/Installation" target="_blanck">https://github.com/ccrisan/motioneyeos/wiki/Installation</a>

<a href="http://www.howtoembed.com/projects/raspberry-pi/95-motioneye-with-raspberry-pi" target="_blanck">http://www.howtoembed.com/projects/raspberry-pi/95-motioneye-with-raspberry-pi</a>
