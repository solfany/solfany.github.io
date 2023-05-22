---
layout: archive
title: "Blog Dev"
permalink: /Blog
author_profile: true
sidebar:                 
  nav: "sidebar-category" 
---


{% assign posts = site.categories.Blog %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
