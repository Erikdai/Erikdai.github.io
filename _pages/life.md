---
layout: page
title: Life
title_zh: 生活
permalink: /life/
nav: true
nav_order: 5
description: Just a chill guy.
description_zh: 一个松弛的人。
---

<!-- Photo effects (this page only): a curtain reveal as each photo scrolls into view, then on hover a lift, an
     in-frame parallax that follows the cursor, a light sheen and the other photos dimming; click opens the photo
     (medium-zoom via zoomable=true). The reveal is skipped without JS or with prefers-reduced-motion.
     Two columns of 4:3 photos, plus one panorama spanning both columns (.life-wide) and two portraits spanning two
     rows (.life-tall); keep the cell count even so the last row stays full. -->
<script>
  if (!window.matchMedia("(prefers-reduced-motion: reduce)").matches) document.documentElement.classList.add("life-fx");
</script>

<style>
  .life-gallery { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1.1rem; }
  .life-gallery figure {
    --px: 0px;
    --py: 0px;
    --d: 0s;
    position: relative;
    margin: 0;
    overflow: hidden;
    aspect-ratio: 4 / 3; /* all photos are cropped to 4:3; reserves the space before the lazy image loads */
    border-radius: 12px;
    box-shadow: 0 6px 18px rgba(0, 0, 0, 0.12);
    cursor: zoom-in;
    transition: transform 0.5s cubic-bezier(0.2, 0.8, 0.2, 1), box-shadow 0.5s ease, opacity 0.45s ease, filter 0.45s ease;
  }
  .life-gallery .life-wide { grid-column: 1 / -1; }
  .life-gallery .life-wide figure { aspect-ratio: 8 / 3; } /* cropped to 8:3, about one row tall */
  .life-gallery .life-tall { grid-row: span 2; }
  .life-gallery .life-tall figure { aspect-ratio: auto; height: 100%; } /* cropped to 2:3, fills two rows */
  .life-gallery .life-tall picture { position: absolute; inset: 0; }
  @media (max-width: 575px) {
    .life-gallery { grid-template-columns: 1fr; }
    .life-gallery .life-tall { grid-row: auto; }
    .life-gallery .life-tall figure { aspect-ratio: 2 / 3; height: auto; }
  }
  .life-gallery picture, .life-gallery img { display: block; width: 100%; height: 100%; }
  .life-gallery img { object-fit: cover; }
  .life-gallery img {
    --s: 1;
    border-radius: 0 !important;
    box-shadow: none !important;
    transform: translate(var(--px), var(--py)) scale(var(--s));
    transition: transform 0.9s cubic-bezier(0.2, 0.8, 0.2, 1), filter 0.9s ease;
  }

  /* Curtain reveal: the frame opens from the middle while the photo settles from a blurred zoom */
  .life-fx .life-gallery figure:not(.is-in) { clip-path: inset(12% 12% 12% 12% round 12px); opacity: 0; }
  .life-fx .life-gallery figure:not(.is-in) img { --s: 1.18; filter: blur(8px); }
  .life-fx .life-gallery figure.is-in:not(.is-done) {
    clip-path: inset(0 0 0 0 round 12px);
    transition: clip-path 1.1s cubic-bezier(0.2, 0.8, 0.2, 1) var(--d), opacity 0.8s ease var(--d);
  }
  .life-fx .life-gallery figure.is-in:not(.is-done) img {
    transition: transform 1.4s cubic-bezier(0.2, 0.8, 0.2, 1) var(--d), filter 1s ease var(--d);
  }

  /* Light sheen that sweeps across once per hover */
  .life-gallery figure::after {
    content: "";
    position: absolute;
    inset: 0;
    z-index: 1;
    pointer-events: none;
    background: linear-gradient(115deg, transparent 35%, rgba(255, 255, 255, 0.28) 50%, transparent 65%);
    transform: translateX(-120%);
  }

  @media (hover: hover) and (pointer: fine) {
    .life-gallery figure.is-done:hover { transform: translateY(-6px); box-shadow: 0 22px 44px rgba(0, 0, 0, 0.22); }
    .life-gallery figure.is-done:hover img { --s: 1.07; transition: transform 0.3s ease-out; }
    .life-gallery figure.is-done:hover::after { transform: translateX(120%); transition: transform 1.1s cubic-bezier(0.2, 0.8, 0.2, 1); }
    .life-gallery:hover figure.is-done:not(:hover) { opacity: 0.55; filter: saturate(0.6); }
  }

  /* The opened photo sits above the fixed navbar (z-index 1030) */
  .medium-zoom-overlay, .medium-zoom-image--opened { z-index: 1040; }

  @media (prefers-reduced-motion: reduce) {
    .life-gallery figure, .life-gallery img, .life-gallery figure::after { transition: none !important; }
    .life-gallery figure::after { display: none; }
  }
</style>

<div class="life-gallery">
  {% include figure.liquid path="assets/img/life13.jpg" class="img-fluid rounded z-depth-1" alt="Palm trees on a small island" zoomable=true %}
  {% include figure.liquid path="assets/img/life5.jpg" class="img-fluid rounded z-depth-1" alt="Marina Bay Sands, Singapore" zoomable=true %}
  <div class="life-tall">{% include figure.liquid path="assets/img/life19.jpg" class="img-fluid rounded z-depth-1" alt="Airport aprons seen from the terminal" zoomable=true %}</div>
  {% include figure.liquid path="assets/img/life7.jpg" class="img-fluid rounded z-depth-1" alt="Ocean view from a sea cliff" zoomable=true %}
  {% include figure.liquid path="assets/img/life6.jpg" class="img-fluid rounded z-depth-1" alt="A woolly friend on a grassy hill" zoomable=true %}
  {% include figure.liquid path="assets/img/life9.jpg" class="img-fluid rounded z-depth-1" alt="ICML 2026 at COEX" zoomable=true %}
  {% include figure.liquid path="assets/img/life8.jpg" class="img-fluid rounded z-depth-1" alt="Sunset over the bush" zoomable=true %}
  {% include figure.liquid path="assets/img/life2.jpg" class="img-fluid rounded z-depth-1" alt="Beach at sunset" zoomable=true %}
  {% include figure.liquid path="assets/img/life18.jpg" class="img-fluid rounded z-depth-1" alt="A*STAR Advanced Remanufacturing and Technology Centre" zoomable=true %}
  <div class="life-wide">{% include figure.liquid path="assets/img/life10.jpg" class="img-fluid rounded z-depth-1" alt="Sydney Harbour Bridge lit up at night" zoomable=true %}</div>
  {% include figure.liquid path="assets/img/life14.jpg" class="img-fluid rounded z-depth-1" alt="Fiji Airways airliner at a hangar" zoomable=true %}
  {% include figure.liquid path="assets/img/life15.jpg" class="img-fluid rounded z-depth-1" alt="Inside a submarine" zoomable=true %}
  {% include figure.liquid path="assets/img/life17.jpg" class="img-fluid rounded z-depth-1" alt="Airliner cockpit" zoomable=true %}
  <div class="life-tall">{% include figure.liquid path="assets/img/life20.jpg" class="img-fluid rounded z-depth-1" alt="Chinese pavilion above the trees" zoomable=true %}</div>
  {% include figure.liquid path="assets/img/life4.jpg" class="img-fluid rounded z-depth-1" alt="Ocean pool at dusk" zoomable=true %}
  {% include figure.liquid path="assets/img/life16.jpg" class="img-fluid rounded z-depth-1" alt="Cathay Pacific airliner at the gate" zoomable=true %}
  {% include figure.liquid path="assets/img/life3.jpg" class="img-fluid rounded z-depth-1" alt="Coastal road through green hills" zoomable=true %}
  {% include figure.liquid path="assets/img/life21.jpg" class="img-fluid rounded z-depth-1" alt="Waves rolling into a beach town" zoomable=true %}
  {% include figure.liquid path="assets/img/life11.jpg" class="img-fluid rounded z-depth-1" alt="A classic sedan under palm trees" zoomable=true %}
  {% include figure.liquid path="assets/img/life1.jpg" class="img-fluid rounded z-depth-1" alt="Full moon over hillside houses at dusk" zoomable=true %}
  {% include figure.liquid path="assets/img/life12.jpg" class="img-fluid rounded z-depth-1" alt="Beach under a clear blue sky" zoomable=true %}
</div>

<script>
  (function () {
    var gallery = document.querySelector(".life-gallery");
    var figs = gallery.querySelectorAll("figure");
    function done(fig) {
      fig.classList.add("is-in", "is-done");
    }
    if (!document.documentElement.classList.contains("life-fx") || !("IntersectionObserver" in window)) {
      figs.forEach(done);
    } else {
      var io = new IntersectionObserver(
        function (entries) {
          entries.forEach(function (e) {
            if (!e.isIntersecting) return;
            var fig = e.target;
            io.unobserve(fig);
            // the right-hand photo of a row opens a beat later (read from layout, since the panorama shifts the order)
            var right = fig.getBoundingClientRect().left - gallery.getBoundingClientRect().left > 20;
            fig.style.setProperty("--d", (right ? 0.12 : 0) + "s");
            fig.classList.add("is-in");
            // hand over to the hover transitions once the reveal has played
            setTimeout(function () {
              fig.classList.add("is-done");
            }, 1600);
          });
        },
        { threshold: 0.15 }
      );
      figs.forEach(function (fig) {
        io.observe(fig);
      });
    }

    // In-frame parallax: the photo drifts against the cursor (mouse only)
    if (!window.matchMedia("(hover: hover) and (pointer: fine)").matches) return;
    if (window.matchMedia("(prefers-reduced-motion: reduce)").matches) return;
    figs.forEach(function (fig) {
      var img = fig.querySelector("img");
      if (!img) return;
      var raf = 0;
      fig.addEventListener("mousemove", function (e) {
        var r = fig.getBoundingClientRect();
        var dx = (e.clientX - r.left) / r.width - 0.5;
        var dy = (e.clientY - r.top) / r.height - 0.5;
        if (raf) return;
        raf = requestAnimationFrame(function () {
          raf = 0;
          img.style.setProperty("--px", (-dx * 18).toFixed(1) + "px");
          img.style.setProperty("--py", (-dy * 14).toFixed(1) + "px");
        });
      });
      fig.addEventListener("mouseleave", function () {
        img.style.setProperty("--px", "0px");
        img.style.setProperty("--py", "0px");
      });
    });
  })();
</script>
