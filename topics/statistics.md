---
layout: page
title: "Statistic Posts"
permalink: /topics/statistics/
---

# Statistic Topics

All statistics posts below:

<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'statistics' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

Browse by academic topics, research, and news updates categorized by section below:

---

## Statistical Theory
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'statistics' and post.tags contains 'theory' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

---

## Experimental Design
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'statistics' and post.tags contains 'design' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

---

## Statistical Modeling
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'statistics' and post.tags contains 'models' %}
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
    {% if post.tags contains 'statistics' and post.tags contains 'research' %}
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
    {% if post.tags contains 'statistics' and post.tags contains 'news' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>
