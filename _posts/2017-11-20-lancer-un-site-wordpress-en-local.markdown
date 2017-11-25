---
layout: default
title:  "Lancer un site wordpress en local avec Lamp et Ubuntu 17.10"
date:   2017-11-20 8:30:00 +0200
categories: Jekyll 
tags: Jekyll ftp 
---

# Lamp
## Installation

Pour un serveur web avec apache, php et mysql : 

```
sudo apt install apache2 php mysql-server libapache2-mod-php php-mysql
```

## Connexion au Serveur
Après l'installation, le serveur se lance automatiquement à l'adresse : 

* [http://127.0.0.1/](http://127.0.0.1/){:target="_blank"}
* [http://localhost](http://localhost){:target="_blank"}

```


## Télécharger Wordpress

[https://fr.wordpress.org/](https://fr.wordpress.org/){:target="_blank"}

Déplacer suite le dossier dézippé à l'adresse `/var/html/www/` :

```
sudo unzip wordpress-4.9-fr_FR.zip -d wordpress
sudo cp wordpress /var/html/www/
cd /var/html/www/
sudo mv wordpress/* .
sudo rm -r wordpress
sudo rm -r index.html

```
On supprime 'indexl.html' la page par défaut.

## Créer la base de donnée mysql

l'utlisateur par defaut est "root" avec un password vide

```
sudo mysql -u root

```

Une fois sql lancé, on tape  : 

```SQL
mysql> create database wordpress;
mysql> create user nomUtilisateur;
mysql> set password for nomUtilisateur = PASSWORD("monMotDePasse");
mysql> GRANT ALL PRIVILEGES ON wordpress.* TO nomUtilisateur@localhost IDENTIFIED by "monMotDePasse";
```

# Activer .htaccess overide




```
sudo nano /etc/apache2/apache2.conf
```
et ajouter à la fin du fichier, les lignes suivantes : 


```
<Directory /var/www/html/>
    AllowOverride All
</Directory>
```

# Donner les droits en ecriture à l'utilisateur apache

```
ps aux|grep apache
```
Normalement, l'utilisateur `root `et plusieurs `www-data` sont présents.

```

```
sudo chown  -R www-data /var/www
```
On permet ainsi à `www-data` de modifier le dossier `/var/www`
---
1. En voulant télécharger un document j'obtiens l'erreur :

```
Impossible de créer le dossier wp-content/uploads/2017/11. Son dossier parent est-il accessible en écriture par le serveur ?
```

Il faut changer les droit du dossier où le site se situe `/var/www`

---

# Activer le module Rewrite 

```
sudo a2enmod rewrite
sudo systemctl restart apache2

```




# Finaliser l'installation de wordpress

Si tout se passe bien, vous devriez voir la page wordpress d'installation s'afficher, il suffit alors de rentrer les informations utilisées pour la création de la base de donnée mysql.
On vous demandera enfin pour finaliser l'installation Wordpress 4.9, de créer un fichier `wp-config.php` et d'y insérer les lignes contenant votre configuration effectuée. 



## Ajouter un templates


## Sources :
+ [https://doc.ubuntu-fr.org/lamp](https://doc.ubuntu-fr.org/lamp){:target="_blank"}
+ [https://www.it-connect.fr/installation-de-wordpress-sous-linux/#IV_Decompression_de_larchive_dans_varwww](https://www.it-connect.fr/installation-de-wordpress-sous-linux/#IV_Decompression_de_larchive_dans_varwww){:target="_blank"}
+ [https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-lamp-on-ubuntu-16-04](https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-lamp-on-ubuntu-16-04){:target="blank"}
