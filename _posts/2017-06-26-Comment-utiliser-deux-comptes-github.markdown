---
layout: default
title:  "Comment utiliser deux comptes Github"
date:   2017-06-26 8:30:00 +0200
categories: Github 
---
## Comment utiliser deux comptes Github sur un même ordinateur? ## 
 
Dans le cas où vous utilisez les Github Pages, et que vous souhaitez avoir un deuxième site, vous aurez besoin d'avoir un deuxième compte Github, puisque le site est à l'adresse : username.github.io. Evidement pour d'autres raisons ( compte personnel, compte professionnel...), cette necessité peut se faire sentir. Heuresement, Github permet cette situation. Il va falloir créer d'autres clefs SSH.

### Création de la nouvelle clef SSH ###

Génerer une nouvelle clef associé au mail utilisé pour nouveau compte Github
```Shell
ssh-keygen -t rsa -C "monSecondMail@mail.com"
```
et l'enregistrer avec un autre nom que le nom par défaut afin de ne pas écraser celle qui existe déja : 
```Shell
Generating public/private rsa key pair.
Enter file in which to save the key (/home/fabien/.ssh/id_rsa): /home/Moi/.ssh/id_rsa_monSecondMail_git
```
### Enregistrer la nouvelle clef SSH sur le compte Github###

Déposer la nouvelle clef sur le compte Github va permettre d'identifier et autoriser le pc à utiliser les services git. Pour ce faire, aller dans `settings>SSH and GPG keys> New SSH key` et copier-coller le contenu de la clef  en faisant ` cat /home/Moi/.ssh/id_rsa_monMail_git.pub`

### Créer un fichier config pour gérer les clefs SSH ###
Afin que votre ordinateur sache quelle clef appeler lors de la connexion aux services git, il va falloir créer un fichier `/home/Moi/.ssh/config` dans lequel on indiquera le chemin des clefs à utiliser pour chaque compte. Dans notre cas, on y ajoutera les informations suivantes :

```SHELL
# compte primaire
  Host github-primaire
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_monPremierMail_git

# compte secondaire
  Host github-secondaire
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_monSecondMail_git

```
### Modifier le fichier `monDepotGit/.git/config` ###

Afin que les dépots des 2 comptes github prennent bien la bonne clef SSH, il va falloir modifier les fichiers "config" present dans le dossier `.git` de chaque dépot. On veillera alors que le fichier contienne bien les informations suivantes ( pour le dépot associé au deuxiemme compte"):
```SHELL
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[user]
        name = monNomUtilisateurGithub
        email = monSecondMail@mail.com
[remote "origin"]
        url = git@github-secondaire:monNomUtilisateurGithub/monDepot.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
        remote = origin
        merge = refs/heads/master


```
Faire de même pour le ou les dépots associé au premier compte.

Enfin on verifiera que la connexion se passe bien : 

```Shell
ssh -T git@github-secondaire
```

En retour , on devra avoir :

```Shell
Hi monNomUtilisateurGithub! You've successfully authenticated, but GitHub does not provide shell access.

```

On peut alors utiliser son deuxième en renseignant simplement le nom d'utilisateur et le mot de passe associé, le fichier config s'occupera du reste

Remarque : Si vous utilisez la clef ssh id_rsa ( par defaut) pour le premier compte, il peut y avoir des conflits d'autorisation et des problemes de connexions ( [voir: Problemes recurrents ](https://memofil.github.io/github/pages/2017/05/22/Problemes-reccurents-avec-github-pages.html){:target="_blanck"} ).
Une solution est d'avoir une clef personnel pour chaque compte github que vous utilisez.


## Sources : ##
* [http://sametmax.com/utiliser-deux-comptes-github-separement/](http://sametmax.com/utiliser-deux-comptes-github-separement/){:target="_blanck"}

* [https://coderwall.com/p/7smjkq/multiple-ssh-keys-for-different-accounts-on-github-or-gitlab](https://coderwall.com/p/7smjkq/multiple-ssh-keys-for-different-accounts-on-github-or-gitlab){:target="_blanck"}
* [https://confluence.atlassian.com/bitbucket/configure-multiple-ssh-identities-for-gitbash-mac-osx-linux-271943168.html](https://confluence.atlassian.com/bitbucket/configure-multiple-ssh-identities-for-gitbash-mac-osx-linux-271943168.html){:target="_blanck"}