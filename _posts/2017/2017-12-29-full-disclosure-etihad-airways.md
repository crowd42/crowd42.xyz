---
layout: post
title: "Full Disclosure : Des emails et mots de passe de la compagnie aérienne Etihad Airways dans l'air"
date: 2017-12-28 01:01:01
categories:
    - blog
tags:
    - infosec
    - brèche
    - leak
    - etihad
    - HackerOne
    - coup de gueule
    - ful-disclosure
---

Il y a près de deux mois, je discutais avec [@href \[0\]][0] un sujet dont je me rappelle plus les détails (désolé, on va mettre ça sur le dos de la vieillesse et la mémoire qui commence à flancher), tout ce dont je me rappelle c'est que ça parlait d'emailing et de [web scraping \[1\]][1] (ou pas, je ne me rappelle vraiment pas). Parce que juste après je me suis lancé dans l'écriture d'un script python (tout pourri je dois avouer) qui prenait comme argument un [Google dork \[2\]][2] :

~~~
$ python email_harvester.py -d "site:.com +@ gmail.com|yahoo.com"
~~~

Le but était de voir combien d'adresse email je pouvais collecter en une heure. Le script n'avait rien de spécial, il cherchait des fichiers sur le web qui contenaient des adresses email et les sauvegarder dans un répertoire. Le script affichait aussi les liens en cours de traitement. Sauf qu'à la première exécution du script, j'ai remarqué un nom de domaine qui m'a obligé à arrêter le programme : [etihadmediacentre.com](http://etihadmediacentre.com). Pour ceux qui ne le savent Etihad est une compagnie aérienne émaratie, elle est dans le top 3 des plus grandes/meilleures compagnies aériennes au monde. Pourquoi j'ai arrêté le script ? Le petit bout de code va vous donner élément de réponse :

{% highlight python %}
# Filter-out unrelated links and extract actual URL from Google's.
        if i.get('href').startswith('/url?') and not i.get('href').startswith(
                "/url?q=http://webcache.googleusercontent.com"):
            extract = re.findall(r"q=(.*\.sql)", i.get('href'))
            for link in extract:
                get_emails(link)
                print(link)

{% endhighlight %}

Vous l'avez remarquer le "*.sql" ? Ce bout bout du script va s'assurer de ne traiter que les liens avec l'extension .sql (des dumps sql) et le lien que j'ai vu dans mon terminal était un dump d'Etihad !

J'ai ouvert le site web dans mon navigateur et fait un whois du nom de domaine pour m'assurer que c'était bien un site web appartenant un à la compagnie aérienne Etihad Airways et non pas site web appartenant à des phishers comme je l'ai pensé pendant un petit moment de doute. Mon action suivante était d'aller vers la page qui contenait le dump sql :
<div>
    <img src="{{ site.baseurl }}/images/posts/2017/etihad_sql.png" style="width:75%"/>
</div>
<br/>

Si vous aviez bien regardé l'image, vous devriez avoir remarqué deux choses :
1. L'archive a été mis en ligne le 24 juillet 2017, il est donc très récent et les informations qu'il doit contenir sont probablement à leur tour très récentes ;
2. La taille du dump est assez conséquente, plus de 600Mo quand même.

J'ai téléchargé le dump sql ainsi que l'archive tar, légalement parlant ce n'est pas répréhensible, tout ce que j'ai fait c'est d'accéder à des fichiers disponible publiquement (même si le juge de l'affaire bluetouff pense différemment). Ensuite j'ai exporté le dump sql vers un serveur mysql pour les examiner.

Deux tables ont attiré mon attentions : root_users et users, j'ouvre la première je copie un hash d'un mot de passe pour l'identifier avec [hash-identifier \[2\]][2] :
~~~
   #########################################################################
   #     __  __                     __           ______    _____           #
   #    /\ \/\ \                   /\ \         /\__  _\  /\  _ `\         #
   #    \ \ \_\ \     __      ____ \ \ \___     \/_/\ \/  \ \ \/\ \        #
   #     \ \  _  \  /'__`\   / ,__\ \ \  _ `\      \ \ \   \ \ \ \ \       #
   #      \ \ \ \ \/\ \_\ \_/\__, `\ \ \ \ \ \      \_\ \__ \ \ \_\ \      #
   #       \ \_\ \_\ \___ \_\/\____/  \ \_\ \_\     /\_____\ \ \____/      #
   #        \/_/\/_/\/__/\/_/\/___/    \/_/\/_/     \/_____/  \/___/  v1.1 #
   #                                                             By Zion3R #
   #                                                    www.Blackploit.com #
   #                                                   Root@Blackploit.com #
   #########################################################################

   -------------------------------------------------------------------------
   HASH: fc36a188c2e9554f0c19bf28520ec187
   Possible Hashs:
[+]  MD5
[+]  Domain Cached Credentials - MD4(MD4(($pass)).(strtolower($username)))
~~~

Du MD5, à ce moment là j'espérais pour eux qu'aucun script kiddie n'ait découvert ce dump. Je vérifie quelques tables pour voir la dernière activité enregistré dans la base de données, même date que celle de la mise en ligne du dump sql. Ça commence à devenir chaud pour eux.

J'ai récupéré quelques adresses emails des gens qui travaillent pour Etihad Airways et Four Communication (la boite qui a développé le site web et qui gère leurs communications) depuis la base de données, et je leurs envoyais un email qui explique la situation et le risque qu'ils encourent. Dans ma naïveté, je me suis attendu à un message de retour d'eux au bout de 48 heures maximum ! C'était il y a presque deux mois et toujours aucune réponse.

Après plusieurs semaines sans réponse, j'ai décidé de leur passer un message via le programme "Disclosure Assistance" de [HackerOne \[3\]][3]. Quelques heures après l'avoir fait, j'ai reçu un email de leur part (hackerOne pas Etihad) me confirmant la "légitimité" de ma découverte.

<div>
    <img src="{{ site.baseurl }}/images/posts/2017/hackerone.png" style="width:75%"/>
</div>
<br/>

Encore une fois, naïf que je suis, j'ai pensé que la réputation de HackerOne allait les pousser à se bouger le c** et supprimer le dump sql, c'était il y a plus d'un mois.

Le risque qu'ils encourent est grand, ça m'a pris quelques minutes pour déchiffrer les mots de passe. Je vous laisse imaginer combien parmi les employés d'Etihad et Four Coummunication utilisent le même mot de passe pour plusieurs services. Mais ce n'est pas tout, les informations sur les employés d'Etihad Airways présentes dans la base de données sont une mine d'or pour un phisher : fonction dans l'entreprise, parfois même adresse et numéro de téléphone et bien évidemment leurs emails professionnels, imaginez les dégâts que ça peut faire si quelqu'un décide de lancer une campagne de phishing en spoofant les adresses emails présentes dans le dump.

Certains d'entre vous sont surement en train de se dire mais pourquoi alors je divulgue tout ça si c'est aussi risqué que ça ? Et bien tout simplement parce que j'en ai assez de ces entreprises, administrations publiques, etc qui s'en foutent de la sécurité de leurs sites web, applications, serveurs... Durant les dernières années je dois au moins avoir rapporté des failles chez une une bonne centaines d'entreprises et administrations, je peux vous assurer que le pourcentage de ceux qui m'ont répondu ne dépassent pas les 2%. Imaginez ma frustration quand je voyais des sites des universités, ministères, entreprises se faire piraté alors que j'avais remonté les mêmes failles qui ont permet ce piratage il y a plusieurs mois auparavant. 

Donc dorénavant, ce sera [full-disclsure \[4\]][4] dès que je découvre une faille et à eux de se démerder après.


### Liens
~~~
[0]: https://soc.ialis.me/@href
[1]: https://fr.wikipedia.org/wiki/Web_scraping
[2]: https://fr.wikipedia.org/wiki/Google_hacking
[3]: https://www.hackerone.com/
[4]: https://fr.wikipedia.org/wiki/Full_disclosure
~~~
[0]: https://soc.ialis.me/@href
[1]: https://fr.wikipedia.org/wiki/Web_scraping
[2]: https://fr.wikipedia.org/wiki/Google_hacking
[3]: https://www.hackerone.com/
[4]: https://fr.wikipedia.org/wiki/Full_disclosure
