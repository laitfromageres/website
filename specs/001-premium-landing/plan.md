# Implementation Plan: Landing Page Premium Lait Fromageres

**Branch**: `001-premium-landing` | **Date**: 2026-02-21 | **Spec**: [spec.md](./spec.md)
**Input**: Feature specification from `/specs/001-premium-landing/spec.md`

## Summary

Build a single-page premium landing page for the fromagerie/epicerie fine
"Lait Fromageres" in Domont. The page is a static HTML5 file styled with
Tailwind CSS (CDN) and Google Fonts, with minimal vanilla JavaScript for
the mobile hamburger menu and smooth scrolling. The page contains four
content sections (Hero, Expertise, Plateaux, Contact) plus a sticky
navigation header and a minimalist footer.

## Technical Context

**Language/Version**: HTML5, CSS3 (via Tailwind CSS 3.x CDN), ES6+ JavaScript
**Primary Dependencies**: Tailwind CSS (CDN), Google Fonts (Playfair Display, Montserrat)
**Storage**: N/A (static page, no server-side storage)
**Testing**: Manual browser testing (Chrome, Firefox, Safari, Edge) + Google Lighthouse audit
**Target Platform**: Modern web browsers (desktop + mobile), static hosting
**Project Type**: Static landing page (single HTML file)
**Performance Goals**: Lighthouse 90+ all categories, page load < 3s on 4G
**Constraints**: Total page weight < 500KB (excluding images), zero JS frameworks, only 2 CDN dependencies
**Scale/Scope**: Single page, 6 sections, ~300-400 lines of HTML

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| # | Principle | Status | Evidence |
|---|-----------|--------|----------|
| I | Design-First (NON-NEGOTIABLE) | PASS | Color palette (#D1B054, #C5A059, #F8F8F8, #333333), typography (Playfair Display, Montserrat), spacing rules all defined in constitution and spec. |
| II | Semantic HTML & Accessibility | PASS | FR-011 mandates semantic elements, FR-012 mandates keyboard accessibility and ARIA attributes, FR-003 requires ARIA on hamburger. |
| III | Performance & Zero-Bloat | PASS | FR-014 locks dependencies to Tailwind CDN + Google Fonts only. No JS frameworks. Page weight target < 500KB. |
| IV | Responsive & Mobile-First | PASS | FR-013 mandates 320px to 4K. FR-003 mandates hamburger menu. Mobile-first Tailwind breakpoint strategy. |
| V | Premium Content Tone | PASS | Spec defines exact French headlines, descriptions, and premium tone requirements for all sections. |

**GATE RESULT**: ALL PASS — proceed to implementation.

## Project Structure

### Documentation (this feature)

```text
specs/001-premium-landing/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── checklists/
│   └── requirements.md  # Spec quality checklist
└── tasks.md             # Phase 2 output (/speckit.tasks command)
```

### Source Code (repository root)

```text
/
├── index.html              # Single-page landing (all HTML + inline JS)
└── assets/
    └── images/
        └── hero-placeholder.jpg  # Hero background (placeholder until client provides)
```

**Structure Decision**: Minimal flat structure. Single `index.html` at root
with an `assets/images/` directory for optimized images. No build step,
no `src/` directory — the simplicity of a static HTML page does not
warrant deeper nesting. Tailwind config is inline via `<script>` tag.

## Implementation Phases

### Phase 1: Initialization & Base Structure

**Goal**: Deliver a valid HTML5 page with all dependencies loaded and
Tailwind custom config applied.

**Tasks**:
- Create `index.html` with HTML5 boilerplate (`<!DOCTYPE html>`,
  `<html lang="fr">`, meta viewport, charset UTF-8)
- Add Tailwind CSS CDN script tag
- Add Tailwind config script with custom colors:
  - `gold: { DEFAULT: '#D1B054', hover: '#C5A059' }`
  - Extended font families: `playfair: ['Playfair Display', 'serif']`,
    `montserrat: ['Montserrat', 'sans-serif']`
- Add Google Fonts `<link>` for Playfair Display (700) and
  Montserrat (400, 600) with `display=swap`
- Set page background to `bg-[#F8F8F8]` and default text to
  `text-[#333333]`
- Create empty `<header>`, `<main>` (with empty `<section>` stubs
  for each content block), and `<footer>` skeleton

**Validation**: Page opens in browser, fonts load, background color
is pearl grey, no console errors.

**Constitution Refs**: I (Design-First), II (Semantic HTML), III (Zero-Bloat)

---

### Phase 2: Header & Hero Section

**Goal**: Deliver the sticky navigation and hero with CTA.

**Tasks**:
- Build `<header>` with `<nav>`:
  - Logo "LF" text on the left (Playfair Display)
  - Nav links on the right: "La Boutique", "Nos Plateaux",
    "Acces & Contact" (hidden on mobile, visible on md+)
  - Hamburger button (hidden on md+, visible on mobile) with
    `aria-expanded="false"` and `aria-controls="mobile-menu"`
  - Sticky positioning: `sticky top-0 z-50` with
    `bg-white/90 backdrop-blur-sm`
- Build hero `<section id="accueil">`:
  - Full-width with min-height (min-h-[70vh] or min-h-screen)
  - Background: placeholder gradient or image with dark overlay
    (`bg-cover bg-center` + `bg-black/40` overlay div)
  - Centered content: h1 headline in Playfair Display 700,
    p subtitle in Montserrat with wide tracking,
    CTA button `<a href="#plateaux">` styled with gold bg
  - All text white on dark overlay

**Validation**: Sticky nav works on scroll. Hero fills viewport.
CTA button is gold. Mobile hamburger icon appears below 768px.
Keyboard tab navigates all links.

**Constitution Refs**: I (Design-First), II (Semantic/ARIA), IV (Mobile-First)

---

### Phase 3: Content Sections (Expertise & Plateaux)

**Goal**: Deliver the two content sections with responsive layouts.

**Tasks**:
- Build expertise `<section id="expertise">`:
  - Centered h2 title in Playfair Display
  - Two-column grid (`grid md:grid-cols-2 gap-12`) inside
    `max-w-6xl mx-auto`
  - Column 1: "La Fromagerie" — h3, paragraph about AOP/AOC,
    minimalist icon (Unicode or SVG inline)
  - Column 2: "L'Epicerie Fine" — h3, paragraph about curated
    products, small producers
  - Generous padding (`py-20 px-6`)
  - Stacks to 1 column on mobile automatically

- Build plateaux `<section id="plateaux">`:
  - Centered h2 "L'Art du Plateau" in Playfair Display
  - Subtitle in Montserrat wide-tracking
  - 2x2 grid (`grid md:grid-cols-2 gap-8`) of 4 cards
  - Each card: `bg-white border border-[#C5A059] rounded-sm p-8`
    - h3 card title (Playfair Display)
    - Short paragraph description (Montserrat)
  - Cards: "Aperitif entre amis", "Repas de fetes",
    "Mariages & Receptions", "Evenements d'entreprise"

**Validation**: Desktop shows 2 columns for both sections.
Mobile stacks to 1 column. Gold borders visible on platter cards.
Whitespace is generous. Text is in premium tone.

**Constitution Refs**: I (Design-First), IV (Mobile-First), V (Premium Tone)

---

### Phase 4: Contact, Hours & Footer

**Goal**: Deliver practical info section and footer.

**Tasks**:
- Build contact `<section id="contact">`:
  - Centered h2 in Playfair Display
  - Two-column layout (md:grid-cols-2):
    - Left: Address (with icon), phone (`<a href="tel:+33175412565">`),
      opening hours in a clean table or definition list
    - Right: Google Maps iframe embed or styled placeholder div
      with fallback text address
  - Hours data:
    - Lundi: Ferme
    - Mardi: 15h30 - 19h30
    - Mercredi-Samedi: 09h30 - 12h30, 15h30 - 19h30
    - Dimanche: 09h00 - 12h30
  - Stacks on mobile (info first, map below)

- Build `<footer>`:
  - Simple centered layout: logo reminder "LF - Lait Fromageres",
    copyright with dynamic year (JS `new Date().getFullYear()`),
    "Mentions legales" link (`href="#"`)
  - Subtle top border or darker background
  - Padding: `py-8`

**Validation**: Address, phone, hours are all visible and correct.
Phone link is clickable. Map embed loads (or placeholder is styled).
Footer shows current year. All elements stack on mobile.

**Constitution Refs**: II (Semantic HTML), IV (Mobile-First), V (Premium Tone)

---

### Phase 5: Interactivity (Vanilla JavaScript)

**Goal**: Add the two JS behaviors and final accessibility pass.

**Tasks**:
- Hamburger menu toggle:
  - `document.getElementById('menu-toggle')` click listener
  - Toggles `hidden` class on `#mobile-menu`
  - Updates `aria-expanded` attribute on button
  - Closes menu when a nav link is clicked (for smooth UX)

- Smooth scrolling:
  - `document.querySelectorAll('a[href^="#"]')` forEach
  - `e.preventDefault()` + `target.scrollIntoView({ behavior: 'smooth' })`
  - CSS fallback: `html { scroll-behavior: smooth; }` for
    browsers with JS disabled

- Accessibility final pass:
  - Verify all `alt` attributes on images
  - Verify focus indicators on all interactive elements
    (`focus:ring-2 focus:ring-[#D1B054]`)
  - Verify color contrast (gold on white may need adjustment —
    use gold only on dark backgrounds or as borders)
  - Test keyboard navigation through entire page
  - Verify `aria-expanded` toggles correctly

**Validation**: Hamburger opens/closes on mobile. Smooth scroll
works for all anchor links. Tab key navigates all interactive
elements. Lighthouse accessibility score >= 90.

**Constitution Refs**: II (Accessibility), III (Zero-Bloat JS), IV (Mobile-First)

## Complexity Tracking

> No constitution violations detected. All design choices align with
> the 5 core principles. The project is intentionally minimal.
