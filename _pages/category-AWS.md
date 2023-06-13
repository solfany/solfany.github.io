---
layout: archive
title: "AWS"
permalink: /Aws
author_profile: true
sidebar:
  nav: "sidebar-category"
---

{% assign posts = site.categories.Aws %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
