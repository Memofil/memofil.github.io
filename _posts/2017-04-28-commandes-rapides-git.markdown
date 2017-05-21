---
layout: post
title:  "Commandes rapides Git"
date:   2017-04-28 10:30:00 +0200
categories: Git Linux Terminal 
---

Installer Git
{% highlight ruby %}
sudo apt-get install git-all
{% endhighlight %}

Modifier le fichier .gitconfig (présent dans à la racine du dossier personel):
{% highlight ruby %}
user] 
    email = mon.email@mail.com (associé au compte github)
    name = mon.nom 

 [alias] 
    ci = commit 
    co = checkout 
    st = status 
    br = branch  
{% endhighlight %}


Cloner un dépot github?

1. Se place dans le répertoire Git
2. Récupérer l'adresse du dépot que l'on veut cloner

{% highlight ruby %}
git clone https://github.com/(Adresse-du-répertoire)
{% endhighlight %}


Créer un nouveau dépot

1. Se place dans le répertoire Git
2. Créer le dossier

{% highlight ruby %}
mkdir mon_depot
cd mon_depot
git init
{% endhighlight %}




Connaitre le status des modifications

{% highlight ruby %}
git status
{% endhighlight %}

Connaitre l'historique des modifications

{% highlight ruby %}
git log
{% endhighlight %}


Afficher les différences entre 2 fichiers modifiés

{% highlight ruby %}
git diff
git diff <commit1> <commit2>
{% endhighlight %}

Connaitre le status des modifications

{% highlight ruby %}
git status
{% endhighlight %}

Gestion des versions
Ajouter une nouvelle version d'un fichier
{% highlight ruby %}
git add <mon_fichier_ou_dossier>
{% endhighlight %}
ou bien pour l'intégralité d'un dossier
{% highlight ruby %}
git add *
{% endhighlight %}

Effacer le fichier
{% highlight ruby %}
git rm <mon_fichier>
{% endhighlight %}


Déplacer le fichier
{% highlight ruby %}
git mv <mom_fichier> <nouvelle_destination>
{% endhighlight %}

Gestion des commits

Mettre à jour le dépot avant tout commit pour récupérer les modifications des autres utilisateur
{% highlight ruby %}
git pull
{% endhighlight %}

Faire un commit
Pour un nouveau fichier :
{% highlight ruby %}
git add mon_fichier
git commit mon_fichier
{% endhighlight %}


Pour des fichiers déja existant
{% highlight ruby %}
git commit -a
{% endhighlight %}


Faire un commit avec commentaires :
{% highlight ruby %}
git commit -a -m "Mon commentaire"
{% endhighlight %}

Envoyer les fichiers sur GitHub sur la branche master du dépot origin
{% highlight ruby %}
git push origin master
{% endhighlight %}
ou simplement
{% highlight ruby %}
git push 
{% endhighlight %}




[source][source]
[source]: https://doc.ubuntu-fr.org/git
[source2][source2]
[source2]: https://git-scm.com/book/fr/v2

