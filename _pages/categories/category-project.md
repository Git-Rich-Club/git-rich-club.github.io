---
title: "Project"
layout: archive
permalink: categories/project
author_profile: true
types: posts
---

{% assign categories_to_show = "deep_learning,dagm2007" | split: "," %}

{% for cat in categories_to_show %}
  <h2>{{ cat | replace: "_", " " | capitalize }}</h2>
  {% assign posts = site.categories[cat] %}
  {% for post in posts %}
    {% include archive-single.html type=page.entries_layout %}
  {% endfor %}
{% endfor %}