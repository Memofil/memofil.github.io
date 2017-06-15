---
layout: default
title:  "Commandes rapides Git"
date:   2017-04-28 10:30:00 +0200
categories: Git Linux Terminal 
---

<h2>Commandes rapides Git </h2>

<h3> Préalables </h3>
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


<h3>Comment cloner un dépot github?</h3>

1. Se place dans le répertoire Git
2. Récupérer l'adresse du dépot que l'on veut cloner

{% highlight ruby %}
git clone https://github.com/(Adresse-du-répertoire)
{% endhighlight %}


<h3>Créer un nouveau dépot</h3>

1. Se place dans le répertoire Git
2. Créer le dossier

{% highlight ruby %}
mkdir mon_depot
cd mon_depot
git init
{% endhighlight %}




<h3>Connaitre le status des modifications</h3>

{% highlight ruby %}
git status
{% endhighlight %}

<h3>Connaitre l'historique des modifications

{% highlight ruby %}
git log
{% endhighlight %}


<h3>Afficher les différences entre 2 fichiers modifiés</h3>

{% highlight ruby %}
git diff
git diff <commit1> <commit2>
{% endhighlight %}

<h3>Connaitre le status des modifications</h3>

{% highlight ruby %}
git status
{% endhighlight %}

<h3>Gestion des versions</h3>
Ajouter une nouvelle version d'un fichier
{% highlight ruby %}
git add <mon_fichier_ou_dossier>
{% endhighlight %}
ou bien pour l'intégralité d'un dossier
{% highlight ruby %}
git add *
{% endhighlight %}

<h3>Effacer le fichier</h3>
{% highlight ruby %}
git rm <mon_fichier>
{% endhighlight %}


<h3>Déplacer le fichier</h3>
{% highlight ruby %}
git mv <mom_fichier> <nouvelle_destination>
{% endhighlight %}

<h2>Gestion des commits</h2>

<h3>Mettre à jour le dépot avant tout commit pour récupérer les modifications des autres utilisateur
{% highlight ruby %}
git pull
{% endhighlight %}

<h3>Faire un commit</h3>
Pour un nouveau fichier :
{% highlight ruby %}
git add mon_fichier
git commit mon_fichier
{% endhighlight %}


<h3>Pour des fichiers déja existant</h3>
{% highlight ruby %}
git commit -a
{% endhighlight %}


<h3>Faire un commit avec commentaires :</h3>
{% highlight ruby %}
git commit -a -m "Mon commentaire"
{% endhighlight %}

<h3>Envoyer les fichiers sur GitHub sur la branche master du dépot origin</h3>
{% highlight ruby %}
git push origin master
{% endhighlight %}
ou simplement
{% highlight ruby %}
git push 
{% endhighlight %}

<h3>Faire un push sans mot de passe</h3>
Il est possible de stocker l'identifiant et le mot de passe pour eviter d'avoir à les retaper à chaque push via les "credential.helper".
Pour enregistrer l'identifiant et le mot de passe pendant une heure, à la racine du dépot on tapera :
<br>
{% highlight ruby %}
git config --global credential.helper "cache --timeout=3600"
git push
{% endhighlight %}
Une fois les informations renseignées la porte restera ouverte pendant une heure.

<br>

<h4>Sources :</h4>

<ul>
<li>
<a href=" https://doc.ubuntu-fr.org/git" target="_blanck">https://doc.ubuntu-fr.org/git</a>
</li>
<li>
<a href="https://git-scm.com/book/fr/v2" target="_blanck">https://git-scm.com/book/fr/v2</a>
</li>
</ul>

