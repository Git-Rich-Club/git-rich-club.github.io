---
title: "DL"
layout: archive
permalink: categories/project/deep_learning
author_profile: true
types: posts
---

{% assign posts = site.categories['deep_learning']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}