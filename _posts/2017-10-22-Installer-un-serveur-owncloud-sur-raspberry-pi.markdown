---
layout: default
title:  "Installer un serveur Owncloud sur rapsberry pi sous Raspbian 8"
date:   2017-10-22 14:30:00 +0200
categories: Raspberry Raspbian
tag: Raspberry Raspbian Jessie Installation 
---


# Installer Owncloud

```SHELL
sudo apt-get update
sudo apt-get install owncloud
```
# Install mySQL et créer votre base de donnée

```SHELL
sudo apt-get install mysql-server
```

## Configurer apache pour qu'il accepte des gros fichiers:
Pour cela, modifier la taille limite des envois dans le fichier `/etc/php5/apache2/php.ini`, à deux endroits :
`post_max_size = 1024M ` et `upload_max_filesize = 1024M`

## Créer la base de donnée mySQL :


```
mysql –u root –p
```
On vous demandera alors de rentrer le mot de passe créé lors de l'installation de mysql.


Vous entrez ensuite  les commandes : 

```
CREATE USER 'nomUtilisateur'@'localhost' IDENTIFIED BY 'motDePasse';
CREATE DATABASE IF NOT EXISTS owncloud;
GRANT ALL PRIVILIGES on owncloud.* TO 'nomUtilisateur'@'localhost' IDENTIFIED BY 'motDePasse';
```


# Activer votre serveur
Tout d'abord, redemarrer apache :
```
systemctl restart apache2.service
```

Votre owncloud est pret à etre configurer via le navigateur internet à l'adresse : `192.168.1.80/owncloud/`

Vous pouvez alors créer un compte admin .
Pour configurer la partie concernant la base de donnée, on aura : 

```
Utilisateur : nomUtilisateur
Mot de passe de la base : motDePasse
Nom de la base de donnée : owncloud
```


# Configurer owncloud pour pouvoir s'y connecter depuis l'exterieur

Si vous souhaitez utiliser utiliser en dehors de votre réseau local , il faudra y acceder via l'adresse ip publique de votre connexion internet. Il faudra aussi prendre quelques précaution pour sécurisez l'accès.


## Ouvrir un port de forwarding

Si vous utilisez une connexion internet via une box telque freebox , i est possible simplement de mettre en place une redirection de port (voir  : [Acceder à son raspberry pi en dehors de son réseau local](https://memofil.github.io/raspberry/linux/terminal/2017/05/15/AccederAsonRaspberryDepuisInternet-via-ssh.html){:target="_blank"})

### Configuration sur le port 80

Pour passer via le port 80 ( http par defaut) , il faut que la redirection s'ecrive telle que :
```
port exterieur : 1002 ( celui que vous voulez)
port interieur : 80
Protocole : TCP :
IP : l'IP du serveur en local , dans notre cas : 192.168.1.80
```


### Connexion via le navigateur : 

Dans le cas ou mon IP serait : 23.542.54.65, il suffit d'écrire dans l'url du navigateur
```
23.542.54.65:1002
```

Vous tombez alors sur la page du serveur apache par défaut du raspi  qui vous  indique que l'adresse point bien sur ce dernier

en tapant : 

```
23.542.54.65:1002/owncloud/
```
Vous devriez avoir un message d'erreur de la part d'owncloud : ` You are accessing the server from an untrusted domain.`

Il faut en effet ajouter l'adresse IP au fichier `/etc/owncloud/config.php` à la suite de l'adresse ip locale déja présente : 


```
  'trusted_domains' => 
  array (
    0 => '192.168.0.144',
    1 => '23.542.54.65',
  ),

```


Il est alors possible de se connecter à owncloud via l'IP publique ! Un (gros) probleme demeure la connexion n'est alors pas sécurisé car nous passons par le protocole http et non https. Pour remedier à cela , nous allons utiliser les certificats SSS.

## Utiliser les certificats SSL pour sécuriser la connexion

### Créer un hote virtuel owncloud pour le serveur apache

```
cd /etc/apache2/sites-available/
sudo nano owncloud.conf

```

on insere alors :

```
<VirtualHost *:443>
DocumentRoot /usr/share/owncloud
SSLEngine On
SSLOptions +FakeBasicAuth +ExportCertData +StrictRequire
SSLCertificateFile /etc/ssl/certs/owncloud.crt
SSLCertificateKeyFile /etc/ssl/private/owncloud.key
</VirtualHost>

```

où `/usr/share/owncloud` est le dossier racine ( par défaut ) du stockage.
Il faut ensuite activer le module ssl et ajouter `owncloud.conf` aux sites actifs d'apache :

```
a2enmod ssl
service apache2 restart
a2ensite owncloud.conf
service apache2 reload
```


Il faut ensuite interdire l'accès au serveur en http, pour cela on doit forcer owncloud à utiliser `https`.
```
cd /usr/share/owncloud/config/
sudo nano config.php
```

et  ajouter la ligne :

```
'forcessl' => true
```


### creation des cetificats 

```
cd /etc/apache2/ 
mkdir CertOwncloud
openssl genrsa -out owncloud.key 1024
openssl req -new -key owncloud.key -out owncloud.csr
openssl x509 -req -days 365 -in owncloud.csr -signkey owncloud.key -out owncloud.crt
cp owncloud.crt /etc/ssl/certs
cp owncloud.key /etc/ssl/private
service apache2 restart


```
Sources :

* [Installer un serveur OwnCloud sur Raspberry Pi](http://www.raspberrypi-france.fr/serveur-owncloud-raspberry-pi/){:target="_blank"}

* [ownCloud 10.0.3 Server Administration Manual](https://doc.owncloud.org/server/latest/admin_manual/configuration/database/linux_database_configuration.html#db-binlog-label){:target="_blank"}

* [Sécuriser ownCloud par HTTPS/SSL](https://www.it-connect.fr/securiser-owncloud-par-httpsssl/){:target="_blank"}

