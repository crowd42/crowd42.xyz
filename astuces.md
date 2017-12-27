---
layout: blog
title: "Trucs & astuces"
permalink: /astuces/
---


<ul class="posts">
    {% for post in site.categories.astuce %}
        <li>
            <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
