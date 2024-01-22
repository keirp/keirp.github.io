---
layout: page
permalink: /publications/
title: publications
description: A complete list of my publications.
# years: [2018, 2021, 2022, 2023]
years: [2024, 2023, 2022, 2021, 2018]
nav: true
nav_order: 1
---

<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}

  <h2 class="year">{{y}}</h2>
  {% bibliography -f {{ site.scholar.bibliography }} -q @*[year={{y}}]* %}
{% endfor %}

</div>
