---
layout: page
title: "Data Science Posts"
permalink: /topics/datascience/
---

## Posts tagged with "Data Science"

<ul>
  {% for post in site.posts %}
    {% if post.tags contains 'datascience' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> - <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>