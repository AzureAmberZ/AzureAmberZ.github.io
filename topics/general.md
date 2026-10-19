---
layout: page
title: "General Posts"
permalink: /topics/general/
---

# General Topics

All general posts below:

<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'general' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

Browse by general blog, research, and news updates categorized by section below:

---

## General Updates
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'general' and post.tags contains 'blog' %}
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
    {% if post.tags contains 'general' and post.tags contains 'research' %}
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
    {% if post.tags contains 'general' and post.tags contains 'news' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>