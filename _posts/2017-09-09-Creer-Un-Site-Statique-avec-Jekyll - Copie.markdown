---
layout: default
title:  "Créer un site statique avec Jekyll"
date:   2017-09-09 8:30:00 +0200
categories: Jekyll 
tags: Jekyll ftp 
---

# Jekyll : Pour commencer

Jekyll permet de créer en un rien de temps des sites statiques modifiables très facilement.
Développer par les équipes du projet Github, il est impossible d'obtenir un hebergement gratuit open-source (  [voir Gihub Pages](https://pages.github.com/){:target="_blank"} ) et synchroniser son site web comme un dépot GIT. 
Mais il est aussi possible de déployer son site statique sur une plateforme d'hebergement privée comme ovh ou free, en passant alors par le protocole FTP.

+ [Mettre en page un site statique]({% post_url 2017-06-04-Mettre-en-page-un-site-statique-avec-jekyll-et-github-pages %}){:target="_blank"}

## Installer un site Jekyll en local 
En mode administrateur (avec Bash Ubuntu pour windows: 
```
sudo gem install jekyll bundler
jekyll new monSite
cd monSite

```
Le site est créé automatiquement, pour qu'il soit accessible en local, avec un terminal il faut se rendre à la racine du répertoire du site et entrer les commandes : 
```
bundle exec jekyll serve
```


## Installer Jekyll sur une page perso Free

### Préalable 
Afin de transférer son site Jekyll deployé en local par le protocole ftp.


### Synchroniser via lftp

```
lftp ftp://login:password@host -c "mirror --delete --reverse --exclude-glob dossierExclu /repertoire_local /repertoire_distant"
```

### Synchroniser Jekyll avec Glynn
#### Installer Glynn
```BASH
sudo gem install glynn --no-ri --no-rdoc
```
#### Modifier le fichier `_config.yml`
Insérer les lignes suivantes dans le corps du fichier : 
```
ftp_host: 'ftpperso.free.fr'  
ftp_dir: '/'  
ftp_passive: false

# optional
ftp_port: 21 # default 21  
ftp_username: 'NomUtilisateur' # default read from stdin
```
### Synchroniser
Dans le repertoire local du site, tapez :
```
glynn
```

## Sources :
+ [https://darryldias.me/07/deploy-jekyll-using-ftp/](https://darryldias.me/07/deploy-jekyll-using-ftp/){:target="blank"}
+ [https://www.christopheducamp.com/2014/01/12/deploiement-jekyll/](https://www.christopheducamp.com/2014/01/12/deploiement-jekyll/){:target="_blank"}
+ [http://www.leunen.com/linux/2010/06/synchroniser-deux-repertoires-distants-par-ftp/](http://www.leunen.com/linux/2010/06/synchroniser-deux-repertoires-distants-par-ftp/){:target="_blank"}
+ [https://www.dewep.net/realisations/script-shell-pour-synchroniser-fichiers-ftp](https://www.dewep.net/realisations/script-shell-pour-synchroniser-fichiers-ftp){:target="_blank"}
