---
layout: default
title:  "Bugs reccurents - Raspberry PI"
date:   2017-04-18 00:09:36 +0200
categories: Bug Raspberry Raspbian
---
Bugs Reccurents sur Raspbian Jessie

La session (via l'interface graphique) ne s'ouvre plus alors que les identifiants sont corrects.

Hypothèse : Le clavier est en mode qwerty par défaut, 
Solution : Avec un clavier azeerty, si le mot de passe par défaut est raspberry, il faut taper :  rqspberry.

Hypothèse : Il y a peut etre eu un changement de droit sur l'OS suite à des installations mal déroulées, Pi n'est plus admin. 
Solution : Il faut accéder au raspberry via une connexion ssh et rétablir les droits de l'utilisateur pi

1. une connexion en ssh avec pi et le mot de passe associé
2. - sudo chown pi:pi /home/pi/.Xauthority (chown=changement du propriétaire et du groupe)
3. Redemarrer
- 3 - depuis l'interface graphique de la raspberry -> Eteindre (ou à la sauvage débranche/rebranche)
- 4 - redémarrer votre Raspberry et tout il est beau !


https://www.raspberrypi.org/forums/viewtopic.php?f=65&t=45072