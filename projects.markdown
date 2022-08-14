---
title: Projects
layout: page
---

# Projects

Some interesting projects I've worked on...

{% if customer.name == "kevin" %}
  {% for project in site.projects %}
    <h2>
      <a href="{{ project.url }}">
        {{ project.title }} - {{ project.description }}
      </a>
    </h2>
    <p>{{ project.content | markdownify }}</p>
  {% endfor %}
{% else %}
  <p>:construction: Under Construction :construction:</p>
{% endif %}
