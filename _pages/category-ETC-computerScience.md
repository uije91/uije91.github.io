---
title: "컴퓨터 공학"
layout: archive
permalink: categories/computerScience/
author_profile: true
sidebar_main: true
---

***

{% assign posts = site.categories.computerScience %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}