---
layout: default
title: Hangar
index_page: true
---
![Glider](/assets/images/hand_glider.jpg)
<sup><sup>
  Photo by [Andrey Larin](https://unsplash.com/@engine9)
  on [Unsplash](https://unsplash.com)
</sup></sup>

{% for post in site.posts %}
  <blog-date>{{ post.date | date_to_string }}</blog-date>
  <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {{ post.description }}

  {{ post.excerpt }}
{% endfor %}
