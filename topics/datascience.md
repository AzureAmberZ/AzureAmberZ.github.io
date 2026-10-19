---
layout: page
title: "Data Science Posts"
permalink: /topics/datascience/
---

# Data Science Topics

All data science posts below:

<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'datascience' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

Browse by academic topics, tutorials, research, and news updates categorized by section below:

---

## Academic Topics
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'datascience' and post.tags contains 'academic' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

---

## Tutorials
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'datascience' and post.tags contains 'tutorial' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

---

## Research Updates
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'datascience' and post.tags contains 'research' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

---

## News Updates
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'datascience' and post.tags contains 'news' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>