---
layout: page
permalink: /publications/
title: publications
description: A list of my published academic research and peer-reviewed contributions.
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

{% include bib_search.liquid %}

<div class="pub-filter" role="tablist" aria-label="Filter publications by topic">
  <button type="button" class="pub-filter-btn is-active" data-filter="all">All</button>
  <button type="button" class="pub-filter-btn" data-filter="LLM">LLM</button>
  <button type="button" class="pub-filter-btn" data-filter="Data-Centric AI">Data-Centric AI</button>
  <button type="button" class="pub-filter-btn" data-filter="Fairness">Fairness</button>
</div>

<h2 class="pub-section-heading">Preprints &amp; Under Review</h2>

<div class="publications">

{% bibliography --query @*[status=preprint] %}

</div>

<h2 class="pub-section-heading">Publications</h2>

<div class="publications">

{% bibliography --query @*[status=published] %}

</div>

<script>
  (function () {
    const buttons = document.querySelectorAll('.pub-filter-btn');
    const entries = document.querySelectorAll('.publication-entry');
    const yearHeadings = document.querySelectorAll('.publications h2.year');

    function applyFilter(filter) {
      entries.forEach(function (el) {
        const cats = (el.getAttribute('data-categories') || '')
          .split(',')
          .map(function (s) { return s.trim(); })
          .filter(Boolean);
        const show = filter === 'all' || cats.indexOf(filter) !== -1;
        el.style.display = show ? '' : 'none';
      });

      yearHeadings.forEach(function (h) {
        let sib = h.nextElementSibling;
        let hasVisible = false;
        while (sib && !(sib.tagName === 'H2' && sib.classList.contains('year'))) {
          if (sib.classList && sib.classList.contains('publication-entry') && sib.style.display !== 'none') {
            hasVisible = true;
            break;
          }
          sib = sib.nextElementSibling;
        }
        h.style.display = hasVisible ? '' : 'none';
      });
    }

    buttons.forEach(function (btn) {
      btn.addEventListener('click', function () {
        buttons.forEach(function (b) { b.classList.remove('is-active'); });
        btn.classList.add('is-active');
        applyFilter(btn.getAttribute('data-filter'));
      });
    });
  })();
</script>
