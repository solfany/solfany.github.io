---

layout: archive
title: "Java"
permalink: /Java
author_profile: true
sidebar:                  
  nav: "sidebar-category" 
---


{% assign posts = site.categories.Java %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
