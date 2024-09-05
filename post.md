---
layout: single
title: "Posts"
permalink: /posts/
---

# Blog Posts

{% for post in site.posts %}
  - [{{ post.title }}]({{ post.url }})
{% endfor %}
