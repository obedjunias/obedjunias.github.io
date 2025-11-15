---
layout: page
title: interests
permalink: /interests/
description: Beyond research - books, hobbies, photography, and more
nav: true
nav_order: 7
display_categories: [reading, hobbies, photography, travel]
horizontal: false
---

<!-- pages/interests.md -->
<div class="projects">
{% if page.display_categories %}
  <!-- Display categorized interests -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_interests = site.interests | where: "category", category %}
  {% assign sorted_interests = categorized_interests | sort: "importance" %}
  <!-- Generate cards for each interest -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for interest in sorted_interests %}
      {% include projects_horizontal.liquid project=interest %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for interest in sorted_interests %}
      {% assign project = interest %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display interests without categories -->

{% assign sorted_interests = site.interests | sort: "importance" %}

  <!-- Generate cards for each interest -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for interest in sorted_interests %}
      {% assign project = interest %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for interest in sorted_interests %}
      {% assign project = interest %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>
