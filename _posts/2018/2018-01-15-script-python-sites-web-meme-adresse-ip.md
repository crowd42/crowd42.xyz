---
layout: post
title: "Un petit script pour récupérer les URLs des sites web hébergés sur la même adresse IP"
date: 2018-01-16 19:30:10
categories: 
    -blog
tags:
    - infosec
    - python
    - bing
    - osint
    - pentest
---

Dans un de mes derniers articles ([Comment j'ai pu gagner un accès administrateur sur un serveur Windows 2012 grâce à Google \[0\]][0]), j'ai évoqué comment j'ai utilisé le moteur de recherche de Microsoft afin de trouver les sites web qui sont hébergés sur le même serveur web d'un client lors d'un test d'intrusion. 

Pour ceux qui ont la flemme d'aller jeter un coup d'œil à l'article en question, on peut obtenir ces sites web en laçant la requête suivante :
~~~
ip: 93.184.216.34 (l'adresse IP du site example.com)
~~~

Dans les cas où les résultats ne dépassent pas cinq voire même un peu plus, ça reste gérable, on peut copier et coller les urls dans un fichier pour les utiliser plus tard. Cependant, si on est face à plus d'une dizaine d'urls, le copier/coller devient beaucoup moins pratique et très fatiguant. C'est la raison pour laquelle j'avais écrit un script python pour automatiser cette tâche. 

C'est un script python très banal et je suis quasiment certain que si j'avais pris le temps de le chercher sur le web, j'aurais surement trouvé une meilleure version que la mienne, mais voilà, j'en avais besoin et je l'ai écrit.

Pour utiliser ce script vous aurez besoin de vous enregistrer sur le site des [services Azure de Microsoft \[1\]][1] pour obtenir votre clé API (je pense que je vais réaliser une deuxième version de ce script en utilisant [requests \[2\]][2] et [BeautifulSoup \[3\]][3] afin d'éviter l'inscription chez Microsoft).

Son utilisation est très simple :
~~~
usage: ip_bing.py [-h] [-i IP] [-c COUNT] [-f FILE] [-o OFFSET]

Find websites hosted on the same IP address

optional arguments:
  -h, --help            show this help message and exit
  -i IP, --ip IP        The IP address of the web server
  -c COUNT, --count COUNT
                        Number of results to return
  -f FILE, --file FILE  Save the output into a text file
  -o OFFSET, --offset OFFSET
                        start in results number x, default: 0
~~~

Par défaut le script ne va afficher que les dix premièrs résultats :
~~~
python ip_bing.py -i  93.184.216.34
~~~

Pour obtenir plus de résultat utilisez l'argument -c (--count) :
~~~
python ip_bing.py -i  93.184.216.34 -c 40
~~~

Avec cette commande, vous obtiendrez les premiers 40 résultats, à condition bien évidemment que le moteur de recherche trouve 40 résultats ou plus.

Vous pouvez aussi spécifier la page par laquelle vous souhaitez commencer :
~~~
python ip_bing.py -i  93.184.216.34 -c 20 -o 30
~~~

Dans l'exemple ci-dessus ip_bing va récupérer les vingts premiers résultat mais à partir de la quatrième page.

Enfin pour sauvegardé les urls dans un fichier ajouter l'argument -f à votre commande :
~~~
python ip_bing.py -i  93.184.216.34 -c 20 -o 30 -f urls_example_com.txt
~~~

Voilà ci-dessous le script en question, faites en ce que vous voulez :-)

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import argparse
import requests

# ip_bing take 3 arguments, the last two are optional
parser = argparse.ArgumentParser(
    description="Find websites hosted on the same IP address")
parser.add_argument('-i', '--ip', help="The IP address of the web server")
parser.add_argument('-c', '--count', help='Number of results to return')
parser.add_argument('-f', '--file', help='Save the output into a text file')
parser.add_argument(
    '-o',
    '--offset',
    help='start in results number x, default: 0')
args = parser.parse_args()

if not args.ip:
    parser.print_help()
    exit()
# Subscription key which provides access to this API.
headers = {'Ocp-Apim-Subscription-Key': 'PASE_YOUR_KEY_HERE'}

# Request URL
url = "https://api.cognitive.microsoft.com/bing/v7.0/search"

# The keyword (dork) to pass to bing
keyword = 'ip:' + args.ip
payloads = {'q': keyword, 'count': args.count, 'offset': args.offset}
response = requests.get(url, params=payloads, headers=headers)

# Get the response as json content
content = response.json()
data = content['webPages']['value']
for i in range(len(data)):
    print(data[i]['url'])
    # We also the save output as file in the current directory, so we can use
    # later with other programs for example
    try:
        with open(args.file, 'a') as f:
            f.write(data[i]['url'] + '\n')
    except TypeError:
        pass
{% endhighlight %}

### Liens
~~~
[0]: https://crowd42.github.io/comment-jai-pu-gagner-acces-administrateur-serveur-windows-grace-google/
[1]: https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/
[2]: https://github.com/requests/requests
[3]: https://www.crummy.com/software/BeautifulSoup/#HallOfFame
~~~
[0]: https://crowd42.github.io/comment-jai-pu-gagner-acces-administrateur-serveur-windows-grace-google/
[1]: https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/
[2]: https://github.com/requests/requests
[3]: https://www.crummy.com/software/BeautifulSoup/#HallOfFame
