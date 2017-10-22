---
layout: default
title:  "Installer Raspbian 8 pour une Raspberry Pi sans écran"
date:   2017-10-22 14:30:00 +0200
categories: Raspberry Raspbian
tag: Raspberry Raspbian Jessie Installation 
---


# Flasher la carte SD 


Il faut tout d'abord situer l'emplacement de la carte SD insérée dans le pc.
Pour cela, il faut taper 

```BASH 
df

```
Dans mon cas :
```BASH
$ df
Sys. de fichiers blocs de 1K  Utilisé Disponible Uti% Monté sur
udev                 3997296        0    3997296   0% /dev
tmpfs                 804760    10100     794660   2% /run
/dev/sda2          238798492 13505080  213093376   6% /
tmpfs                4023780    40288    3983492   2% /dev/shm
tmpfs                   5120        4       5116   1% /run/lock
tmpfs                4023780        0    4023780   0% /sys/fs/cgroup
/dev/loop0            147456   147456          0 100% /snap/brackets/21
/dev/loop1             85120    85120          0 100% /snap/core/3017
/dev/sda1             523248     4684     518564   1% /boot/efi
tmpfs                 804756       16     804740   1% /run/user/121
tmpfs                 804756     3676     801080   1% /run/user/1000
/dev/mmcblk0p1         41322    20761      20561  51% /media/memo/boot
/dev/mmcblk0p2       1169348   757768     334128  70% /media/memo/f2100b2e-fd82-4647-b5ae-089280112716

```

Démonter les lecteurs associés à la SD , dans mon cas j'ai 2 partitions (  associées à une ancienne config rapsbian) : `/dev/mmcblk0p1` et `/dev/mmcblk0p2` .

```SHELL
sudo umount -l /dev/mmcblk0p2 /dev/mmcblk0p1
```

Une fois que vous avez récupéré la version de Raspbian , vous pouvez flasher votre carte SD en lignes de commande assez simplement. Dans mon cas , j'ai dézipper raspbian  depuis le dossier de Téléchargement, j''écris donc : 

```SHELL
sudo dd if=Téléchargements/2017-04-10-raspbian-jessie-lite.img of=/dev/mmcblk0
```


Après quelques "longues" minutes, le systeme est copié  et vous obtenez normalement  un message du type :

```BASH
2534888+0 enregistrements lus
2534888+0 enregistrements écrits
1297862656 bytes (1,3 GB, 1,2 GiB) copied, 269,062 s, 4,8 MB/s

```

# Placer un fichier vierge `ssh` dans la partition boot

Une fois la carte SD flashée, vous devez voir s'afficher deux partitions dont une se nomme boot, il faudra y placer un fichier nommé `ssh` pour que la rapsberry accepte la connexion ssh au demarrage :

```
cd /media/memo/boot/
touch ssh
```


# Configurer une IP statique pour la raspberry PI

Il faut tout d’abord récupérer des informations sur la connexion , notamment connaitre l’adresse de la porte du routeur :

```
ip route | grep default | awk '{print $3}'
```

dans mon cas : 

``` BASH
192.168.1.254
```

Il faut ensuite modifier le fichier dhcpd.conf présent sur la plus grosse des deux partitions de la carte sd ( celle qui contient tous les fichiers sources necessaires à la pi ):


```SHELL
cd /media/memo/f2100b2f-ed84-4647-b5ae-089280112716
sudo nano ./etc/dhcpcd.conf
```
et insérer à la fin du fichier : 

```
#Allouer une IP STATIQUE

interface eth0
static ip_address=192.168.1.80/24
static routers=192.168.1.254
static domain_name_servers=208.67.222.222 208.67.220.220
interface wlan0
static ip_address=192.168.1.81/24
static routers=192.168.1.254
static domain_name_servers=208.67.222.222 208.67.220.220
```


où `192.168.1.80` est l'adresse IP réservée pour la connexion en ethernet et `192.168.1.81` l'ip réservée lorsque le pi est connectée en WIFI.


#Configurer le réseau Wifi ( si necessaire )

si vous souhaitez que la raspberry PI soit connectée en WIFI, il faudra modifier le fichier `wpa_supplicant.conf` :

```SHELL
sudo nano etc/wpa_supplicant/wpa_supplicant.conf
```

en ajoutant votre réseau et le mot de passe associé 



```SHELL
network={
        ssid="MonRéseauWifi"
        psk="LeMotDePasseWifi"
        key_mgmt=WPA-PSK
}
```

Remarque : Il est conseillé de le modifier plus tard depuis la pi et utiliser `wpa_passphrase` pour qu'il ne soit pas inscrit en "clair" dans le fichier, en tapant `wpa_passphrase "MonRéseauWifi"` )

# Se connecter à la raspberry
La carte est enfin prete, une fois installée dans la rapsberry pi, on s'y connectera ( en Wifi )avec la commande :

```
ssh pi@192.168.1.81
```
avec le mot de passe par défaut `rapsberry` .



Sources :

* [Installation de Rapsbian sur une carte SD à partir d'Ubuntu](https://www.generation-linux.fr/index.php?post/2013/01/29/Installation-de-Rapsbian-sur-une-carte-SD-%C3%A0-partir-d-Ubuntu){:target="_blank"}
* [Mettre en place une Raspberry Pi sans écran ni clavier](https://raspbian-france.fr/raspberry-pi-sans-ecran-sans-clavier/){:target="_blank"}
