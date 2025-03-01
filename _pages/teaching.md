---
layout: page
title: teaching
permalink: /teaching/
nav: true
nav_order: 5
toc:
    sidebar: left
---

<!-- _pages/teaching.md -->
<div class="teaching">

  {%- assign classes = site.teaching -%}

  {% assign terms = "" %}
  {% for class in classes %}
    {% unless terms contains class.term %}
      {% assign terms = terms | append: class.term | append: ", " %}
    {% endunless %}
  {% endfor %}

  {% assign unique_terms = terms | split: ", " | uniq %}
  {% assign years_and_terms = "" %}

  {% for term in unique_terms %}
    {% assign split_term = term | split: " " %}
    {% assign year = split_term[1] %}
    {% assign season = split_term[0] %}
    {% assign year_season = year | append: "-" %}
    {% if season == "Spring" %}
      {% assign year_season = year_season | append: "1" %}
    {% elsif season == "Summer" %}
      {% assign year_season = year_season | append: "2" %}
    {% elsif season == "Fall" %}
      {% assign year_season = year_season | append: "3" %}
    {% elsif season == "Winter" %}
      {% assign year_season = year_season | append: "4" %}
    {% endif %}
    {% assign years_and_terms = years_and_terms | append: year_season | append: "," | append: term | append: "|" %}
  {% endfor %}

  {% assign sorted_years_and_terms = years_and_terms | split: "|" | sort | reverse %}

  {% assign sorted_unique_terms = "" %}
  {% for year_and_term in sorted_years_and_terms %}
    {% if year_and_term != "" %}
      {% assign split_year_and_term = year_and_term | split: "," %}
      {% assign term = split_year_and_term[1] %}
      {% assign sorted_unique_terms = sorted_unique_terms | append: term | append: ", " %}
    {% endif %}
  {% endfor %}

  {% assign sorted_unique_terms = sorted_unique_terms | split: ", " | uniq %}

  <!-- Display classes by term -->
  {% for term in sorted_unique_terms %}
    <h2 class="teaching"> {{ term }}</h2>

    <!-- Generate cards for each class -->
    <div class="container">
    <div class="row row-cols-1">
    {%- for class in classes -%}
      {% if class.term == term %}
        {% include class.html %}
      {% endif %}
    {%- endfor %}
    </div>
    </div>
  {% endfor %}

</div>
