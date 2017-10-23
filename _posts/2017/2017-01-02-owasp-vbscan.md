---
layout: post
title:  "Petite astuce pour ne plus saisir mot de passe git"
date:   2017-10-23 11:15:00
categories:
    - blog
tags:
    - git
    - github
    - astuce
---

Un petit billet pour partager une astuce et qui est surement connu de la quasi majorité des personnes
qui utilisent Git, mais je tiens à la partager quand même parce qu'on sait jamais, qui sait, 
    peut être qu'un newbie (rien de péjoratif) va tomber dessus et pour me remercier, il va prier que je gagne le loto !

Alors oui l'astuce. Donc quand vous cloner/initialiser un dépôt Git, à chaque fois que vous faites un "push",
      git vous demande de saisir votre nom d'utilisateur et mot de passe. Ça peut vite devenir pénible si vous
      êtes amenés à le faire plusieurs fois par heure/jour.

Pour t'éviter de petit calvaire toi petit noob, il te suffit d'exécuter ces deux lignes de commande :
~~~
$ git config --global credential.helper cache
~~~

Par défaut Git va se rappeler de votre pseudo/mot de passe pendant 15 minutes, vous pouvez modifier ce comportement avec cette commande :
~~~
git config --global credential.helper 'cache --timeout=3600'
~~~

Voilà voilou :p
