---
layout: post
title:  "Synchroniser avec Unison"
date:   2017-04-28 12:30:00 +0200
categories: Unison Linux Terminal 
---

Installer Unison
{% highlight ruby %}
sudo apt-get install unison
{% endhighlight %}

Afin de configurer le serveur d'envoi, il faut éditer le fichier sstmp.conf

{% highlight ruby %}
sudo nano /etc/ssmtp/ssmtp.conf 
{% endhighlight %}

Ajouter alors les infos de comptes:

{% highlight ruby %}
root=postmaster
mailhub=smtp.gmail.com:587
hostname=raspberrypi
AuthUser=MonAdresse@gmail.com
AuthPass=MotdePasseGmail
FromLineOverride=YES
UseSTARTTLS=YES
{% endhighlight %}

Attention, le mot de passe sera en clair! Conseil pour plus de sécurité : ouvrir une messagerie spéciale pour le raspberry pi.

Envoyer un mail :


{% highlight ruby %}
echo "Le corps du mail" | mail -s "Titre du mail" destinataire@mail.com
{% endhighlight %}


Envoyer une piece jointe :

{% highlight ruby %}
mpack -s "Titre du Mail" /home/pi/dossier-perso/fichier destinataire@mail.com
{% endhighlight %}





[source][source]
[source]: http://www.raspberry-projects.com/pi/software_utilities/email/ssmtp-to-send-emails


