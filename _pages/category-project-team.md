---
title: "Team Project"
layout: archive
permalink: categories/teamProject/
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.teamProject %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}