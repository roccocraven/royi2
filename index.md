---
layout: modern
title: "Royi2"
---

{% for post in site.posts %}
<article>
  <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
  <small>{{ post.date | date: "%B %d, %Y" }}</small>
  {% if post.description %}
  <p>{{ post.description }}</p>
  {% else %}
  <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
  {% endif %}
</article>
{% endfor %}
