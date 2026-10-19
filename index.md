---
layout: default
title: Home
---

# Azure Amber Blog

Hello, everyone!
I am a PhD Student studying Statistics.

Welcome to my blog where I post material, tutorials, and updates on Statistics, Data Science, ML/AI, etc.

**[Learn more about me]({{ '/about/' | relative_url }})**



## Contents

Select a subject to view all related material:

| Topic | Description | Link |
| :--- | :--- | :--- |
| **General** | Non-Academic/Industry Material | [View Posts](/topics/general/) |
| **Statistics** | Classical Statistics Topics and Material | [View Posts](/topics/statistics/) |
| **Data Science** | Methods and Techniques in Data Science | [View Posts](/topics/datascience/) |
| **ML / AI** | Machine Learning and AI Topics | [View Posts](/topics/mlai/) |



## Recent Posts

<ul>
  {% for post in site.posts limit:10 %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a> 
      <small>({{ post.date | date: "%b %d, %Y" }})</small>
    </li>
  {% endfor %}
</ul>