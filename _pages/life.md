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
     (medium-zoom via zoomable=true). The reveal is skipped without JS or with prefers-reduced-motion. -->
<script>
  if (!window.matchMedia("(prefers-reduced-motion: reduce)").matches) document.documentElement.classList.add("life-fx");
</script>

<style>
  .life-gallery { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1.1rem; }
  @media (max-width: 575px) { .life-gallery { grid-template-columns: 1fr; } }
  .life-gallery figure {
    --px: 0px;
    --py: 0px;
    --d: 0s;
    position: relative;
    margin: 0;
    overflow: hidden;
    aspect-ratio: 4 / 3; /* all photos are 1600x1200; reserves the space before the lazy image loads */
    border-radius: 12px;
    box-shadow: 0 6px 18px rgba(0, 0, 0, 0.12);
    cursor: zoom-in;
    transition: transform 0.5s cubic-bezier(0.2, 0.8, 0.2, 1), box-shadow 0.5s ease, opacity 0.45s ease, filter 0.45s ease;
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

<!-- ===== Journey timeline: China, Malaysia, Australia, Singapore, South Korea, Fiji (in the user's order). The route
     is drawn by the script below from the stop positions (--x / --y), so it never stretches. When the section scrolls
     into view a plane flies the whole route and lights each stop as it passes; hovering, clicking or the arrow keys fly
     it to another stop and update the card underneath. Below 768px it becomes a vertical list. -->
<style>
  .journey { margin: 0.25rem 0 2.75rem; }
  .journey-head { display: flex; align-items: baseline; gap: 0.9rem; margin-bottom: 0.25rem; }
  .journey-eyebrow { font: 600 0.72rem/1 "Cascadia Mono", Consolas, ui-monospace, monospace; letter-spacing: 0.22em; color: var(--global-theme-color); }
  .journey-title { margin: 0; font-size: 1.6rem; font-weight: 300; }
  .journey-track { position: relative; height: 230px; }
  .journey-svg { position: absolute; inset: 0; width: 100%; height: 100%; overflow: visible; pointer-events: none; }
  .journey-svg .route-bg { fill: none; stroke: var(--global-divider-color); stroke-width: 2; stroke-dasharray: 2 8; stroke-linecap: round; }
  .journey-svg .route { fill: none; stroke: var(--global-theme-color); stroke-width: 2.5; stroke-linecap: round; stroke-dasharray: 1; stroke-dashoffset: 0; opacity: 0.85; }
  .journey-plane {
    position: absolute;
    left: 0;
    top: 0;
    z-index: 3;
    font-size: 1.15rem;
    color: var(--global-theme-color);
    pointer-events: none;
    filter: drop-shadow(0 3px 6px color-mix(in srgb, var(--global-theme-color) 45%, transparent));
    opacity: 0;
  }
  .journey.has-js .journey-plane { opacity: 1; }
  .journey-stops { list-style: none; margin: 0; padding: 0; }
  .journey-stop { position: absolute; left: var(--x); top: var(--y); z-index: 2; }
  .journey-stop button {
    position: relative;
    display: block;
    width: 0;
    height: 0;
    padding: 0;
    border: 0;
    background: none;
    color: inherit;
    cursor: pointer;
  }
  .journey-stop .jm {
    position: absolute;
    left: -9px;
    top: -9px;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background: var(--flag);
    border: 3px solid var(--global-bg-color);
    box-shadow: 0 0 0 1.5px var(--global-divider-color), 0 3px 8px rgba(0, 0, 0, 0.18);
    transition: transform 0.45s cubic-bezier(0.3, 1.5, 0.5, 1), box-shadow 0.35s ease;
  }
  .journey-stop .jl {
    position: absolute;
    left: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    white-space: nowrap;
    transform: translateX(-50%);
    transition: transform 0.35s ease, opacity 0.35s ease;
  }
  .journey-stop.down .jl { top: 18px; }
  .journey-stop.up .jl { bottom: 18px; flex-direction: column-reverse; }
  .journey-stop .ji { font: 600 0.68rem/1.2 "Cascadia Mono", Consolas, ui-monospace, monospace; letter-spacing: 0.12em; color: var(--global-text-color-light); }
  .journey-stop .jn { font-size: 0.98rem; font-weight: 400; line-height: 1.5; }
  .journey-stop .jh { display: none; }
  .journey-stop button:hover .jm,
  .journey-stop button:focus-visible .jm { transform: scale(1.3); }
  .journey-stop.is-active .jm {
    transform: scale(1.45);
    box-shadow: 0 0 0 1.5px var(--global-theme-color), 0 0 0 7px color-mix(in srgb, var(--global-theme-color) 16%, transparent), 0 4px 12px rgba(0, 0, 0, 0.2);
  }
  .journey-stop.is-active .jn { color: var(--global-theme-color); font-weight: 500; }
  .journey-stop.is-active.down .jl { transform: translate(-50%, 3px); }
  .journey-stop.is-active.up .jl { transform: translate(-50%, -3px); }
  /* Before the intro flight the stops wait, dimmed */
  .journey.is-pending .journey-stop:not(.is-reached) .jm { transform: scale(0.55); }
  .journey.is-pending .journey-stop:not(.is-reached) .jl { opacity: 0.3; }

  .journey-card {
    display: flex;
    align-items: center;
    gap: 1.4rem;
    margin-top: 0.75rem;
    padding: 1rem 1.25rem;
    border: 1px solid var(--global-divider-color);
    border-radius: 14px;
    background: color-mix(in srgb, var(--global-theme-color) 4%, transparent);
  }
  .journey-card .jc-idx { font: 200 2.6rem/1 "Roboto Slab", serif; color: var(--global-theme-color); min-width: 3.2rem; }
  .journey-card .jc-main { flex: 1 1 auto; min-width: 0; }
  .journey-card .jc-name { font-size: 1.35rem; font-weight: 500; line-height: 1.3; }
  .journey-card .jc-sub { font-size: 0.85rem; color: var(--global-text-color-light); }
  .journey-card .jc-hi { font: 300 1.7rem/1.2 "Roboto Slab", serif; color: var(--global-theme-color); white-space: nowrap; }
  .journey-card .jc-nav { display: flex; gap: 0.4rem; }
  .journey-card .jc-nav button {
    width: 2.1rem;
    height: 2.1rem;
    border-radius: 50%;
    border: 1px solid var(--global-divider-color);
    background: none;
    color: var(--global-text-color);
    cursor: pointer;
    transition: background-color 0.25s ease, border-color 0.25s ease, color 0.25s ease;
  }
  .journey-card .jc-nav button:hover {
    border-color: var(--global-theme-color);
    color: var(--global-theme-color);
    background: color-mix(in srgb, var(--global-theme-color) 10%, transparent);
  }
  .journey-card.jc-swap { animation: jc-in 0.45s cubic-bezier(0.2, 0.8, 0.2, 1); }
  @keyframes jc-in { from { opacity: 0.2; transform: translateY(6px); } to { opacity: 1; transform: none; } }
  .journey:not(.has-js) .journey-card { display: none; }

  @media (max-width: 767.98px) {
    .journey-track { height: auto; }
    .journey-svg, .journey-plane, .journey-card { display: none !important; }
    .journey-stops { position: relative; margin-left: 0.6rem; padding-left: 1.6rem; border-left: 2px dashed var(--global-divider-color); }
    .journey-stop { position: relative; left: auto; top: auto; margin: 0.9rem 0; }
    .journey-stop button { width: 100%; height: auto; text-align: left; }
    .journey-stop .jm { left: calc(-1.6rem - 10px); top: 50%; margin-top: -9px; }
    .journey-stop .jl,
    .journey-stop.up .jl,
    .journey-stop.down .jl { position: static; flex-direction: row; align-items: baseline; gap: 0.6rem; transform: none !important; opacity: 1 !important; }
    .journey-stop .jh { display: inline; margin-left: auto; font-family: "Roboto Slab", serif; color: var(--global-theme-color); }
    .journey.is-pending .journey-stop .jm { transform: none; }
  }
  @media (prefers-reduced-motion: reduce) {
    .journey *, .journey-card { transition: none !important; animation: none !important; }
  }
</style>

<section class="journey" aria-label="Journey">
  <div class="journey-head">
    <span class="journey-eyebrow">JOURNEY</span>
    <h2 class="journey-title"><span class="lang-en">Footprints</span><span class="lang-zh">足迹</span></h2>
  </div>
  <div class="journey-track">
    <svg class="journey-svg" aria-hidden="true"><path class="route-bg" d=""></path><path class="route" d="" pathLength="1"></path></svg>
    <i class="fa-solid fa-plane journey-plane" aria-hidden="true"></i>
    <ol class="journey-stops">
      <li class="journey-stop down" style="--x: 6%; --y: 66%;" data-hi="你好">
        <button type="button" aria-label="China">
          <span class="jm" style="--flag: conic-gradient(#de2910 0 70%, #ffde00 70% 100%);"></span>
          <span class="jl"><span class="ji">01</span><span class="jn"><span class="lang-en">China</span><span class="lang-zh">中国</span></span><span class="jh">你好</span></span>
        </button>
      </li>
      <li class="journey-stop up" style="--x: 23.6%; --y: 34%;" data-hi="Apa khabar">
        <button type="button" aria-label="Malaysia">
          <span class="jm" style="--flag: conic-gradient(#cc0001 0 25%, #ffffff 25% 50%, #010066 50% 75%, #ffcc00 75% 100%);"></span>
          <span class="jl"><span class="ji">02</span><span class="jn"><span class="lang-en">Malaysia</span><span class="lang-zh">马来西亚</span></span><span class="jh">Apa khabar</span></span>
        </button>
      </li>
      <li class="journey-stop down" style="--x: 41.2%; --y: 66%;" data-hi="G'day">
        <button type="button" aria-label="Australia">
          <span class="jm" style="--flag: conic-gradient(#00008b 0 50%, #ffffff 50% 70%, #e4002b 70% 100%);"></span>
          <span class="jl"><span class="ji">03</span><span class="jn"><span class="lang-en">Australia</span><span class="lang-zh">澳大利亚</span></span><span class="jh">G'day</span></span>
        </button>
      </li>
      <li class="journey-stop up" style="--x: 58.8%; --y: 34%;" data-hi="Selamat datang">
        <button type="button" aria-label="Singapore">
          <span class="jm" style="--flag: conic-gradient(#ef3340 0 50%, #ffffff 50% 100%);"></span>
          <span class="jl"><span class="ji">04</span><span class="jn"><span class="lang-en">Singapore</span><span class="lang-zh">新加坡</span></span><span class="jh">Selamat datang</span></span>
        </button>
      </li>
      <li class="journey-stop down" style="--x: 76.4%; --y: 66%;" data-hi="안녕하세요">
        <button type="button" aria-label="South Korea">
          <span class="jm" style="--flag: conic-gradient(#ffffff 0 40%, #cd2e3a 40% 60%, #0047a0 60% 80%, #111111 80% 100%);"></span>
          <span class="jl"><span class="ji">05</span><span class="jn"><span class="lang-en">South Korea</span><span class="lang-zh">韩国</span></span><span class="jh">안녕하세요</span></span>
        </button>
      </li>
      <li class="journey-stop up" style="--x: 94%; --y: 34%;" data-hi="Bula!">
        <button type="button" aria-label="Fiji">
          <span class="jm" style="--flag: conic-gradient(#68bfe5 0 50%, #002868 50% 75%, #ce1126 75% 100%);"></span>
          <span class="jl"><span class="ji">06</span><span class="jn"><span class="lang-en">Fiji</span><span class="lang-zh">斐济</span></span><span class="jh">Bula!</span></span>
        </button>
      </li>
    </ol>
  </div>
  <div class="journey-card" aria-live="polite">
    <div class="jc-idx">06</div>
    <div class="jc-main"><div class="jc-name"></div><div class="jc-sub"></div></div>
    <div class="jc-hi"></div>
    <div class="jc-nav">
      <button type="button" class="jc-prev" aria-label="Previous stop"><i class="fa-solid fa-chevron-left"></i></button>
      <button type="button" class="jc-next" aria-label="Next stop"><i class="fa-solid fa-chevron-right"></i></button>
    </div>
  </div>
</section>

<script>
  (function () {
    var root = document.querySelector(".journey");
    if (!root) return;
    var track = root.querySelector(".journey-track");
    var svg = root.querySelector(".journey-svg");
    var bg = svg.querySelector(".route-bg");
    var route = svg.querySelector(".route");
    var plane = root.querySelector(".journey-plane");
    var stops = Array.prototype.slice.call(root.querySelectorAll(".journey-stop"));
    var card = root.querySelector(".journey-card");
    var still = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
    var lens = [];
    var total = 0;
    var at = 0; // plane position along the route, in CSS px
    var active = stops.length - 1;
    var anim = 0;
    var facing = 1; // +1 flying along the route, -1 flying back
    root.classList.add("has-js");

    function points() {
      var W = track.clientWidth;
      var H = track.clientHeight;
      return stops.map(function (s) {
        var cs = getComputedStyle(s);
        return [(parseFloat(cs.getPropertyValue("--x")) / 100) * W, (parseFloat(cs.getPropertyValue("--y")) / 100) * H];
      });
    }

    // A smooth curve through the stops (Catmull-Rom written as cubic Beziers)
    function build() {
      var p = points();
      var d = "M" + p[0][0].toFixed(1) + " " + p[0][1].toFixed(1);
      for (var i = 0; i < p.length - 1; i++) {
        var a = p[i - 1] || p[i];
        var b = p[i];
        var c = p[i + 1];
        var e = p[i + 2] || c;
        d +=
          " C" + (b[0] + (c[0] - a[0]) / 6).toFixed(1) + " " + (b[1] + (c[1] - a[1]) / 6).toFixed(1) +
          " " + (c[0] - (e[0] - b[0]) / 6).toFixed(1) + " " + (c[1] - (e[1] - b[1]) / 6).toFixed(1) +
          " " + c[0].toFixed(1) + " " + c[1].toFixed(1);
      }
      svg.setAttribute("viewBox", "0 0 " + track.clientWidth + " " + track.clientHeight);
      bg.setAttribute("d", d);
      route.setAttribute("d", d);
      total = route.getTotalLength();
      lens = p.map(function (pt) {
        var lo = 0;
        var hi = total;
        for (var k = 0; k < 30; k++) {
          var mid = (lo + hi) / 2;
          if (route.getPointAtLength(mid).x < pt[0]) lo = mid;
          else hi = mid;
        }
        return (lo + hi) / 2;
      });
    }

    function placePlane(L) {
      at = Math.max(0, Math.min(total, L));
      var p = route.getPointAtLength(at);
      var q = route.getPointAtLength(Math.min(total, at + 1));
      var r = route.getPointAtLength(Math.max(0, at - 1));
      var ang = (Math.atan2(q.y - r.y, q.x - r.x) * 180) / Math.PI + (facing < 0 ? 180 : 0);
      plane.style.transform =
        "translate(" + p.x.toFixed(1) + "px," + p.y.toFixed(1) + "px) translate(-50%,-50%) rotate(" + ang.toFixed(1) + "deg)";
    }

    function show(i, swap) {
      active = i;
      stops.forEach(function (s, k) {
        s.classList.toggle("is-active", k === i);
      });
      var s = stops[i];
      var en = s.querySelector(".jn .lang-en").textContent;
      var zh = s.querySelector(".jn .lang-zh").textContent;
      var n = i + 1;
      var N = stops.length;
      card.querySelector(".jc-idx").textContent = (n < 10 ? "0" : "") + n;
      card.querySelector(".jc-name").innerHTML = '<span class="lang-en">' + en + '</span><span class="lang-zh">' + zh + "</span>";
      card.querySelector(".jc-sub").innerHTML =
        '<span class="lang-en">' + zh + " &middot; Stop " + n + " of " + N + "</span>" +
        '<span class="lang-zh">' + en + " &middot; 第 " + n + " 站，共 " + N + " 站</span>";
      card.querySelector(".jc-hi").textContent = s.getAttribute("data-hi");
      if (swap) {
        card.classList.remove("jc-swap");
        void card.offsetWidth; // restart the animation
        card.classList.add("jc-swap");
      }
    }

    function ease(t) {
      return t < 0.5 ? 4 * t * t * t : 1 - Math.pow(-2 * t + 2, 3) / 2;
    }

    function fly(to, ms, onStep, done) {
      cancelAnimationFrame(anim);
      var from = at;
      var t0 = performance.now();
      if (to !== from) facing = to > from ? 1 : -1;
      if (still || ms <= 0) {
        placePlane(to);
        if (onStep) onStep(1, to);
        if (done) done();
        return;
      }
      (function step(now) {
        var t = Math.min(1, (now - t0) / ms);
        var L = from + (to - from) * ease(t);
        placePlane(L);
        if (onStep) onStep(t, L);
        if (t < 1) anim = requestAnimationFrame(step);
        else if (done) done();
      })(t0);
    }

    // The plane parks just short of a stop on the side it arrives from, nose towards it, so it never hides the marker
    var PARK = 24;
    function park(i, dir) {
      var L = dir < 0 ? lens[i] + PARK : lens[i] - PARK;
      return Math.max(0, Math.min(total, L));
    }

    var intro = false;
    function go(i) {
      if (intro || i < 0 || i >= stops.length || i === active) return;
      var dir = lens[i] > at ? 1 : -1;
      var to = park(i, dir);
      show(i, true);
      fly(to, Math.min(1300, 450 + Math.abs(to - at) * 0.9));
    }

    build();
    placePlane(park(active, 1));
    show(active, false);

    var hover = window.matchMedia("(hover: hover) and (pointer: fine)").matches;
    stops.forEach(function (s, i) {
      var b = s.querySelector("button");
      b.addEventListener("click", function () {
        go(i);
      });
      if (hover)
        b.addEventListener("mouseenter", function () {
          go(i);
        });
    });
    card.querySelector(".jc-prev").addEventListener("click", function () {
      go(active - 1);
    });
    card.querySelector(".jc-next").addEventListener("click", function () {
      go(active + 1);
    });
    root.addEventListener("keydown", function (e) {
      if (e.key === "ArrowLeft") {
        go(active - 1);
        e.preventDefault();
      } else if (e.key === "ArrowRight") {
        go(active + 1);
        e.preventDefault();
      }
    });
    window.addEventListener("resize", function () {
      build();
      placePlane(park(active, facing));
    });

    // Intro flight: the route draws itself behind the plane and each stop lights up as the plane passes
    // (no intro on narrow screens: the route is hidden there and the stops show as a list)
    if (still || window.matchMedia("(max-width: 767.98px)").matches || !("IntersectionObserver" in window)) return;
    intro = true;
    root.classList.add("is-pending");
    route.style.strokeDashoffset = "1";
    placePlane(0);
    stops[0].classList.add("is-reached");
    show(0, false); // the card follows the plane during the intro
    var io = new IntersectionObserver(
      function (entries) {
        if (!entries[0].isIntersecting) return;
        io.disconnect();
        fly(
          park(stops.length - 1, 1),
          3200,
          function (t, L) {
            route.style.strokeDashoffset = String(1 - Math.min(total, L + PARK) / total);
            stops.forEach(function (s, k) {
              if (L >= lens[k] - PARK - 2 && !s.classList.contains("is-reached")) {
                s.classList.add("is-reached");
                show(k, true);
              }
            });
          },
          function () {
            intro = false;
            root.classList.remove("is-pending");
            route.style.strokeDashoffset = "0";
          }
        );
      },
      { threshold: 0.35 }
    );
    io.observe(root);
  })();
</script>

<div class="life-gallery">
  {% include figure.liquid path="assets/img/life1.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" zoomable=true %}
  {% include figure.liquid path="assets/img/life2.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" zoomable=true %}
  {% include figure.liquid path="assets/img/life3.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" zoomable=true %}
  {% include figure.liquid path="assets/img/life4.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" zoomable=true %}
  {% include figure.liquid path="assets/img/life5.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" zoomable=true %}
  {% include figure.liquid path="assets/img/life6.jpg" class="img-fluid rounded z-depth-1" alt="Everyday life" zoomable=true %}
</div>

<script>
  (function () {
    var figs = document.querySelectorAll(".life-gallery figure");
    var cols = window.matchMedia("(max-width: 575px)").matches ? 1 : 2;
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
            fig.style.setProperty("--d", (Array.prototype.indexOf.call(figs, fig) % cols) * 0.12 + "s");
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
