---
layout: home
title: Home
---

# Jonathan Boilard

Welcome to my Machine Learning & Data Science Portfolio.

## Projects

Here are some of the projects I've worked on:

<ul>
  {% for project in site.projects %}
    <li>
      <h3>
        <a href="{{ project.url | relative_url }}">{{ project.title }}</a>
      </h3>
      <p>{{ project.description }}</p>
    </li>
  {% endfor %}
</ul>
