---
layout: page
title: publications
permalink: /publications/
nav: true
nav_order: 3
toc:
    sidebar: left
---

<!-- _pages/publications.md -->
<div class="publications">

{% bibliography -f {{ site.scholar.bibliography }} %}

<script>
  document.addEventListener("DOMContentLoaded", function() {
    document.querySelectorAll('.publications h2').forEach(function(heading) {
      var yearText = heading.textContent.trim();
      if (/^\d{4}$/.test(yearText)) {
        heading.id = 'year-' + yearText;
      }
    });
  });
</script>

</div>
