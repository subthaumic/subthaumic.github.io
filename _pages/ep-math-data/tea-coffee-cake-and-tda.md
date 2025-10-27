---
layout: page
title: Tea, Coffee, Cake & TDA
permalink: /projects/ep-math-data/tea-coffee-cake-and-tda/
description: Talk series hosted by EP Mathematics and Data.
# toc:
#   sidebar: left
---

Tea, Coffee, Cake & TDA is a talk series organised by the EP Mathematics and Data to provide a platform to present current work in topological data analysis.  



<!-- _pages/events.md -->
<div class="talks">

  <!-- get CCTDA events and sort them by date-->
  {% assign events = site.events | where: "short_title", "CCTDA" | sort: "sort_date" %}
  {% assign years = "" %}

  <!-- Extract unique years from the events -->
  {%- for event in events -%}
    {% assign event_year = event.sort_date | default: event.date | date: "%Y" %}
    {% unless years contains event_year %}
      {% assign years = years | append: event_year | append: ", " %}
    {% endunless %}
  {%- endfor -%}

  {% assign sorted_years = years | split: ", " | uniq | sort | reverse %}

  <!-- Display events by year -->
  {% for year in sorted_years %}
    {% if year != "" %}
      <h2 class="talks" id="year-{{ year }}"> {{ year }}</h2>

      <!-- Generate cards for each event -->
      <div class="container">
      <div class="row row-cols-1">
      {%- for event in events -%}
        {% assign event_year = event.sort_date | default: event.date | date: "%Y" %}
        {% if event_year == year %}
          <!-- Include a card for each event -->
          {% include event.html %}
        {% endif %}
      {%- endfor %}
      </div>
      </div>
    {% endif %}
  {% endfor %}

</div>
