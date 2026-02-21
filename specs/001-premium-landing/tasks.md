# Tasks: Landing Page Premium Lait Fromageres

**Input**: Design documents from `/specs/001-premium-landing/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, quickstart.md

**Tests**: No test tasks included — not requested in the feature specification.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story. All tasks target a single `index.html` file (plus one assets directory), so parallelism within phases is limited.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3, US4)
- Include exact file paths in descriptions

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization — HTML5 boilerplate with all external dependencies loaded and Tailwind custom config applied.

- [x] T001 Create `index.html` with HTML5 boilerplate (`<!DOCTYPE html>`, `<html lang="fr">`, meta charset UTF-8, meta viewport, page title "Lait Fromageres — Fromagerie & Epicerie Fine a Domont") in `index.html`
- [x] T002 Add Tailwind CSS CDN `<script src="https://cdn.tailwindcss.com"></script>` and inline `tailwind.config` with custom colors (`gold: { DEFAULT: '#D1B054', hover: '#C5A059' }`), font families (`playfair: ['Playfair Display', 'serif']`, `montserrat: ['Montserrat', 'sans-serif']`) in `index.html`
- [x] T003 [P] Add Google Fonts `<link>` tags with preconnect to `fonts.googleapis.com` and `fonts.gstatic.com`, load Playfair Display (700) and Montserrat (400, 600) with `display=swap` in `index.html`
- [x] T004 [P] Create directory `assets/images/` for future image assets

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Semantic page skeleton that ALL user stories will build into. MUST be complete before any story content.

**CRITICAL**: No user story work can begin until this phase is complete.

- [x] T005 Create semantic page skeleton in `index.html`: `<header>` with empty `<nav>`, `<main>` containing four empty `<section>` elements with IDs (`id="accueil"`, `id="expertise"`, `id="plateaux"`, `id="contact"`), and an empty `<footer>`. Set `<body>` base classes: `bg-[#F8F8F8] text-[#333333] font-montserrat`

**Checkpoint**: Page opens in browser with pearl grey background, correct fonts loading, no console errors. Empty section structure is in place.

---

## Phase 3: User Story 1 — First Impression & Navigation (Priority: P1) MVP

**Goal**: A visitor lands on the page and immediately sees a premium brand identity via a hero section, can navigate with a sticky header, and sees a closing footer.

**Independent Test**: Open `index.html` in browser. Hero is visible with headline, subtitle, and gold CTA. Navigation is sticky on scroll. On mobile (< 768px), a hamburger icon appears. Footer shows copyright and legal links.

### Implementation for User Story 1

- [x] T006 [US1] Build sticky navigation `<header>` in `index.html`: `sticky top-0 z-50 bg-white/90 backdrop-blur-sm` containing `<nav>` with logo text "LF" (Playfair Display, left-aligned) and three anchor links on the right ("La Boutique" `href="#expertise"`, "Nos Plateaux" `href="#plateaux"`, "Acces & Contact" `href="#contact"`). Links hidden on mobile (`hidden md:flex`), styled in Montserrat with `hover:text-[#D1B054]` and `focus:ring-2 focus:ring-[#D1B054]` focus indicator
- [x] T007 [US1] Add hamburger menu button and mobile menu in `index.html`: button (`id="menu-toggle"`) visible only on mobile (`md:hidden`), with `aria-expanded="false"`, `aria-controls="mobile-menu"`, and SVG hamburger icon. Add hidden `<div id="mobile-menu" class="hidden md:hidden">` containing same three nav links stacked vertically with `py-2` padding and gold hover states
- [x] T008 [US1] Build hero `<section id="accueil">` in `index.html`: full-width (`min-h-[70vh]`) with CSS gradient placeholder background (`bg-gradient-to-br from-neutral-800 to-neutral-600`) and semi-transparent dark overlay. Centered content: `<h1>` "L'Excellence du Terroir, l'Art de l'Epicerie." in `font-playfair text-4xl md:text-6xl font-bold text-white`, `<p>` subtitle "Votre Fromagerie & Epicerie Fine a Domont." in `font-montserrat text-lg tracking-widest text-white/90`, and CTA `<a href="#plateaux">` "Commander un plateau" styled as gold button (`bg-[#D1B054] hover:bg-[#C5A059] text-white font-montserrat font-semibold uppercase tracking-wider px-8 py-4 rounded-sm`)
- [x] T009 [US1] Build `<footer>` in `index.html`: `bg-neutral-800 text-white/80 py-8` with centered layout containing logo reminder "LF — Lait Fromageres" in Playfair Display, copyright line with dynamic year via `<script>document.getElementById('year').textContent = new Date().getFullYear();</script>`, and "Mentions legales" link (`href="#"`) styled with gold hover

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently. Page has a sticky nav, impactful hero with CTA, and complete footer.

---

## Phase 4: User Story 2 — Find Practical Information (Priority: P2)

**Goal**: A visitor quickly finds the boutique address, phone number, opening hours, and location on a map.

**Independent Test**: Scroll to contact section. Address "53 Avenue Jean Jaures, 95330 Domont", phone "01 75 41 25 65" (clickable), and full weekly schedule are visible. Map embed or placeholder is displayed. Stacks on mobile.

### Implementation for User Story 2

- [x] T010 [US2] Build contact `<section id="contact">` layout in `index.html`: section with `py-20 px-6 bg-white`, centered `<h2>` "Informations Pratiques" in `font-playfair text-3xl md:text-4xl text-center mb-12`, and two-column responsive grid (`grid md:grid-cols-2 gap-12 max-w-6xl mx-auto`)
- [x] T011 [US2] Add business info in left column of contact section in `index.html`: address "53 Avenue Jean Jaures, 95330 Domont" with map-pin icon, phone `<a href="tel:+33175412565">01 75 41 25 65</a>` with phone icon, and opening hours in a clean `<dl>` or `<table>` layout (Lundi: Ferme, Mardi: 15h30–19h30, Mer-Sam: 09h30–12h30 & 15h30–19h30, Dimanche: 09h00–12h30). Use Montserrat, `text-[#333333]` for days and `text-[#666666]` for hours
- [x] T012 [US2] Add Google Maps iframe in right column of contact section in `index.html`: `<div class="aspect-video rounded-sm overflow-hidden border border-[#C5A059]">` containing `<iframe>` with `src` pointing to Google Maps embed for "53 Avenue Jean Jaures 95330 Domont", `loading="lazy"`, `title="Localisation Lait Fromageres"`, and `<noscript>` fallback with text address

**Checkpoint**: User Stories 1 AND 2 should both work independently. Visitor can navigate to contact, see all info.

---

## Phase 5: User Story 3 — Discover Expertise & Products (Priority: P3)

**Goal**: A visitor explores the fromagerie and epicerie fine expertise in a two-column layout.

**Independent Test**: Scroll to expertise section. Two columns on desktop (fromagerie left, epicerie right), stacked on mobile. Content highlights AOP/AOC, curated products, pairings. Generous whitespace.

### Implementation for User Story 3

- [x] T013 [US3] Build expertise `<section id="expertise">` layout in `index.html`: section with `py-20 px-6`, centered `<h2>` "L'Excellence & L'Expertise" in `font-playfair text-3xl md:text-4xl text-center`, decorative gold line separator (`w-16 h-0.5 bg-[#D1B054] mx-auto my-6`), and two-column grid (`grid md:grid-cols-2 gap-12 max-w-6xl mx-auto`)
- [x] T014 [US3] Add La Fromagerie column content in expertise section in `index.html`: `<article>` with `<h3>` "La Fromagerie" in Playfair Display, paragraph about AOP/AOC cheeses and exceptional aging emphasizing terroir excellence, and minimalist Unicode cheese icon or SVG. Text in Montserrat, `text-[#333333]`, premium artisanal tone
- [x] T015 [US3] Add L'Epicerie Fine column content in expertise section in `index.html`: `<article>` with `<h3>` "L'Epicerie Fine" in Playfair Display, paragraph about curated discoveries from small artisan producers and food & wine pairings, and minimalist Unicode/SVG icon. Same styling as fromagerie column

**Checkpoint**: All three completed stories are independently functional. Expertise section enriches the brand narrative.

---

## Phase 6: User Story 4 — Browse Custom Platter Offerings (Priority: P4)

**Goal**: A visitor discovers the four bespoke platter offerings through elegant cards with gold borders.

**Independent Test**: Scroll to plateaux section (or click hero CTA). Four cards in 2x2 grid on desktop, stacked on mobile. Each card has fine gold border, title, and description.

### Implementation for User Story 4

- [x] T016 [US4] Build plateaux `<section id="plateaux">` layout in `index.html`: section with `py-20 px-6 bg-white`, centered `<h2>` "L'Art du Plateau" in `font-playfair text-3xl md:text-4xl text-center`, subtitle "Creations sur mesure pour chaque occasion" in `font-montserrat tracking-widest text-[#666666] text-center`, decorative gold separator, and responsive grid container (`grid md:grid-cols-2 gap-8 max-w-5xl mx-auto`)
- [x] T017 [US4] Create 4 platter cards in plateaux grid in `index.html`: each card styled as `<article class="bg-white border border-[#C5A059] rounded-sm p-8 text-center">` with `<h3>` in Playfair Display and `<p>` description in Montserrat `text-[#666666]`. Cards: (1) "Aperitif entre amis" — curated cheeses and charcuterie for casual gatherings, (2) "Repas de fetes" — festive platters for holiday celebrations and family reunions, (3) "Mariages & Receptions" — bespoke creations tailored for your special day, (4) "Evenements d'entreprise" — professional catering for corporate events and seminars

**Checkpoint**: All four user stories are independently functional. CTA from hero correctly scrolls to this section.

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: JavaScript interactivity, accessibility audit, and responsive verification across all sections.

- [x] T018 Add hamburger menu toggle JavaScript at bottom of `<body>` in `index.html`: click listener on `#menu-toggle` that toggles `hidden` class on `#mobile-menu`, toggles `aria-expanded` attribute, and closes menu when any mobile nav link is clicked
- [x] T019 Add smooth scroll JavaScript at bottom of `<body>` in `index.html`: CSS baseline `html { scroll-behavior: smooth; }` in a `<style>` tag, plus JS `querySelectorAll('a[href^="#"]')` with `preventDefault()` and `scrollIntoView({ behavior: 'smooth' })` for enhanced control
- [x] T020 Accessibility pass on `index.html`: verify all images have French `alt` text, all interactive elements have visible focus indicators (`focus:ring-2 focus:ring-[#D1B054] focus:outline-none`), hamburger `aria-expanded` toggles correctly, color contrast meets WCAG AA for large text on gold backgrounds, `lang="fr"` present on `<html>`
- [x] T021 Responsive pass on `index.html`: test at 320px (no overflow, stacked layout, 44px touch targets), 768px (columns appear, hamburger hides), 1280px (full desktop layout), and 2560px (content centered, no stretch). Fix any horizontal scrolling issues
- [x] T022 Performance pass: verify page weight < 500KB (excluding images), ensure `font-display: swap` active via Google Fonts, confirm only 2 CDN dependencies, run Lighthouse audit targeting 90+ on all four categories

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion — BLOCKS all user stories
- **User Stories (Phase 3-6)**: All depend on Foundational phase completion
  - User stories can proceed sequentially in priority order (P1 → P2 → P3 → P4)
  - Parallel story execution is NOT practical here (single `index.html` file)
- **Polish (Phase 7)**: Depends on all user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) — No dependencies on other stories. Provides nav and footer used by all pages.
- **User Story 2 (P2)**: Can start after US1 (needs nav anchor targets to exist). Contact content is independent.
- **User Story 3 (P3)**: Can start after US1 (needs nav anchor targets). Expertise content is independent.
- **User Story 4 (P4)**: Can start after US1 (hero CTA links to `#plateaux`). Platter content is independent.

### Within Each User Story

- Section layout before section content
- Content structure before detailed text
- Story complete before moving to next priority

### Parallel Opportunities

Since all tasks target a single `index.html` file, true parallelism is limited to:

- **Phase 1**: T003 and T004 can run in parallel (fonts link vs directory creation)
- **Phase 3+**: Within a story, tasks are sequential (each builds on previous HTML structure)
- **Between stories**: Stories 2, 3, 4 are content-independent but edit the same file, so sequential execution avoids merge conflicts

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup (T001-T004)
2. Complete Phase 2: Foundational (T005)
3. Complete Phase 3: User Story 1 (T006-T009)
4. **STOP and VALIDATE**: Page loads, hero visible, nav works, footer shows
5. Deploy/demo if ready — minimal viable landing page

### Incremental Delivery

1. Complete Setup + Foundational → Structure ready
2. Add User Story 1 → Test independently → Demo (MVP with hero + nav + footer)
3. Add User Story 2 → Test independently → Demo (now has contact info)
4. Add User Story 3 → Test independently → Demo (now has expertise)
5. Add User Story 4 → Test independently → Demo (now has platters + CTA works)
6. Complete Polish → Final Lighthouse audit → Ship

### Recommended Approach

Sequential execution in priority order with validation at each checkpoint:
```
T001 → T002 → T003/T004 → T005 → T006 → T007 → T008 → T009 → [validate US1]
→ T010 → T011 → T012 → [validate US2]
→ T013 → T014 → T015 → [validate US3]
→ T016 → T017 → [validate US4]
→ T018 → T019 → T020 → T021 → T022 → [final validation]
```

---

## Notes

- All tasks target `index.html` (single-file project) — mark this in each task description
- [P] tasks = different files or truly independent operations
- [Story] label maps task to specific user story for traceability
- Each user story adds a new `<section>` block to the existing page skeleton
- The user requested step-by-step validation — pause at each checkpoint
- Commit after each completed phase for clean git history
