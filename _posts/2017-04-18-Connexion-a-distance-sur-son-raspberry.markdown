---
layout: post
title:  "Se connecter à distance sur son Rapsberry Pi via ssh"
date:   2017-04-17 10:37:00 +0200
categories: raspberry pi raspbian ssh 
---
Comment se connecter à distance sur son Rapsberry Pi ?

{% highlight ruby %}
# uncomment if you get no picture on HDMI for a default "safe" mode
#hdmi_safe=1

# uncomment this if your display has a black border of unused pixels visible
# and your display can output without overscan
disable_overscan=0

# uncomment if hdmi display is not detected and composite is being output
#hdmi_force_hotplug=1

# uncomment to force a specific HDMI mode (this will force VGA)
hdmi_group=2
hdmi_mode=1
hdmi_mode=87
hdmi_cvt=800 480 60 6 0 0 0
{% endhighlight %}

Redemarrer ensuite la rapsberry. LA résolution 800x480 devrait etre effective.


Rendre l'écran tactile :

Etape 1 :

{% highlight ruby %}
sudo apt-get update
sudo apt-get -y install xinput-calibrator
{% endhighlight %}

Etape 2 :
Ajouter les lignes suivantes à la fin du fichier config.txt modifié précédemment :
{% highlight ruby %}
# Enable touchscreen on Elecrow HDMI interface.
dtparam=spi=on
dtparam=i2c_arm=on
dtoverlay=ads7846,cs=1,penirq=25,penirq_pull=2,speed=50000,keep_vref_on=0,swapxy=0,pmax=255,xohms=150,xmin=200,xmax=3900,ymin=200,ymax=3900
dtoverlay=w1-gpio-pullup,gpiopin=4,extpullup=1
{% endhighlight %}




[source][source]
[source]: https://raspbian-france.fr/controlez-raspberry-pi-ssh-ordinateur/
