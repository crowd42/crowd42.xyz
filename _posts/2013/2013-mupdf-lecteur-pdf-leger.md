---
layout: post
title : "MUPDF : un lecteur PDF très léger"
date:   2013-10-10 21:12:11
categories:
    - blog
tags:
    - GNU/Linux
    - pdf
    - mupdf
---

Je suis un addict des applications légères, il faut dire qu’avec mon laptop qui commence à devenir un peu vieux je n’ai pas trop le choix. Ainsi dès que je peux remplacer un logiciel avec un autre plus léger et moins gourmand, je le fais sans hésitation. Une de mes dernières trouvailles est MuPDF, un lecteur pdf ultra léger. Bien plus léger que epdfview par exemple.

Pour autant, mupdf n’est pas dépourvu de fonctionnalités, au contraire, il n’a rien à envier aux autres lecteurs que j’utilisais jusqu’à présent, notamment epdfview. Mais ce qui m’a séduit le plus, c’est son côté Vim-like. En effet, son interface est épurée et ne contient aucun raccourci ou bouton de fonction, tout se gère via les touches clavier. Les vimistes seront ravis.

MuPDF est disponible dans les dépôts de toutes les distributions majeures, cependant, j’invite les utilisateurs d’ubuntu et de Debian GNU/Linux à passer par le dépôt ppa du projet, afin de profiter d’une version plus récente que celle proposée dans les dépôts officiels.

Pour installer MuPDF sur Debian GNU/Linux ou Ubuntu, ouvrez un terminal et exécutez les lignes de commandes suivantes :
~~~
sudo add-apt-repository ppa:guilhem-fr/mupdf
sudo apt-get update
sudo apt-get install mupdf
~~~

![mupdf]({{ site.baseurl }}/images/posts/2013/mupdf.png "MUPDF")

Je vous invite à consulter le manuel (man mupdf) pour connaître les différentes commandes de MuPDF. Par exemple pour faire un zoom sur le fichier ouvert suffit d’appuyer sur “+”, pour chercher une occurrence dans le texte “/”, pour le défilement h,j,k,l, bref comme avec Vim.

### Lines
~~~
[0]: https://www.mupdf.com
