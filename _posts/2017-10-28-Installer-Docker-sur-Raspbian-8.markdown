---
layout: default
title:  "Installer Docker sur rapsberry pi sous Raspbian 8"
date:   2017-10-28 17:30:00 +0200
categories: Raspberry Raspbian
tag: Raspberry Raspbian Jessie Installation 
---


# Installer Docker

```SHELL
sudo apt-get update
sudo apt-get upgrade
curl -sSL get.docker.com | sh
```


# Demarrer le daemon docker

```SHELL
 sudo systemctl start docker
```

# Afficher les infos du Docker
```SHELL
sudo docker info
```

# Afficher les processus actifs
```SHELL
docker ps
```
# Afficher les images
```SHELL
docker images
```
Sources :

* [Raspberry Pi : installer simplement Docker dans Raspbian Jessie](https://www.nextinpact.com/news/101174-raspberry-pi-installer-simplement-docker-dans-raspbian-jessie.htm){:target="_blank"}

* [Initiation à Docker](https://korben.info/video/initiation-a-docker){:target="_blank"}
