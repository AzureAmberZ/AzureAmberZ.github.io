---
layout: page
title: "General Posts"
permalink: /topics/general/
---

## Posts tagged with "General"

<ul>
  {% for post in site.posts %}
    {% if post.tags contains 'general' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> - <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>