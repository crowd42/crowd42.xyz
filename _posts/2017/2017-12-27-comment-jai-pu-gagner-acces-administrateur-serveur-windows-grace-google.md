---
layout: post
title: "Comment j'ai pu gagner un accès administrateur sur un serveur Windows 2012 grâce à Google"
date: 2017-12-27 11:15:40
categoeries:
    - blog
tags:
    - pentest
    - infosec
    - test d'intrusion
    - penetration testing
    - Windows
---

La semaine dernière j'ai effectué un [test d'intrusion \[0\]][0] pour le compte d'une agence web espagnole (dont je vais taire le nom pour des raisons évidentes). Le client m'avait fixé un délai de 4 jours pour réussir à trouver un moyens pour compromettre la sécurité des sites web de l'agence (pas ceux des clients) hébergés sur son serveur ainsi que ce dernier. Le [hameçonnage (ou phishing) \[1\]][1] et les attaques par force brute étaient était exclus du cadre (scope) de la mission. Il m'aura fallu à peine un peu plus de trois heures pour être sûr à 90% que j'allais réussir ce test d'intrusion. Ce n'est pas que je suis arrogant ou bien que je suis super bon dans mon travail, non détrompez vous, c'est juste que le client n'est pas très bon dans SON TRAVAIL.

J'ai commencé par énumérer tous les sites web hébergé sur le serveur en utilisant le moteur de recherche Bing et le script [theHarvester \[2\]][2]. En tapant IP:xxx.xxx.xxx.xxx sur le champ de recherche de Bing, où les x représentent l'adresse IP du client, on peut lister tous les sites web qui pointent vers cette même IP (il faut vérifier qu'il s'agit pas d'un CDN). Par exemple, voilà la résultat de la requête avec l'IP du serveur d'example.com

<div>
	<img src="{{ site.baseurl }}/images/posts/2017/bing.png" style="width:75%;"/>
</div>
<br />

Le résultat de cette recherche je l'ai passé à TheHarvester, j'ai pu ainsi récupérer une dizaine sites web (sous domaines) de sites web hébergés sur la même IP. 
~~~
$ theharvester -d example -b all -l 500
[+] Emails found:
------------------
Anna@example.com
admin@example.com
administrator@example.com
bo@example.com
dbmaster@example.com
hello@example.com
july@example.com

[+] Hosts found in search engines:
------------------------------------
[-] Resolving hostnames IPs... 
93.184.216.34:Www.example.com
93.184.216.34:www.example.com
[+] Virtual hosts:
-----------------
93.184.216.34	example.com
93.184.216.34	example

~~~

J'ai continué ma chasse aux informations en servant uniquement des outils [OSINT \[3\]][3] (enseignement de sources ouvertes), mais je ne vais pas tous les énumérer dans ce billet, je me contenterai d'évoquer les techniques (si on peut parler de technique) et outils qui m'ont permet de mener à bout ma mission. Muni de la liste des noms de domaines qui pointent vers l'adresse IP, j'ai commencé à chercher sur Google tous le fichiers (documents word, pdf, excel, sql, archive zip et rar, sql et surtout fichiers générés automatiquement tels que les .swp. C'est à ce moment que j'ai découvert le fichier `config.php.bak`.

En ouvrant le fichier avec mon éditeur de texte, j'ai trouvé l'identifiant et le mot de passe pour se connecter au serveur de la base de données. J'ai copié le nom d'utilisateur et le mot de passe dans le wiki je m'en sert, j'ai testé le mot de passe sur 4 sites web, à chaque fois j'ai réussi à me connecter en tant qu'administrateur ! C'est à ce moment là que j'ai su que j'allais réussir cette mission.

J'ai continué le test d'intrusion comme je l'avais planifié dès le départ, j'ai fini la phase de reconnaissance, j'ai ensuite scanné les sites web avec des scanners des vulnérabilités ainsi que manuellement, je me suis inscrit sur les sites et j'ai vérifié qu'il n'y avait pas de faille (j'avais constaté qu'ils utilisaient un CMS fait maison, ce qui m'a fait gagné beaucoup de temps dans mes scans).

Après avoir fini toute la panoplie de tests, je me suis connecté en tant qu'administrateur avec l'identifiant et le mot de passe que j'avais trouvé au début, avec l'aide [burp suite \[4\]][4] j'ai essayé de contourner les protections mis en place pour sécuriser l'upload sans succès. J'ai tenté de me connecter via SSH, pas de chance là non plus, seule l'authentification avec clé est autorisée. J'essaie alors de me connecter au serveur FTP et là bingo ! 

Je génère un backdoor avec l'excellent webshell [b374k \[5\]][5] et je l'upload. Une fois connecté à mon webshell, la première chose que j'ai fait c'est d'essayer de me connecter au serveur mysql avec le mot de passe que j'ai trouvé au début, là aussi BINGO ! Une trentaine de base données qui contiennent au total les informations (nom et prénom, email, adresse, numéro de téléphone, mots de passe...) de plus de deux millions clients ! (btw, je crois que j'ai oublié de vous dire que d'après les informations affichées dans le panneau d'administration de deux sites du client, ce dernier totalisait un CA de plus de 19 millions d'euros en 2017.).

Je pouvais m'arrêter là et rédiger mon rapport et l'envoyer au client, l'objectif principal de ce test d'intrusion était de voir si c'était possible ou pas de récupérer les données des clients. Mais pourquoi s'arrêter là alors que le fun ne fait que commencer :-).

J'avais 3 informations que j'avais collecté dans les premières phases du pentest dans ma possession :

1. Je savais que le serveur tournait sur un Windows server 2012;
2. Un port [rdp \[6\]][6] était ouvert;
3. Un serveur SSH (copSSH) est installé sur la machine mais qui n'autorise que les connexions par clé.

Je vais dans l'onglet `Terminal` de b374k et je crée un nouveau utilisateur 
~~~
net user toor MdP3240 /add
~~~

Je me connecte en utilisant [rdesktop \[7\]][7]

~~~
rdesktop -u toor adresse_ip_du_serveur
~~~

re re bingo !

<div>
	<img src="{{ site.baseurl }}/images/posts/2017/rdesktop.png" style="width:75%;"/>
</div>
<br />

J'ouvre le gestionnaire de fichier de Windows et je me déplace au dossier `C:\Program Files (x86)\copSSH\home\root\.ssh`, j'éditais le fichier `authorized_keys` pour y ajouter ma clé publique. Je pouvais maintenant accéder au serveur de 3 différentes manières.

<div>
	<img src="{{ site.baseurl }}/images/posts/2017/ssh.png" style="width:75%;"/>
</div>
<br />

Avant de supprimer l'utilisateur pour ne pas alerter l'administrateur du serveur qui aurait pu se connecter le matin en rentrant le matin et découvrir ce que je faisais, j'ai installé [Mimikatz \[8\]][8] et récupérer quelques hashs. En utilisant [CeWl et John The Ripper \[9\]][9] ainsi que quelques mots de passe qui était sauvegardés en clair les bases de données, j'ai pu enfin obtenir le mot de passe compte root de la machine \o/.

Quand j'en ai parlé avec le client pour lui annoncer les résultats du test d'intrusion (je fais souvent ça avant d'envoyer le rapport), il m'a avoué qu'il était persuadé que j'allais échouais, tellement il avait confiance dans "les mesures de sécurités" qu'il avait mis en place. Mais les deux erreurs qu'il a commis, ont été fatales pour lui : la sauvegarde du fichier de configuration non supprimée et l'utilisation du même mot de passe pour l'authentification dans plusieurs sites web et services.

J'espère que vous avez retenu la leçon derrière ce billet :-).


### Liens
~~~
[0]: https://fr.wikipedia.org/wiki/Test_d'intrusion
[1]: https://fr.wikipedia.org/wiki/Hame%C3%A7onnage
[2]: https://github.com/laramies/theHarvester
[3]: https://fr.wikipedia.org/wiki/Renseignement_d'origine_source_ouverte
[4]: https://portswigger.net/burp/
[5]: https://github.com/b374k/b374k
[6]: https://fr.wikipedia.org/wiki/Remote_Desktop_Protocol
[7]: http://www.rdesktop.org/
[8]: https://github.com/gentilkiwi/mimikatz
[9]: {{ site.baseurl }}/blog/generer-un-dectionnaire/
~~~
[0]: https://fr.wikipedia.org/wiki/Test_d'intrusion
[1]: https://fr.wikipedia.org/wiki/Hame%C3%A7onnage
[2]: https://github.com/laramies/theHarvester
[3]: https://fr.wikipedia.org/wiki/Renseignement_d'origine_source_ouverte
[4]: https://portswigger.net/burp/
[5]: https://github.com/b374k/b374k
[6]: https://fr.wikipedia.org/wiki/Remote_Desktop_Protocol
[7]: http://www.rdesktop.org/
[8]: https://github.com/gentilkiwi/mimikatz
[9]: https://crowd42.github.io/blog/generer-un-dectionnaire/

