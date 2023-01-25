---
title: Index
---
{% assign doclist = site.pages | sort: 'url'  %}
<h2>Contents</h2>
<ul>
  {% for doc in doclist %}
    {% if doc.name contains '.md' or doc.name contains '.html' %}
    <li><a class="index-link" href="{{ site.baseurl }}{{ doc.url }}">{{ doc.title | default: doc.url }}</a></li>
    {% endif %}
  {% endfor %}
</ul>
