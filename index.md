---
layout: page
title: Kavi  
tagline: 永远一知半解
---
{% include JB/setup %}


<ul class="posts">
  {% for post in site.posts limit:80%}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


