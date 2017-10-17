---
layout: post
title:  "Générer un dictionnaire de mots de passe"
date:   2016-11-27 12:15:00
categories:
    - blog
tags:
    - infosec
    - penetration testing
    - hacking
---
## Introduction

Lorsqu'un pentester réussi à s'introduire dans le système informatique de sa
cible, une de ses premieres actions serait de trouver un moyens d'élever ses
privilèges (privileges escalations), par exemple de passer d'un compte de simple
utilisateur à celui d'administrateur. Le moyen le plus "simple" serait que le
pentester récupère les hashs de mots de passe (on va partir de l'idée que les
dev n'ont pas fait la boulette de stocker les mdp en plain text).

Un script kiddie, une fois qu'il a les hashs va surement fait chauffer son
CPU/GPU en lançant John The Ripper ou oclHashcat (paramètres par défaut bien
évidemment, car il n'était pas foutu de lire la doc) avec une liste de mots de passe
comme `rockyou.txt`, après plusieurs heurs et de Wuts d'électricité gaspillé pour
rien, il laissera tomber et passera à autre chose.

Un bon pentester par contre aurait procédé différemment. Au lieu de s'attaquer
directement au cassage des mots de passe avec un dictionnaire comme rockyou, il
aurait généré un dico spécialement pour la cible à partir de son site web par
exemple, il aurait généré un dico spécialement pour la cible à partir de son
site web par exemple. Un des tools que j'utilise personnellement c'est CeWl,
     prononcé `cool` [lien pour télécharger \[0\]][0]

### Qu'est-ce que c'est CeWl ?

CeWL (Custom Wordlist Generator) est générateur de dico qui a été conçu pour
parcourir un site web et de collecter des mots clés et de les compiler dans une
liste.

CeWL dispose de plusieurs paramètres qui le rendent encore plus puissant, on
peut par exemple le nombre de lien à suivre, le nombre de caractères dans chaque
mot, inclure les adresses email et plus encore. Prenons l'exemple suivant.

~~~
$ cewl http://www.example.com -d 1 -m 6 -w dicto.txt
~~~

Tout d'abord on indique à CeWL l'url du site, ensuite le nombre de lien à suivre
(-d). Le nombre minimum de caractères dans chaque mot qu'on va ajouter à notre
dico est 6 (d'ailleurs faut qu'un jour qu'on m'explique pourquoi une bonne
        partie des sites web continuent à des mot de passe aussi faibles). Enfin
le dernier paramètre permet comme vous en doutez de spécifier un fichier ou
l'output de notre commande sera sauvegardé.

Pour connaitre le nombre de mots de passe généré par CeWL, il suffit d'exécuter
cette ligne de commande :


~~~
$ wc -l dicto.txt
1337 dico.txt
~~~

### Faites entrer John The Ripper

Grâce à CeWL on a réussi à compiler une liste de mots clés que notre cible
aurait pu utiliser pour ses mots de passe, mais avec eux uniquement on ira pas
loin. C'est là qu'entre en jeu JTR. John tire en grosse partie sa puissance des
régles que l'on peut appliquer à nos wordlists, on peut voir ces règles; les
éditer, en ajouter via le fichier de conf `/etc/john/john.conf` dans la rubrique
`# Wordlist mode rules`. Vous pouvez en apprendre plus sur les règles de JTR et
de leurs syntaxe en se rendant sur [cette page \[1\]][1]

~~~
# Wordlist mode rules
[List.Rules:Wordlist]
# Try words as they are
# Lowercase every pure alphanumeric word
-c >3 !?X l Q
# Capitalize every pure alphanumeric word
-c (?a >2 !?X c Q
# Lowercase and pluralize pure alphabetic words
<* >2 !?A l p
# Lowercase pure alphabetic words and append '1'
<* >2 !?A l $1
# Capitalize pure alphabetic words and append '1'
-c <* >2 !?A c $1
# Duplicate reasonably short pure alphabetic words (fred -> fredfred)
<7 >1 !?A l d
# Lowercase and reverse pure alphabetic words
>3 !?A l M r Q
# Prefix pure alphabetic words with '1'
>2 !?A l ^1
~~~

On peut par exemple ajouter cette régle qui va nous permettre d'ajouter quatre
chiffres à la fin des mots de passe :

~~~
# Ajoute quatre chiffres à la fin de chaque mot de passe
$[0-9]$[0-9]$[0-9]$[0-9]
~~~

Comme vous l'avez sans doute deviné, cette ligne va nous aidez avec les mots de
passe du genre "mdp2016", "mdp1980"...
On peut maintenant exécuter John pour appliquer ces régles à notre liste de mots
de passe générée par CeWL :

~~~
john --wordlist=dico.txt --rules --stdout > nouveau-dico.txt
~~~

Pour voir la différence, tapons de nouveau dans un terminal notre commande tout
à l'heure :

~~~
$ wc -l nouveau_dico.txt
212564 nouveau_dico.txt
~~~

Bon Cassage ;-)

## Liens

~~~
[0]: https://github.com/digininja/CeWL/
[1]: http://www.openwall.com/john/doc/RULES.shtml 
~~~

[0]: https://github.com/digininja/CeWL/
[1]: http://www.openwall.com/john/doc/RULES.shtml
