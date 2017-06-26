---
layout: default
title:  "Problèmes reccurents avec Github Pages"
date:   2017-05-22 00:09:36 +0200
categories: Github Pages
---

# Problèmes reccurents avec Github Pages #

## Mon site ne s'affiche plus : La page est blanche##

Apres avoir voulu changer de template GithubPages, la page d'acceuil de mon site statique est devenu blanche.
Comment donc récupérer un site fonctionnel?

Il faut essayer de faire tourner le site en local.



Dans le répertoire de la page Github :


S'assurrer que ruby est bien installé, ruby va ensuite installer les dépendances necessaires indiqué par le gemfile présent à la racine du répertoire.

{% highlight ruby %}
 sudo apt-get install ruby-dev
 bundle install
{% endhighlight %}

voici la réponse du terminal :

{% highlight ruby %}
Warning: the running version of Bundler is older than the version that created the lockfile. We suggest you upgrade to the latest version of Bundler by running `gem install bundler`.
Fetching gem metadata from https://rubygems.org/............
Fetching version metadata from https://rubygems.org/...
Fetching dependency metadata from https://rubygems.org/..
Using public_suffix 2.0.5
Using colorator 1.1.0
Installing ffi 1.9.18 with native extensions
Using forwardable-extended 2.6.0
Using sass 3.4.23
Using rb-fsevent 0.9.8
Using kramdown 1.13.2
Using liquid 3.0.6
Using mercenary 0.3.6
Using rouge 1.11.1
Using safe_yaml 1.0.4
Using bundler 1.11.2
Using addressable 2.5.1
Installing rb-inotify 0.9.8
Installing pathutil 0.14.0
Installing jekyll-sass-converter 1.5.0
Installing listen 3.0.8
Installing jekyll-watch 1.5.0
Installing jekyll 3.4.3
Installing jekyll-feed 0.9.2
Installing minima 2.1.0
Bundle complete! 4 Gemfile dependencies, 21 gems now installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.
Post-install message from minima:

----------------------------------------------
Thank you for installing minima 2.0!

Minima 2.0 comes with a breaking change that
renders '<your-site>/css/main.scss' redundant.
That file is now bundled with this gem as
'<minima>/assets/main.scss'.

More Information:
https://github.com/jekyll/minima#customization
----------------------------------------------

{% endhighlight %}

 
On tente ensuite de démarrer le serveur
 
 {% highlight ruby %}
   bundle exec jekyll serve
{% endhighlight %}

Si le terminal ne renvoi aucune erreurs, le site est alors disponible à l'adresse : <code>http://localhost:4000</code>


<h3>Erreur :</h3>

 {% highlight ruby %}
Configuration file: /home/fabien/git/monsite.github.io/_config.yml
Configuration file: /home/fabien/git/monsite.github.io/_config.yml
jekyll 3.4.3 | Error:  The jekyll-theme-dinky theme could not be found.
{% endhighlight %}

Dans le fichier "_congig.yml" on a fait référence theme dinky mais ce dernier est introuvable. Deplus, on remarque que le theme qui vient d'etre installé via le gemfile est "minima 2.0". 
Voici donc la source du conflit.

1. Il faut alors éditer le fichier 'config.yml', mettre en commentaire <code>#gem "minima", "~> 2.0"</code> et ajouter : <code>gem "github-pages", group: :jekyll_plugins</code>
2. Taper : <code> bundle update github-pages</code> , les themes par défaut de github vont etre installés
3. Il faut changer le layout dans chaque page te article. Avec minima, au debut de chaque page, nous avions <code> layout : post </code>, on écrit à la place <code> layout : default </code> or "post" ne signifie plus rien, il faut alors créer le répertoire _layouts et y ajouter une page ' default.html' que l'on trouvera sur le dépots du theme choisi. C'est cette struture de page qui sera utilisée.

Sources : 
<a href="https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#step-4-build-your-local-jekyll-site" target="_blanck">https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#step-4-build-your-local-jekyll-site</a>

https://github.com/pages-themes/dinky

http://literaturegeek.com/2017/02/04/building-research-website-with-jekyll-githubpages-theming




## Deux comptes github, Problème avec les clefs ssh ##
 Après la configuration d'un nouveau compte github sur le même pc, on a du créer une nouvelle clef ssh. voir l'article Comment créer deux comptes github . Cependant le nouveau compte crée fonctionne mais plus le premier. Si l'host ( configuré dans `.ssh/config` est github-primaire , en tapant : `ssh -T git@github-primaire`, on obtient : 

```SHELL
Connection to github.com closed by remote host.

```

Face à ce probleme de clef, le mieux est d'affecter une clef speciale pour chaque compte github sans utiliser celle de base (cad : id_rsa). Puis supprimer celles en trop ou inutile. Sous Ubuntu 16.04, la solution qui a marché est d'ouvrir l'application : "Mots de passe et clefs" ( passwords and keys) et de les supprimer à la main.

La solution peut se trouver à cette adresse :

[https://stackoverflow.com/questions/25464930/how-to-remove-a-ssh-key](https://stackoverflow.com/questions/25464930/how-to-remove-a-ssh-key){:target="_blanck"}


Attention : Voir aussi la suite ci- desous, car mofifier ".git/config" peut aboutir a de nouveaux bugs.

## Apres une modification du fichier ".git/config", les mises à jour ne fonctionnent plus ( localement et en ligne )##

Lorsque je tape `bundle exec Jekyll serve `, j'obtiens : 


```SHELL
 No repo name found. Specify using PAGES_REPO_NWO environment variables, 'repository' in your configuration, or set up an 'origin' git remote pointing to your github.com repository.
``` 
 
 Une solution (proposée [ici](https://github.com/jekyll/jekyll/issues/4705){:target="_blanck"}) consiste à indiquer le chemin du dépot dans le fichier `_config.yml`. 
 Dans le cas d'une page GitHub, on ajoutera alors la ligne suivante : `repository: username/username.github.io`.