---
layout: post
title:  "Automatiser les taches de sa framboise avec cron"
date:   2017-05-17 18:30:00 +0200
categories: Raspberry Pi Cron Linux Terminal 
---

<h3>Installation de Cron</h3>

Cron est installé par défaut sur Raspbian 8 Jessie, mais il est possible d'obtenir une version graphique en installant gnome-schedule :

{% highlight ruby %}
sudo apt-get install gnome-schedule
{% endhighlight %}

<h3>Utiliser Cron</h3>
Afin de planifier des taches, il faut editer la cron table :
{% highlight ruby %}
crontab -e
{% endhighlight %}

A la fin du fichier, vous verrez normalement des exemples, si vous souhaitez que cron exceute le script <code>/home/pi/backup.sh</code> toute les  minutes, on écrira :

{% highlight ruby %}
#execution du backup de la base historique toutes les minutes
* * * * * sh /home/pi/backup.sh
{% endhighlight %}


<strong>Sources :</strong>
<ul>
    <li>
    <a href="https://www.raspberrypi.org/documentation/linux/usage/cron.md">Documentation Officielle Raspbian </a>
    </li>
    <li>
     <a href="https://technique.arscenic.org/commandes-linux-de-base/article/cron-gestion-des-taches-planifiees">cron-gestion-des-taches-planifiees</a>
    </li>
</ul>