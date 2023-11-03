---
title: "Backjoon"
layout: archive
permalink: categories/backjoon/
author_profile: true
sidebar_main: true
paginate: 5
paginate_path: /page:num/
---

{% assign posts = site.categories.backjoon %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}