---
layout: default
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

Si vous souhaitez que Cron execute le script <code>/home/pi/backup.sh</code> toutes les  minutes, on écrira à la fin du fichier :

{% highlight ruby %}
#execution du backup de la base historique toutes les 5 minutes
*/5 * * * *  /home/pi/backup.sh >>/home/pi/backupLog/backup.log 2>&1
{% endhighlight %}

ou bien encore toutes les minutes ( sans append ) : 
{% highlight ruby %}
#execution du backup de la base historique toutes les minutes
* * * * *  /home/pi/backup.sh >/home/pi/backupLog/backup.log 
{% endhighlight %}



<strong>Remarques : </strong> 

<ul>
<li>La deuxième partie permet d'enregistrer dans un fichier l'historique des sauvegardes. 
Si vous avez mis en place un service de mail sur votre Raspberry, cette option est necessaire, car Cron va essayer de vous envoyer les logs par mail et "par defaut". 
Voir -> <a href="https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=66165" target="_blanck">https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=66165</a>
</li>
<li>
Veiller à ce que le script soit executable :  <code>sudo chmod +x backup.sh</code>
</li>
<li>
Si les synchronisations sont trop peu espacées dans le temps, un nouveau job peut démarrer avant que l'ancien soit terminé,et cela peut provoquer des conflits et un comportement hasardeux de cron.
Une <a href="https://serverfault.com/questions/461306/make-a-cronjob-wait-for-previous-rsync-job-to-finish" target="_blanck">solution</a> est de conditionner le lancement de l'application associée au script.
Si cette derniere est déja en marche, l'application ne se lancera pas. Prenons l'exemple d'un backup avec rsync, du dossier <code>Documents</code> d'un Raspberry PI vers un dosser <code>PI/backup</code> d'un serveur distant.
<code>backup.sh</code> s'écrira :
{% highlight ruby %}
pgrep -c rsync || rsync -ssh -avz /home/pi/Documents user@IP.ADRESS:"PI/backup/"
{% endhighlight %}



</li>
<li>
Pour que la connexion soit automatique sans que la rpi redemande le mot de passe, il est essentiel d'utiliser les clefs SSH
{% highlight ruby %}
ssh-keygen -t dsa
ssh-copy-id nom@monserveur
{% endhighlight %}
</li>

</ul>
<strong>Sources :</strong>
<ul>
    <li>
    <a href="https://www.raspberrypi.org/documentation/linux/usage/cron.md" target="_blanck">Documentation Officielle Raspbian </a>
    </li>
    <li>
     <a href="https://technique.arscenic.org/commandes-linux-de-base/article/cron-gestion-des-taches-planifiees" target="_blanck">cron-gestion-des-taches-planifiees</a>
    </li>
</ul>
