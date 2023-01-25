---
title: Index
---
{% assign doclist = site.pages | sort: 'url'  %}
<h2>About</h2>
My learnings from conferences, talks, work etc.

The general structure is that i try to summarize per conference, talk etc. a markdown file summarizing my learnings.

<h2>Documents</h2>
<ul>
  {% for doc in doclist %}
    {% if doc.name contains '.md' or doc.name contains '.html' %}
    <li><a class="index-link" href="{{ site.baseurl }}{{ doc.url }}">{{ doc.title | default: doc.url }}</a></li>
    {% endif %}
  {% endfor %}
</ul>
