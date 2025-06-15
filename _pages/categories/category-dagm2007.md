---
title: "DAGM2007"
layout: archive
permalink: categories/project/dagm2007
author_profile: true
types: posts
---

{% assign posts = site.categories['dagm2007']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}