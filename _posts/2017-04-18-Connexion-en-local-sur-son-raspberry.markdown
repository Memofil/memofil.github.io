---
layout: post
title:  "Se connecter en local sur son Rapsberry Pi via ssh"
date:   2017-04-17 10:37:00 +0200
categories: raspberry pi raspbian ssh 
---
Comment se connecter à distance sur son Rapsberry Pi via ssh en local ?

{% highlight ruby %}
ssh pi@192.168.0.XX
{% endhighlight %}

Créer un clef ssh pour éviter d'écrire le password a chaque connexion : 

Génèrer la clef
    {% highlight ruby %}
    ssh-keygen
    {% endhighlight %}

Puis envoyer sur le serveur distant ( autrement dit la raspberry)
    {% highlight ruby %}
    ssh-keygen
    ssh-copy-id grainedi@192.168.0.XX
    {% endhighlight %}




[source][source]
[source]: https://raspbian-france.fr/controlez-raspberry-pi-ssh-ordinateur/
