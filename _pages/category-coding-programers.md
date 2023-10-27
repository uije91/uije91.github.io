---
title: "programers"
layout: archive
permalink: categories/programers/
author_profile: true
sidebar:
    nav: "docs"
---

{% assign posts = site.categories.programers %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}