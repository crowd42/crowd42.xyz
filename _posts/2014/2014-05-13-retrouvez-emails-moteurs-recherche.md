---
layout: post
title:  "Retrouver les adresses emails que vous cherchez avec TheHarvester"
date:   2014-05-13 21:15:00
categories:
    - blog
tags:
    - reconnaissance
    - infosec
    - TheHarvester
    - email
    - scraping
---
J’ai une amie sur Twitter qui me demande, de temps en temps, de lui trouver les contacts mails depuis un nom de domaine. TheHarvester est un des outils dont je m’en sers pour l’aider (y a aussi un script nmap et maltego pour ne citer qu’eux).

En fait, TheHarvester ne fait pas que retrouver les adresses email à partir d’un nom de domaine, mais il permet de lister les autres sites web hébergé sur la même adresse ip et beaucoup plus encore. Un simple theharvester -h et vous aurez accès aux différentes options et fonctionnalité de l’outil.

TheHarvester n’est pas disponible dans les dépôts des distributions GNU/Linux (à part le dépôt communautaire AUR d’Archlinux). On va d’abord installer Subversion, si ce n’est pas déjà fait, vous pouvez le faire en exécutant la commande suivante :

~~~
$ git clone https://github.com/laramies/theHarvester
~~~

On va ensuite déplacer le répertoire qu’on vient de décompresser vers /opt/ :
~~~
$ sudo mv theharvester /opt/theharvester
~~~

Et pour qu’on puisse exécuter notre soft en toute simplicité, on va créer un lien symbolique de theharvester.py vers /usr/bin/ :
~~~
ln -s /opt/theharvester/theharvester.py /usr/bin/theharvester
~~~
Maintenant passons aux choses sérieuses et voyons comment utiliser TheHarvester pour collecter les adresses emails à partir d’un nom de domaine. Supposons qu’on veut retrouver les contacts mails du centre d’investissement de Laayoune (le bled où je vis). Soyez rassurés, on va rien “pirater”, TheHarvester n’est pas un exploit tool, donc du point de vue légal vous ne risquez rien, car les informations qu’on va collecter sont déjà disponible sur le Web et elles ont été publié par leurs détenteurs.

Dans notre premier exemple on va demander à TheHarvester d’aller chercher les adresses email sur toutes les sources disponibles (google,bing,bingapi,pgp,linkedin,google-profiles,people123,jigsaw) :
~~~
theharvester -d laayouneinvest.ma -b all
~~~
Comme vous l’aurez sans doute deviné, l’option -d permet de spécifier la cible, quant à l’option -b c’est pour définir les source sur lesquelles on va chercher les adresses email. Dans notre exemple nous avons demandé à TheHarvester d’utiliser toutes les sources, mais on aurait pu en spécifier qu’une seule :
~~~
theharvester -d laayouneinvest.ma -b google
~~~
Par défaut, TheHarvester cherche dans les 100 premiers résultats des moteurs de recherche, mais si on n’est pas satisfait du résultat obtenu, on peut ajouter une autre option à notre ligne de commande :
~~~
theharvester -d laayouneinvest.ma -b google -l 300
~~~
Et si vous souhaitez sauvegarder le résultat de la commande d’un fichier :

theharvester -d laayouneinvest.ma -b google -f fichier.html (ou .xml)

Et voilà c’est tout pour ce petit tuto, enjoy it ￼

### Liens
~~~
[0]: https://github.com/laramies/theHarvester
~~~
[0]: https://github.com/laramies/theHarvester

