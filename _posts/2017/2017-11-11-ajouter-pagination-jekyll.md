---
layout: post
title: "Comment ajouter une pagination à votre site Jekyll"
date: 2017-11-11 21:20:11
categories:
    - blog
    - astuce
tags:
    - Jekyll
    - pagination
    - liquid
    - astuce
---

Comme des millions de gens, j'avais utilisé Wordpress pendant des années pour publier mon blog et tant que j'avais du temps à lui consacrer, tout aller bien. Cependant dès que l'IRL me forçait à rester des déconnecter pendant plus d'une semaine, je commençais à flipper et à se demander si y avait pas une nouvelle faille a été découverte dans un plugin pendant mon absence, et que mon site s'est fait pown par un script kiddie, bien que j'avais automatisé pas mal de chose (dont les mises à jours) pour prévenir ça. D'ailleurs, c'est une des principales raisons qui m'ont poussé à abandonner mon ancien blog [crowd42.info \[0\]][0] dès que j'ai senti ça devenait ingérable avec l'emploi de temps de mon ancien boulot.

Puis il y a quelques mois j'ai découvert [Jekyll \[1\]][1], je ne vous dis pas combien j'ai regretté de ne pas l'avoir fait plus tôt. Après avoir passé deux heures à piocher sa documentation et quelques tutoriels en ligne et j'avais déjà un site/blog qui tourne parfaitement en locale sur ma machine. La suite vous l'avez sous les yeux :-), un blog statique, plus de soucis à se faire quant à sa sécurité, des performances bien supérieures Wordpress.

Quelques mois plus tard, quand le nombre d'articles affiché dans la partie blog du site devenait important. J'ai cherché dans la documentation officielle s'il était possible d'implémenter la pagination (je n'y avais pas pensé au départ quand j'ai mis en place le site), quelques étaient suffisantes pour trouver la solution. Tout ce que j'avais à faire c'est :
* Déplacer le fichier `blog.md` dans un répertoire `blog` que j'ai créé et de le renommer `index.html`;
* Modifier `blog/index.html` pour qu'il ressemble à ceci :

{% highlight jinja %}
{% raw %}
 {% for post in paginator.posts %}
  <li>
    <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
      ::
      <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
      @ {
      {% assign tag = post.tags | sort %}
      {% for category in tag %}<span><a href="{{ site.baseurl }}/category/#{{ category }}" class="reserved">{{ category }}</a>{% if forloop.last != true %},{% endif %}</span>{% endfor %}
      {% assign tag = nil %}
      }
  </li>
    {% endfor %}
!-- Pagination links -->
  {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path }}" class="previous">Page précédente</a>
  {% else %}
    <span class="previous">Page précédente</span>
  {% endif %}

  <span class="page_number ">Page: {{ paginator.page }} sur {{ paginator.total_pages }}</span>
  {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path }}" class="next">Page suivante</a>
  {% else %}
    <span class="next ">Page suivante</span>
    {% endif %}
    {% endraw %}
{% endhighlight %}

* Ajouter les deux lignes suivantes dans le fichier _config.yml

    ~~~
    paginate: 20
    paginate_path: "/blog/page:num/"
    ~~~

    * Pour que ça fonctionne en local, on doit ajouter le plugin jekyll-paginate dans notre fichier Gemfile et de lancer `bundle install`.

    ~~~
    gem 'jekyll-paginate'
    ~~~

Quelques explications le premier bloc du code ci-dessus (celui entre for post in paginator.post et endof) est une boucle for qui va afficher TOUT les articles de notre site, toute catégorie confondue (par exemple sur le mien : blog, movies, trucs et astuces, books...). C'est un des défauts de jekyll-paginotor, il ne permet pas d'exécuter une boucle sur certaines catégories seulement, par exemple `for post in site.catégories.blog`.

Le deuxième bloc quant à lui permet d'afficher une barre pour naviguer entre les pages:
    ~~~
    Page précédente Page: 1 sur 2 Page suivante
    ~~~

Et voila , facile non ? :-)

P.S : Il existe un plugin qui supporte la pagination sur les catégries, malheureusement il n'est pas supporté par Github, donc à moins que vous ne faites tourner jekyll sur votre serveur perso vous pouvez l'oublier.

### Liens
~~~
[0]: https://web.archive.org/web/*/www.crowd42.info
[1]: https://jekyllrb.com/
~~~
[0]: https://web.archive.org/web/*/www.crowd42.info
[1]: https://jekyllrb.com/
