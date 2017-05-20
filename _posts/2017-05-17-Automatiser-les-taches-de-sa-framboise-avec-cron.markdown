---
layout: post
title:  "Automatiser les taches de sa framboise avec Cron"
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

Si vous souhaitez que Cron execute le script <code>/home/pi/backup.sh</code> toute les  minutes, on écrira à la fin du fichier :

{% highlight ruby %}
#execution du backup de la base historique toutes les minutes
* * * * * sh /home/pi/backup.sh >>/home/pi/backupLog/`date +\%Y\%m\%d\%H\%M\%S`-backup.log 2>&1
{% endhighlight %}

ou bien encore ( sans date) : 
{% highlight ruby %}
#execution du backup de la base historique toutes les minutes
* * * * * sh /home/pi/backup.sh >>/home/pi/backupLog/backup.log 2>&1
{% endhighlight %}

<strong>Remarque : </strong> La deuxième partie permet d'enregistrer dans un fichier l'historique des sauvegardes. 
Si vous avez mis en place un service de mail sur votre Raspberry, cette option est necessaire, car Cron va essayer de vous envoyer les logs par mail et "par defaut". 
Voir -> <a href="https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=66165" target="_blanck">https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=66165</a>

<strong>Sources :</strong>
<ul>
    <li>
    <a href="https://www.raspberrypi.org/documentation/linux/usage/cron.md" target="_blanck">Documentation Officielle Raspbian </a>
    </li>
    <li>
     <a href="https://technique.arscenic.org/commandes-linux-de-base/article/cron-gestion-des-taches-planifiees" target="_blanck">cron-gestion-des-taches-planifiees</a>
    </li>
</ul>