---
layout: base
title: Home
---

{{ content }}

## Projects

<ul>
  {% for project in site.projects %}
    <li>
      <a href="{{ project.url }}">{{ project.title }}</a>
      <p>{{ project.description }}</p>
      <p><a href="{{ project.github_url }}">GitHub Repository</a></p>
    </li>
  {% endfor %}
</ul>
