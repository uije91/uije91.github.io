---
title: "개인 프로젝트"
layout: archive
permalink: categories/singleProject/
author_profile: true
sidebar_main: true
---

***

{% assign posts = site.categories.singleProject %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}