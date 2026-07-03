---
layout: page
title: life
permalink: /life/
nav: true
nav_order: 6
description: just a chill guy
---

<style>
  .life-gallery { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1rem; }
  @media (max-width: 575px) { .life-gallery { grid-template-columns: 1fr; } }
  .life-gallery figure { margin: 0; }
  .life-gallery picture, .life-gallery img { display: block; width: 100%; height: auto; }
  .life-gallery img { border-radius: 8px; }
</style>

<div class="life-gallery">
  {% include figure.liquid path="assets/img/life1.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" %}
  {% include figure.liquid path="assets/img/life2.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" %}
  {% include figure.liquid path="assets/img/life3.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" %}
  {% include figure.liquid path="assets/img/life4.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" %}
  {% include figure.liquid path="assets/img/life5.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" %}
  {% include figure.liquid path="assets/img/life6.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" %}
</div>
