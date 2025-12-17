---
layout: page
title: Projects
permalink: /projects/
---

Here is a collection of my work in Machine Learning and Data Science.

<ul>
  {% for project in site.projects %}
    <li>
      <h3><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h3>
      <p>{{ project.description }}</p>
    </li>
  {% endfor %}
</ul>
