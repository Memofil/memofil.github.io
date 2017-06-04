---
layout: default
title:  "Problème reccurent avec Github Pages"
date:   2017-05-22 00:09:36 +0200
categories: Github Pages
---

<h3>Mon site ne s'affiche plus : La page est blanche</h3>

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


<h3>Erreur numéro 1 :</h3>

 {% highlight ruby %}
Configuration file: /home/fabien/git/monsite.github.io/_config.yml
Configuration file: /home/fabien/git/monsite.github.io/_config.yml
jekyll 3.4.3 | Error:  The jekyll-theme-dinky theme could not be found.
{% endhighlight %}

Dans le fichier "_congig.yml" on a fait référence theme dinky mais ce dernier est introuvable. Deplus, on remarque que le theme qui vient d'etre installé via le gemfile est "minima 2.0". 
Voici donc la source du conflit.



Sources : 
<a href="https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#step-4-build-your-local-jekyll-site" target="_blanck">https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#step-4-build-your-local-jekyll-site</a>

https://github.com/pages-themes/dinky