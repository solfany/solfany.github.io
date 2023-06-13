---
layout: archive
title: "Software"
permalink: /Software
author_profile: true
sidebar:
  nav: "sidebar-category"
---

{% assign posts = site.categories.Software %} {% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
