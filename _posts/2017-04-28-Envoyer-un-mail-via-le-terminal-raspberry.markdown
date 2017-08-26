---
layout: default
title:  "Envoyer un mail en ligne de commande sous raspbian jessie"
date:   2017-04-28 12:30:00 +0200
categories: Git Linux Terminal 
---

Installer SSMTP, mail et mpack pour les pieces jointes

{% highlight ruby %}
sudo apt-get install ssmtp
sudo apt-get install mailutils
sudo apt-get install mpack

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


