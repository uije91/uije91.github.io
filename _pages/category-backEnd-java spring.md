---
title: "spring"
layout: archive
permalink: categories/spring/
author_profile: true
sidebar:
    nav: "docs"
---

{% assign posts = site.categories.java %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}