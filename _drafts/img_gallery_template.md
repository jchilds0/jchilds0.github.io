---
title: Title
date: 2021-01-20 00:00
categories: [Photography, Australian International Airshow 2019]
tags: []     # TAG names should always be lowercase
math: true
comments: false
---

{% for index in (1..9) %}
  <img src="/assets/aia2019/{{page.title}}-{{forloop.index}}.jpg">
{% endfor %}
