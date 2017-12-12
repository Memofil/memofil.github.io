---
layout: default
title:  "Premierspas avec Webdriver et Ubuntu 17.10"
date:   2017-12-08 10:25:00 +0200
categories: Webdriver 
tags : [Webdriver, Maven, Java, Ubuntu]
---

# Installation

## Installation Java 9 sur Ubuntu 17.10
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update -y
sudo apt-get install oracle-java9-installer
```

## Installer Maven 3.5

Télécharger le zip `apache-maven-3.5.2-bin.zip` à la page :
+ [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi){:target="_blank"}


Puis décompresser l'archive, se dépacer à l'interieur et copier le contenu dans `/opt/`
```
cd apache-maven-3.5.2-bin/
mv apache-maven-3.5.2/ maven
sudo cp -r maven /opt/

```
Il faut ensuite ajouter la libraire aux variables d'environnement :

Au niveau du Home, on édite le fichier `~/.profile`
```
sudo nano ~/.profile

```
et on y ajoute à la fin du fichier les lignes suivantes : 

```
## Chemin vers Maven
M2_HOME=/opt/maven
PATH=$PATH:$M2_HOME/bin
export M2_HOME
export PATH

```
On peut verifier alors que maven a bien été ajouté :

```
echo $M2_HOME
```
on devrait alors voir s'afficher : 

```
/opt/maven
```

Pour connaitre la version de maven installée: 

```
mvn -v
```
## Liens ## 
+ [http://toolsqa.com/selenium-tutorial/](http://toolsqa.com/selenium-tutorial/){:target="_blank"}
