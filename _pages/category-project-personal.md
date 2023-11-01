---
title: "Personal Project"
layout: archive
permalink: categories/personalProject/
author_profile: true
sidebar:
    nav: "docs"
---

{% assign posts = site.categories.personalProject %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}