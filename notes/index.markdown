---
title:      notes
layout:     default
group:      notes
navigation: true
---

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
