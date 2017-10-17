---
layout: post
title:  "Email extractor :  un script python pour extraire les adresses email depuis un fichier"
date:   2017-10-17 10:00:00
categories:
    - blog
tags:
    - python
    - infosec
    - penetration testing
    - dev
---

Lors de la pahse de reconnaissance d'une de mes missions de [test d'intrusion (penetration testing)\[0\]][0], il m'arrive souvent de tomber sur des fichiers contenant des centaines d'adresses emails, numéro de tél, adresses postales... et plein d'autres informations plus au moins utiles.

Et comme tout "informaticien" qui se respecte, ma fainéantise n'a pas d'égal, donc au lieu d'extraire avec des copier/coller les adresses emails pour les utiliser plus tard dans mes compagnes de phishing, j'avais écrit un petit script en python de quelques lignes qui le fait à ma place ey que j'ai décidé de partager aujourd'hui.

Le script connait quelques lacunes (et bugs) mais comme il faisait exactement ce que je lui ai demandé, je n'ai pas cherché à l'étoffer ou l'améliorer.

Son utilisation est simple :
~~~
python email_extractor.py input_file output_file
~~~

Où "input_file" est le fichier source contenant les adresses emails et output_file est le fichier où seront sauvegardés les emails extrait du fichier.

{% highlight python %}
#!/usr/bin/env python
# coding:utf-8

import re
import sys

if len(sys.argv) < 3:
    print('Usage: python email_extracter.py [input_file] [output_file]')
    sys.exit()

regex = re.compile(r'[\w\.-]+@[\w\.-]+')

# The input file
filename = sys.argv[1]

# The output file.
output_file = sys.argv[2]

with open(filename, 'r') as emailfile:
    email_list = emailfile.read().lower()

# Here re.findall() returns a list of all the found email strings
emails = re.findall(regex, email_list)

# Write the emails into the file, one per line
with open(output_file, 'w') as output_file:
    for email in emails:
        output_file.write(email + '\n')
{% endhighlight %}


### Liens
~~~
[0]:https://en.wikipedia.org/wiki/Penetration_test
~~~
[0]:https://en.wikipedia.org/wiki/Penetration_test

