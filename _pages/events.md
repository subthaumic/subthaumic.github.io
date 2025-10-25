---
layout: page
title: events
permalink: /events/
nav: true
nav_order: 5
toc:
    sidebar: left
---

<!-- _pages/events.md -->
<div class="talks">

  <!-- Get events and sort them by date -->
  {%- assign events = site.events | sort: 'date' | reverse -%}

  {% assign years = "" %}

  <!-- Extract unique years from the events -->
  {%- for event in events -%}
    {% assign event_year = event.date | date: "%Y" %}
    {% unless years contains event_year %}
      {% assign years = years | append: event_year | append: ", " %}
    {% endunless %}
  {%- endfor -%}

  {% assign sorted_years = years | split: ", " | uniq | sort | reverse %}

  <!-- Display events by year -->
  {% for year in sorted_years %}
    {% if year != "" %}
      <h2 class="talks"> {{ year }}</h2>

      <!-- Generate cards for each event -->
      <div class="container">
      <div class="row row-cols-1">
      {%- for event in events -%}
        {% assign event_year = event.date | date: "%Y" %}
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
