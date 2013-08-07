---
layout: page
title: Welcome!
tagline: Simulation, Classic Music & Others
analytics: false
---
{% include JB/setup %}

## Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo;
        <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
    {{ post.content | split: '<!-- more -->' | first }}
    <a href="{{ post.url }}">Read more...</a><br><br>
  {% endfor %}
</ul>

{% include JB/comments %}
