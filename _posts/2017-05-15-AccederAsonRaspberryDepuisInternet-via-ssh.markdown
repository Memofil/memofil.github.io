---
layout: default
title:  "Accéder à son raspberry pi depuis internet via ssh"
date:   2017-05-15 18:30:00 +0200
categories: raspberry Linux Terminal 
---


Si l'on souhaite acceder à son raspberry pi en dehors de son réseau local, c'est à dire via internet, renseigner l'adresse IP locale (192.168.x.x) de son raspberry ne suffit pas. Il va falloir connaitre l'adresse IP public de sa connexion internet et créer une passerelle entre internet, le routeur et le raspberry pi. 


<h3>Configuration du routeur</h3>

Chaque routeur à une interface différente, mais généralement la procédure est la même.

1) Se connecter à son compte Freebox et se rendre à la page : Ma Freebox > Configurer mon routeur > Redirections / Baux DHCP

2) Au niveaux des Redirections de ports, renseigner les ports que vous souhaitez ouvrir :

{% highlight ruby %}
Port externe : 1234 ( peut etre de 0 à 9999 )
Protocole : TCP 
IP DE DESTINATION : 192.168.X.XXX ( par ex :  192.168.0.123, il faudra configurer son raspberry pi en ip fixe )
Port interne : 22 ( le port 22 est par defaut celui qui fonctionne avec ssh sous Raspbian Jessie, mais il est possible de le changer en modifiant le fichier  sshd_config )
{% endhighlight %}

3) Une fois la redirection effectuée, redemarrer la freebox et vérifier que les modifications sont bien actives.


<h3>Préparer son raspberry</h3>

1) Ouvrir la connexion ssh via raspi-config

2) Connaitre l'adresse ip publique de la connexion internet du raspberry, via http://www.whatsmyip.org/ ou sites équivalent. L'adresse est alors du type "92.190.45.32" ( à ne pas confondre avec IP locale, du type 192.168.0.10)


<h3>Connexion à distance via ssh</h3>

Ouvrir un terminal et taper la ligne de commande :


{% highlight ruby %}
ssh pi@92.190.45.32 -p 1234
{% endhighlight %}

Il suffit alors d'entrer votre mot de passe et voila vous etes connecté!

<strong>Remarque : </strong> Il est possible d'avoir une adresse perso avec <a href="http://www.noip.com/" title="http://www.no-ip.com" target="_blank" >no-ip.com</a> qui viendra remplacer l'adresse 92.190.45.30. no-ip va se charger de faire le transfert, ainsi l'IP publique du routeur n'est pas en claire pour les pc distant qui s'y connectent.





