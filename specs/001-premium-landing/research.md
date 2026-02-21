# Research: Landing Page Premium Lait Fromageres

**Branch**: `001-premium-landing` | **Date**: 2026-02-21

## Research Summary

This project is a static HTML landing page with well-defined requirements.
No technical unknowns were identified — the stack (HTML5, Tailwind CDN,
Google Fonts, vanilla JS) is fully specified in the constitution and the
feature spec contains no NEEDS CLARIFICATION markers.

The research below documents key decisions and best practices for the
chosen technologies.

---

## R1: Tailwind CSS via CDN — Configuration Approach

**Decision**: Use the Tailwind CSS CDN play script with inline
`tailwind.config` for custom colors and fonts.

**Rationale**: The CDN play version (`cdn.tailwindcss.com`) supports
runtime configuration via a `<script>` tag with `tailwind.config`,
enabling custom colors (#D1B054, #C5A059) and font families without
a build step. This matches the Zero-Bloat principle.

**Implementation**:
```html
<script src="https://cdn.tailwindcss.com"></script>
<script>
  tailwind.config = {
    theme: {
      extend: {
        colors: {
          gold: { DEFAULT: '#D1B054', hover: '#C5A059' }
        },
        fontFamily: {
          playfair: ['Playfair Display', 'serif'],
          montserrat: ['Montserrat', 'sans-serif']
        }
      }
    }
  }
</script>
```

**Alternatives considered**:
- Tailwind CLI build: Rejected — requires Node.js, adds build step
  complexity for a single static page.
- Plain CSS: Rejected — Tailwind utilities dramatically accelerate
  responsive layout development.

---

## R2: Google Fonts Loading Strategy

**Decision**: Use `<link>` preconnect + stylesheet approach with
`display=swap` for optimal loading.

**Rationale**: Preconnecting to `fonts.googleapis.com` and
`fonts.gstatic.com` reduces DNS/TLS overhead. The `display=swap`
parameter ensures text remains visible during font loading (FOUT
over FOIT), matching the Performance principle.

**Implementation**:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">
```

**Alternatives considered**:
- Self-hosted fonts: Rejected — adds file management overhead,
  Google Fonts CDN has excellent global caching.
- `@import` in CSS: Rejected — slower than `<link>` due to
  render-blocking behavior.

---

## R3: Color Contrast Compliance

**Decision**: Use gold (#D1B054) primarily for borders, buttons
(with white text), and decorative elements. Avoid gold text on
light backgrounds.

**Rationale**: Gold #D1B054 on white (#FFFFFF) has a contrast ratio
of approximately 2.6:1, which fails WCAG AA (requires 4.5:1 for
normal text). Gold on dark backgrounds (e.g., dark overlay in hero)
passes. For buttons, white text on gold background (#D1B054) has
~2.6:1 — to pass AA, use white text on the darker gold hover color
or ensure button text is large (>= 18px bold, which requires only
3:1 ratio).

**Implementation approach**:
- Gold borders on white cards: decorative, no contrast issue
- Gold CTA button: use large bold text (>= 18px) to meet 3:1 AA
  for large text, or darken gold slightly for button background
- Never use gold for small body text on light backgrounds
- Focus indicators: gold ring on focused elements is decorative
  enough at 2px width

**Alternatives considered**:
- Darker gold (#8B7532): Better contrast but deviates from brand
  identity — rejected per Design-First principle.

---

## R4: Smooth Scroll & Hamburger JS

**Decision**: CSS `scroll-behavior: smooth` as baseline + JS
`scrollIntoView` for enhanced control + simple toggle for hamburger.

**Rationale**: CSS smooth scrolling provides graceful degradation
when JS is disabled. The JS layer adds `preventDefault()` to avoid
URL hash changes and provides consistent behavior across browsers.
The hamburger toggle is ~15 lines of vanilla JS.

**Implementation approach**:
```css
html { scroll-behavior: smooth; }
```
```javascript
// Smooth scroll with offset for sticky header
document.querySelectorAll('a[href^="#"]').forEach(link => {
  link.addEventListener('click', e => {
    e.preventDefault();
    const target = document.querySelector(link.getAttribute('href'));
    if (target) target.scrollIntoView({ behavior: 'smooth' });
  });
});

// Hamburger toggle
const toggle = document.getElementById('menu-toggle');
const menu = document.getElementById('mobile-menu');
toggle.addEventListener('click', () => {
  const expanded = toggle.getAttribute('aria-expanded') === 'true';
  toggle.setAttribute('aria-expanded', !expanded);
  menu.classList.toggle('hidden');
});
```

**Alternatives considered**:
- JS scroll libraries (e.g., smooth-scroll): Rejected — violates
  Zero-Bloat principle for a trivial feature.
- CSS-only hamburger (checkbox hack): Rejected — less accessible,
  harder to manage ARIA state.

---

## R5: Google Maps Embed

**Decision**: Use a standard Google Maps `<iframe>` embed with the
boutique address, wrapped in a styled container with fallback text.

**Rationale**: Google Maps embeds are free (no API key required for
simple iframe embed), load asynchronously, and provide immediate
value to visitors. A noscript/fallback ensures the address is
always visible even if the iframe is blocked.

**Implementation approach**:
```html
<div class="aspect-video rounded-sm overflow-hidden border border-[#C5A059]">
  <iframe
    src="https://www.google.com/maps/embed?pb=!1m18!..."
    width="100%" height="100%"
    style="border:0;" allowfullscreen="" loading="lazy"
    referrerpolicy="no-referrer-when-downgrade"
    title="Localisation Lait Fromageres - 53 Avenue Jean Jaures, Domont">
  </iframe>
</div>
<noscript>
  <p>53 Avenue Jean Jaures, 95330 Domont</p>
</noscript>
```

**Alternatives considered**:
- Google Maps JavaScript API: Rejected — requires API key, adds
  complexity, violates Zero-Bloat.
- Static map image: Acceptable fallback but less useful than
  interactive embed.
- OpenStreetMap embed: Viable alternative if Google is not desired.
