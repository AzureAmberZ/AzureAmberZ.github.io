---
layout: page
title: "ML/AI Posts"
permalink: /topics/mlai/
---

# ML/AI Topics

All ML/AI posts below:

<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'mlai' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

Browse by academic topics, research, and news updates categorized by section below:

---

## Classical Machine Learning
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'mlai' and post.tags contains 'ml' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

---

## Deep Learning
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'mlai' and post.tags contains 'dl' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

---

## Computer Vision
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'mlai' and post.tags contains 'computervision' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

---

## Natural Language Processing
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'mlai' and post.tags contains 'nlp' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

---

## Explainable AI (xAI)
<ul>
  {% for post in site.posts limit:5 %}
    {% if post.tags contains 'mlai' and post.tags contains 'xai' %}
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
    {% if post.tags contains 'mlai' and post.tags contains 'research' %}
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
    {% if post.tags contains 'mlai' and post.tags contains 'news' %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — <span>{{ post.date | date: "%B %d, %Y" }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>