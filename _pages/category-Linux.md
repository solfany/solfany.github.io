---
layout: archive
title: "Linux"
permalink: /Linux
author_profile: true
sidebar:
  nav: "sidebar-category"
---

{% assign posts = site.categories.Linux %} {% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
