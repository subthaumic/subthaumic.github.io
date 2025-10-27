---
layout: page
title: EP Math & Data Archive
permalink: /projects/ep-math-data/archive/
description: Preserved content from the former STRUCTURES wiki.
---

> This page preserves and curates material from the former STRUCTURES Wiki, captured in October 2025 after the wiki was decommissioned.

{% assign ep_pages = site.pages | where_exp: "p", "p.path contains '_pages/ep-math-data/'" | sort: "title" %}

<ul>
{%- for entry in ep_pages -%}
    {%- unless entry.url == page.url or entry.path contains 'heidelberg-tda-seminar' or entry.path contains 'tea-coffee-cake' -%}
      <li><a href="{{ entry.url | relative_url }}">{{ entry.title }}</a></li>
    {%- endunless -%}
  {%- endfor -%}
</ul>
