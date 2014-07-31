---
title: notes
layout: default
---

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
