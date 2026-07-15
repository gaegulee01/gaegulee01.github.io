---
layout: page
permalink: /publications/
title: Publications
description: A list of my published academic research and peer-reviewed contributions.
nav: true
nav_order: 2
---

<div class="pub-filters">
  <button class="pub-filter-btn active" data-filter="all">All</button>
  <button class="pub-filter-btn" data-filter="llm">LLM</button>
  <button class="pub-filter-btn" data-filter="data-centric ai">Data-Centric AI</button>
  <button class="pub-filter-btn" data-filter="fairness">Fairness</button>
</div>

<div class="publications">

{% bibliography %}

</div>

<script>
document.addEventListener('DOMContentLoaded', function () {
  const buttons = document.querySelectorAll('.pub-filter-btn');
  const cards = document.querySelectorAll('.publication-card');

  buttons.forEach(function (btn) {
    btn.addEventListener('click', function () {
      buttons.forEach(function (b) { b.classList.remove('active'); });
      btn.classList.add('active');

      const filter = btn.getAttribute('data-filter');

      cards.forEach(function (card) {
        const cats = card.getAttribute('data-category') || '';
        card.style.display = (filter === 'all' || cats.includes(filter)) ? '' : 'none';
      });
    });
  });
});
</script>