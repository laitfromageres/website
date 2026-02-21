<!--
Sync Impact Report
===================
- Version change: 1.0.0 → 1.0.1 (address correction)
- Modified sections:
  - Technical Constraints > Page Sections: address corrected
    "10 Rue de la Mairie, Domont" → "53 Avenue Jean Jaures, 95330 Domont"
- Templates requiring updates: None
- Follow-up TODOs: None
-->

# Lait Fromageres Constitution

## Core Principles

### I. Design-First (NON-NEGOTIABLE)

The brand's visual identity MUST be respected in every element of the page.
All implementation decisions MUST defer to the design system defined in
the "Design System & Brand Identity" section below.

- Every component MUST use the approved color palette, typography, and
  spacing before any functionality is considered.
- Gold accent color (#D1B054) MUST be used exclusively for interactive
  elements (buttons, links, hover states) and decorative borders.
- No visual element may be added without verifying alignment with the
  premium, minimalist aesthetic.

**Rationale**: This is a brand showcase. Visual consistency directly
impacts perceived quality and trust for a premium fromagerie.

### II. Semantic HTML & Accessibility

All markup MUST use semantic HTML5 elements to ensure accessibility,
SEO, and maintainability.

- Use `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>` over
  generic `<div>` elements for page structure.
- All images MUST include descriptive `alt` attributes in French.
- Interactive elements MUST be keyboard-navigable.
- Color contrast MUST meet WCAG 2.1 AA standards (especially gold
  text on light backgrounds — verify contrast ratios).
- The page MUST include appropriate `lang="fr"` and meta tags.

**Rationale**: Accessibility is a legal requirement in France (RGAA)
and semantic markup improves search engine visibility for local SEO.

### III. Performance & Zero-Bloat

The page MUST load fast and contain no unnecessary dependencies.

- Tailwind CSS via CDN is the ONLY external CSS dependency allowed.
- Google Fonts (Playfair Display, Montserrat) is the ONLY external
  font dependency allowed.
- JavaScript MUST be minimal and vanilla — no frameworks, no jQuery.
- Total page weight MUST remain under 500KB (excluding images).
- Images MUST use modern formats (WebP with JPEG fallback) and be
  optimized for web delivery.
- No tracking scripts, analytics, or third-party widgets unless
  explicitly requested.

**Rationale**: Target audience includes local customers on mobile
networks. Fast load times directly impact conversion and local
search ranking.

### IV. Responsive & Mobile-First

The layout MUST be designed mobile-first and adapt gracefully to
all screen sizes.

- All Tailwind classes MUST follow mobile-first breakpoint strategy
  (base = mobile, `sm:`, `md:`, `lg:` for larger screens).
- Touch targets (buttons, links) MUST be at least 44x44px on mobile.
- The hero section MUST be impactful on both mobile and desktop.
- The location/hours section MUST be easily scannable on mobile
  (this is the most accessed info for local businesses).
- No horizontal scrolling on any viewport width >= 320px.

**Rationale**: Over 60% of local business web traffic comes from
mobile devices. The primary use case is a customer checking hours
or location on their phone.

### V. Premium Content Tone

All visible text MUST maintain a consistent premium, artisanal tone
that reflects the brand's positioning.

- Headings MUST be concise and evocative (no generic marketing speak).
- Body text MUST be informative yet refined — short paragraphs,
  deliberate word choices.
- French language MUST be grammatically impeccable with proper
  typographic conventions (espaces insecables, guillemets francais).
- Product descriptions MUST emphasize provenance, craftsmanship,
  and AOP/quality certifications.

**Rationale**: The landing page is the digital extension of the
boutique experience. Every word contributes to brand perception.

## Design System & Brand Identity

This section defines the mandatory visual language for all page elements.

### Typography

| Role | Font Family | Weight | Usage |
|------|-------------|--------|-------|
| Headings (h1-h3) | Playfair Display | 700 (Bold) | Section titles, hero text |
| Subtitles | Montserrat | 400 (Regular) | Tracking/letter-spacing: wide (0.1-0.2em) |
| Body text | Montserrat | 400 (Regular) | Paragraphs, descriptions |
| Buttons/CTA | Montserrat | 600 (Semi-bold) | Uppercase, letter-spacing: wider |

### Color Palette

| Token | Hex | Tailwind | Usage |
|-------|-----|----------|-------|
| Background | #F8F8F8 | `bg-[#F8F8F8]` | Main page background |
| Surface | #FFFFFF | `bg-white` | Card backgrounds, elevated surfaces |
| Text Primary | #333333 | `text-[#333333]` | Headings, body text |
| Text Secondary | #666666 | `text-[#666666]` | Captions, secondary info |
| Accent Gold | #D1B054 | `text-[#D1B054]` / `bg-[#D1B054]` | Buttons, borders, decorative elements |
| Accent Gold Hover | #C5A059 | `hover:bg-[#C5A059]` | Button hover states |
| Border Gold | #D1B054 | `border-[#D1B054]` | Fine decorative borders (1px) |

### Spacing & Layout

- Generous whitespace between sections (py-16 to py-24)
- Content max-width: `max-w-6xl` centered
- Card borders: 1px solid gold, no shadows or very subtle shadows
- Border radius: minimal (`rounded` or `rounded-sm`) for premium feel

## Technical Constraints

### Stack (Locked)

| Layer | Technology | Source |
|-------|------------|--------|
| Markup | HTML5 | Single `index.html` file |
| Styling | Tailwind CSS 3.x | CDN (`<script src="https://cdn.tailwindcss.com">`) |
| Fonts | Google Fonts | CDN (Playfair Display, Montserrat) |
| Scripting | Vanilla JS | Inline or single `<script>` block |
| Hosting | Static | No server-side processing required |

### File Structure

```text
/
├── index.html          # Single-page landing
├── assets/
│   └── images/         # Optimized images (WebP + fallback)
└── specs/              # Feature specifications (Specify workflow)
```

### Page Sections (Mandatory, in order)

1. **Hero** — Full-width, Playfair Display heading, gold CTA button
2. **Expertise** — AOP cheeses & fine epicerie showcase
3. **L'Art du Plateau** — Custom platter offerings (cards with gold borders)
4. **Infos & Localisation** — Address (53 Avenue Jean Jaures, 95330 Domont),
   opening hours, contact

## Governance

This constitution is the authoritative reference for all design and
implementation decisions on the Lait Fromageres landing page project.

- **Amendment process**: Any change to principles or design system
  MUST be documented with rationale and version-bumped accordingly.
- **Versioning**: Semantic versioning (MAJOR.MINOR.PATCH).
  - MAJOR: Principle removal or fundamental redesign.
  - MINOR: New principle or significant design system addition.
  - PATCH: Wording clarification or minor refinement.
- **Compliance**: Every implementation task MUST reference the
  relevant constitution principle(s) it satisfies.
- **Design system changes**: Any color, font, or spacing change
  MUST update both this constitution and all affected HTML/CSS.

**Version**: 1.0.1 | **Ratified**: 2026-02-21 | **Last Amended**: 2026-02-21
