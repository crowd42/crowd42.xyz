---
layout: post
title:  "Choisir un bon mot de passe"
date:   2016-12-02 12:15:00
categories:
    - blog
tags:
    - infosec
    - passwords
    - hacking
---
Récemment j'ai mené un test d'intrusion (penetration testing) pour le compte
d'une petite entreprise marocaine, une boite de communication mais qui réalise
aussi des sites web pour ses clients (des grandes marques marocaines et
        internationales). Pour cette dernière activité elle employait deux
personnes : un dev web "spécialisé drupal" et un web designer slash web
designer... en plus d'une ou deux personnes avec des titres farfelus : degital
machin, vous voyez ce que je veux dire.

Si je me fie à ma mémoire, je crois que c'était à des p0wnages les faciles que
j'ai pu réalisé, il m'a fallu moins de 3 heures pour avoir accès à tout leurs
comptes emails, leur ERP, sites web de leurs clients, compte administrateur sur
un serveur d'emailing, etc. Les ordinateurs des employés était hors de scope, je
pouvais donc pas les attaquer.

Comment j'ai fait ? C'était très simple, trop simple je dirais même et à la
porté de n'importe quel wannabe pentester comme moi.
Lors de la phase reconnaissance, j'avais découvert un répertoire qui contenait
une vieille version du site de la boite, quelques tests manuels et j'ai vite
trouvé une faille file uploqd des XSS à gogo, mais bizarrement pas de SQLi !
Prochaine étape était de générer un backdoor avec [Weevely \[0\]][0] et j'ai
copié le code dans une dizaine de fichiers présents sur leur espace web.

Après je suis partie à la chasse des mots de passe, et c'est là que c'est devenu
"fun". Je me suis placé dans le répertoire "Mail" et à coup de "grep" j'ai
récupéré presque TOUT les mots de passe de la boite (ceux du wifi compris) ainsi que de ceux de leurs clients, le reste John The Ripper s'en est occupé.
Les deux développeurs ont eu cette géniale idée de transmettre les mots de passe
des comptes qu'ils créaient en mail et "plain text", mais ce n'était pas leur
seule boulette, voilà un aperçu de leurs mdp :

* prenom2015
* prenom2016
* entrepsie2014
* service2015
* ...

Et quand ils voulaient compliquer les choses, ils ajoutaient un @ à la fin des
mdp, j'étais partagé entre deux vie : partir dans un fou rire, ou me tirer les
cheveux.

J'ai ensuite téléchargé le code source du site web pour un audit plus poussé
histoire de trouver des vulnérabilités que j'aurais loupé et j'ai passé un coup
de fil au CEO de la boite pour lui annoncer la nouvelle. Son expression de
visage quand je lui ai montré mes trouvailles était "priceless".

Ce qu'il faut retenir de tout ça ?

- Utiliser des combinaisons de lettres, chiffres et caractères spéciaux d'au
moins 12 caractères ;
- Éviter à tout prix d'utiliser vos noms, prénoms, num de téléphone, date de
naissance dans vos de mots de passe ;
- Utiliser un gestionnaire de mot de passe ;
- Éviter les mots de passe avec le nom de la boite/service dedans
- Et surtout évitez d'envoyer les mots de passe dans vos échanges email en
clair, je ne compte plus le nombre de fois où j'ai pu constater cette pratique
chez des boites, c'est comme si vous inscrivez vos mots de passe dans des
post-it et les collez sur vos ordis.. oh wait !
- Instaurer une password policy dans votre boite, ça peut être un peu chaud au
début à faire respecter par tout vous employés, mais croyez moi, elle vous
sauvera de plusieurs catastrophes.


## Liens

~~~
[0]: [https://github.com/epinna/weevely3]
~~~
[0]: [https://github.com/epinna/weevely3]
