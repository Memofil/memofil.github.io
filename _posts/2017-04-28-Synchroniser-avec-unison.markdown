---
layout: default
title:  "Synchroniser avec Unison"
date:   2017-04-28 12:30:00 +0200
categories: Linux Unison Terminal 
tags : Linux Unison Terminal 
---

<h3>Installer Unison</h3>
{% highlight ruby %}
sudo apt-get install unison
{% endhighlight %}

Attention, pour qu'unison fonctionne correctement , il faut que les deux machines que vous souhaitez Synchroniser dispose de la meme version d'unison.
Si les pc n'ont pas le même systeme d'exploitation, les dépots sont généralement différents et vous pouvez avoir un message d'erreur du type : 
{% highlight ruby %}
Contacting server...
Fatal error: Received unexpected header from the server:
 expected "Unison 2.40\n" but received "Unison 2.48\n\000\000\000\000\017", 
which differs at "Unison 2.48".
This can happen because you have different versions of Unison
installed on the client and server machines, or because
your connection is failing and somebody is printing an error
message, or because your remote login shell is printing
something itself before starting Unison.
{% endhighlight %}

Dans ce cas, il faut installer Unison manuellement. A defaut de trouver une version déja compilée pour notre raspberry, nous allons partir du code source.
Comme Unison est ecrit en OCaml, il est necessaire d'avoir Ocaml pour pouvoir compiler.

{% highlight ruby %}
sudo apt-get install ocaml
wget http://www.seas.upenn.edu/~bcpierce/unison//download/releases/unison-2.48.1/unison-2.48.1.tar.gz
tar -zxvf unison-2.48.1.tar.gz
cd unison-2.48.1/
sudo make UISTYLE=text
#On deplace ensuite le dossier compilé dans le répertoire des applications perso "/opt", puis on génére un lien symbolique
sudo cp -r ../unison-2.48.1 /opt/
cd /usr/bin
sudo ln -s /opt/unison-2.48.1/unison unison
{% endhighlight %}


Pour plus de détails d'installation, vous pouvez récupérer <a href="http://www.seas.upenn.edu/~bcpierce/unison//download/releases/unison-2.48.1/unison-2.48.1-manual.pdf">la notice</a>

<h3>Utiliser Unison pour synchroniser la Raspberry PI avec un serveur distant  </h3>

Connaissant l'adresse IP du serveur distant ainsi que l'hostname, par exemple "12.34.56.78" et "bob". Pour synchroniser le contenu de deux dossier d1 (présent sur la pi) et d2 (présent sur le serveur distant), il suffit de taper :

{% highlight ruby %}
./unison -batch /home/pi/d1 ssh://bob@12.34.56.78//home/bob/d2
{% endhighlight %}
