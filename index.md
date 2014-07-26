---
layout: page
title: Welcome!
tagline: Simulation, Classic Music & Others
analytics: google
---
{% include JB/setup %}

{% for post in site.posts %}
  <h2><span>{{ post.date | date_to_string }}</span> &raquo;
  <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
  </h2>
{% endfor %}
