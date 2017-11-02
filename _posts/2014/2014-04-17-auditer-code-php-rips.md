---
layout: post
title:  "Auditer la sécurité de votre code PHP avec RIPS"
date:   2014-04-17 21:15:00
categories:
    - blog
tags:
    - audit code
    - sécurité
    - Infosec
    - audit
    - RIPS
    - php
---
Je n’ai pas des statistiques sous la main, mais je crois que ne pas me tromper en disant que le PHP est le langage le plus populaire pour faire du développement web. La majorité des personnes qui souhaitent s’initier à la programmation le choisissent comme premier langage.

Malheureusement cette popularité a son lot d’inconvénients, une bonne partie des tutoriaux qu’on trouve sur le net négligent un chapitre majeur : la sécurité. Vous serez étonnés de voir le nombre de failles (surtout les SQL injection) qu’on peut trouver dans le code de certains sites web, mêmes ceux développés par des grosses agences web.

Pour auditer votre code il existe RIPS, un petit soft très sympa qui permet de trouver des failles SQLI, RCE, XSS, LFI, RFI, etc en toute simplicité ! Tout ce que vous avez à faire c’est de copier/coller votre code dans le champ réservé à ça et RIPS va s’occuper du reste. RIPS possède d’autres fonctionnalités mais elles nous n’intéressent pas dans ce billet (utilie si vous faites du pentesting).

Pour installer RIPS, il suffit d’avoir un serveur web (apache ou nginx par exemple) et PHP sur sa bécane, ensuite [téléchargez l’archive de RIPS \[0\]][0] et décompressez la dans votre répertoire de travail (/var/www par exemple). Le reste c’est un jeu d’enfant, vous renseignez le chemin vers le fichier contenant que le code que vous souhaiter auditer et vous cliquez sur “scan” !
![static code analyser rips]({{ site.baseurl }}/images/posts/2014/rips.png "screenshot rips")

Vous trouverez sur le site du projet plus de détails sur les fonctionnalités de RIPS pour une utilisation plus avancée, donc n’hésitez pas à le consulter.
