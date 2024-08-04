---
layout: page
title: Projects
permalink: /projects/
---


<ul>
  {% for project in site.projects %}
    <li>
      <a href="{{ project.project_url }}">{{ project.title }}</a>
      <p>{{ project.description }}</p>
      <p><a href="{{ project.github_url }}">GitHub Repository</a></p>
    </li>
  {% endfor %}
</ul>
