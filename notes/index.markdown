---
title:      notes
layout:     default
group:      notes
navigation: true
created:    28 Jun 2014
modified:   28 Jun 2014
---

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
