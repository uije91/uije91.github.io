---
title: "Programers"
layout: archive
permalink: categories/programers/
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.programers %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}