---
layout: page
title: talks
permalink: /talks/
nav: true
nav_order: 4
toc:
    sidebar: left
---

<!-- _pages/talks.md -->
<div class="talks">

  <!-- Get talks and sort them by date -->
  {%- assign talks = site.talks | sort: 'date' | reverse -%}

  {% assign years = "" %}

  <!-- Extract unique years from the talks -->
  {%- for talk in talks -%}
    {% assign talk_year = talk.date | date: "%Y" %}
    {% unless years contains talk_year %}
      {% assign years = years | append: talk_year | append: ", " %}
    {% endunless %}
  {%- endfor -%}

  {% assign sorted_years = years | split: ", " | uniq | sort | reverse %}

  <!-- Display talks by year -->
  {% for year in sorted_years %}
    {% if year != "" %}
      <h2 class="talks"> {{ year }}</h2>

      <!-- Generate cards for each talk -->
      <div class="container">
      <div class="row row-cols-1">
      {%- for talk in talks -%}
        {% assign talk_year = talk.date | date: "%Y" %}
        {% if talk_year == year %}
          <!-- Include a card for each talk -->
          {% include talk.html %}
        {% endif %}
      {%- endfor %}
      </div>
      </div>
    {% endif %}
  {% endfor %}

</div>
