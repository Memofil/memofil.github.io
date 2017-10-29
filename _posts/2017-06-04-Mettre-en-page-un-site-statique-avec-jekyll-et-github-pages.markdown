---
layout: default
title:  "Mettre en page un site statique avec Jekyll et Github Pages"
date:   2017-05-22 00:09:36 +0200
categories: Jekyll 
tags : Github-Pages Jekyll
---

# Mettre en page un site statique avec Jekyll et Github Pages

## Choisir un thème officiel compatible Github page

Github pages propose une liste de thèmes compatibles à l'adresse : 
+[https://pages.github.com/themes/](https://pages.github.com/themes/){:target="_blank"}
Afin de les utiliser, il faut suivre la procédure d'installation indiqué à l'adresse du dépot du theme choisi.

Dans notre cas, nous choisissons le theme [**tactile** (un thème sobre et responsive)](https://github.com/pages-themes/tactile){:target="_blank"} :

### Installation du thème

1. Ouvrir le fichier "_config.yml" à la racine de votre site et ajouter le nom du thème :
{% highlight ruby %}
theme: jekyll-theme-tactile
{% endhighlight %}
2. Pour que le thème soit actif aussi en local, vous pouvez modifier le ".gemfile", en ajoutant : `gem "github-pages", group: :jekyll_plugins`, puis lancer 
```BASH
bundle update github-pages
```
3. Il faut enfin ajouter ou modifier le fichier "_layouts/default.html" en faisant un copier/coller du template présent sur le dépot en ligne d thèmé choisit. 
Dans notre cas :[https://github.com/pages-themes/tactile/blob/master/_layouts/default.html](https://github.com/pages-themes/tactile/blob/master/_layouts/default.html){:target="_blank"}
4. Le push une fois effectué, la page rafraichie et l'historique effacé, le nouveau thème devrait actif!

**Remarques :**

+ Si le thème précédent était 'minima', le thème par défaut chargé à la création du site, ces procédures ne sont pas suffisantes. 

  - Il faudra aussi effacer toute les références à "minima", que ce soit dans le `config.yml`, `about.md` et `gemfile`.
  - Il faudra aussi modifier les premières lignes de tous les articles et pages déja écrites en remplacant `layout: post` par `layout: default`

On remarquera alors que la page d'accueil n'affiche plus les liens vers les articles, comme pouvez le faire minima. Nous allons voir par la suite, comment mettre en page son site et récupérer boutons et fonctionnalités.



## Ajouter une barre de navigation (navbar)

[https://www.taniarascia.com/responsive-dropdown-navigation-bar/](https://www.taniarascia.com/responsive-dropdown-navigation-bar/){:target="_blank"}

## Créer un barre de navigation avancée 

[https://learn.cloudcannon.com/jekyll/advanced-navigation/](https://learn.cloudcannon.com/jekyll/advanced-navigation/
){:target="_blank"}

Il va falloir créer un fichier "navigationTree.yml" qui va nous permettre d'ordonner les pages dans le menu. 
Ainsi à la racine du site :

```
mkdir -p _data
nano navigationTree.yml
```

On integre ensuite la liste des pages de notre site telle que :
```
- link: /
  name: Home
- link: /about/
  name: About
- link: /services
  name: Services
```

Puis dans le fichier `_includes/navigation.html` ( créé précédement pour la barre de navigation "simple" ), il faut insérer les lignes suivantes ;
```HTML
{% raw %}
 {% for item in site.data.navigation %}
    <a href="{{ item.link %}" {% if item.link == page.url %}class="active"{% endif %}>
      {{ item.name }}
    </a>
  {% endfor %}

{% endraw %}
```

Personnaliser la page d'accueil d'un site statique sous Jekyll
Le contenu de la page d'accueil se situe dans le fichier `index.md`


## Afficher les derniers articles

## Créer une nouvelle Page ##
Pour créer une nouvelle page, il suffit de copier la page "about.md" et de la renommée.
Toutes les nouvelles pages doivent etre enregistrées à la racine du site.


## Comment ajouter un sommaire ( TOC : Table of Content) 
Avec krawdow sous github pages, il faut inserer dans l'article : 
```
* TOC
{:toc}
```
Résultat : 

* TOC
{:toc}

## Comment ajouter une image

```
![titre image]({{ site.url }}/assets/image.png)
```
## Comment insérer un lien vers une autre page de son site
Exemple d'un lien qui pointe vers cet article : 
```text
{% raw %}[--> Mettre en page un site satique]({% post_url 2017-06-04-Mettre-en-page-un-site-statique-avec-jekyll-et-github-pages %})
{% endraw %}
```
Résultat : [Mettre en page un site statique]({% post_url 2017-06-04-Mettre-en-page-un-site-statique-avec-jekyll-et-github-pages %})

## Comment insérer un bout de code sur une ligne
Pour avoir `index.htlm` , il faut entourer le mot par le caractère **`**, tel que : 

```text
{% raw %}`index.html`{% endraw %}
``` 


## Personnaliser le template avec Bootstrap

### Installer Bootstrap pour Jekyll
Boostrap fonctionne nativement avec less, pour utiliser Bootstrap avec Jekyll qui utilise Sass, on doit installer [Bootstrap-sass](https://github.com/twbs/bootstrap-sass#a-ruby-on-rails){:target="_blank"} via les gem Ruby : 

```
sudo gem install bootstrap-sass
```


## Liens ## 
+ [http://literaturegeek.com/2017/02/04/building-research-website-with-jekyll-githubpages-theming](http://literaturegeek.com/2017/02/04/building-research-website-with-jekyll-githubpages-theming){:target="_blank"}
+ [http://veithen.github.io/2015/03/26/jekyll-bootstrap.html](http://veithen.github.io/2015/03/26/jekyll-bootstrap.html){:target="_blank"}
+ [https://kvurd.com/blog/my-jekyll-blog-setup-bootstrap-sass-pygments/](https://kvurd.com/blog/my-jekyll-blog-setup-bootstrap-sass-pygments/){:target="blank"}
