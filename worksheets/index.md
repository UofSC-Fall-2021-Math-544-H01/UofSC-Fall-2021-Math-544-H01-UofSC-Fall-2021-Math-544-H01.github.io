---
layout: page
title: Worksheets
nav_order: 3
description: Course worksheets
has_children: true
has_toc: false
---

# Worksheets 

{% assign worksheets = site.pages | where: "tag", "worksheet" | reverse %}
{% for worksheet in worksheets %}
 - [{{ worksheet.title }}]({{ worksheet.url }}). Class: {{ worksheet.date | date: "%B %-d" }}
{% endfor %}