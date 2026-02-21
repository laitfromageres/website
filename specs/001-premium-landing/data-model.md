# Data Model: Landing Page Premium Lait Fromageres

**Branch**: `001-premium-landing` | **Date**: 2026-02-21

## Overview

This is a static landing page with no backend or database. The "data model"
describes the content entities rendered in HTML. All data is hardcoded in
the HTML markup.

---

## Entities

### Section

A top-level content block of the one-page layout.

| Attribute | Type | Description |
|-----------|------|-------------|
| id | string | Unique anchor ID for navigation (e.g., `accueil`, `expertise`, `plateaux`, `contact`) |
| title | string | Section heading displayed in Playfair Display |
| subtitle | string (optional) | Secondary text in Montserrat with wide tracking |
| content | mixed | Section-specific content (columns, cards, info blocks) |

**Instances** (in page order):

| id | title | Type |
|----|-------|------|
| `accueil` | "L'Excellence du Terroir, l'Art de l'Epicerie." | Hero (full-width, bg image, CTA) |
| `expertise` | "L'Excellence & L'Expertise" | Two-column (Fromagerie / Epicerie Fine) |
| `plateaux` | "L'Art du Plateau" | Card grid (4 platter cards) |
| `contact` | "Informations Pratiques" | Info + Map |

---

### Navigation Link

An anchor link in the sticky header.

| Attribute | Type | Description |
|-----------|------|-------------|
| label | string | Display text in the nav bar |
| href | string | Anchor target (`#expertise`, `#plateaux`, `#contact`) |

**Instances**:

| label | href |
|-------|------|
| "La Boutique" | `#expertise` |
| "Nos Plateaux" | `#plateaux` |
| "Acces & Contact" | `#contact` |

---

### Platter Card

A content card within the Plateaux section.

| Attribute | Type | Description |
|-----------|------|-------------|
| title | string | Card heading (Playfair Display) |
| description | string | Short elegant description (Montserrat) |
| border_color | hex | Gold border color (#C5A059) |

**Instances**:

| title | description |
|-------|-------------|
| "Aperitif entre amis" | Curated selection for casual gatherings |
| "Repas de fetes" | Festive platters for holiday celebrations |
| "Mariages & Receptions" | Bespoke creations for your special day |
| "Evenements d'entreprise" | Professional catering for corporate events |

---

### Business Info

The boutique's practical details displayed in the Contact section.

| Attribute | Type | Value |
|-----------|------|-------|
| name | string | "Lait Fromageres" |
| address | string | "53 Avenue Jean Jaures, 95330 Domont" |
| phone | string | "01 75 41 25 65" |
| phone_intl | string | "+33175412565" |
| map_query | string | "53+Avenue+Jean+Jaures+95330+Domont" |

---

### Opening Hours

Weekly schedule for the boutique.

| Day | Morning | Afternoon |
|-----|---------|-----------|
| Lundi | — | Ferme |
| Mardi | — | 15h30 - 19h30 |
| Mercredi | 09h30 - 12h30 | 15h30 - 19h30 |
| Jeudi | 09h30 - 12h30 | 15h30 - 19h30 |
| Vendredi | 09h30 - 12h30 | 15h30 - 19h30 |
| Samedi | 09h30 - 12h30 | 15h30 - 19h30 |
| Dimanche | 09h00 - 12h30 | — |

---

## Relationships

```text
Page
├── Header
│   ├── Logo ("LF")
│   └── Navigation Links [3]
├── Main
│   ├── Section: Hero (id=accueil)
│   │   └── CTA → links to #plateaux
│   ├── Section: Expertise (id=expertise)
│   │   ├── Column: Fromagerie
│   │   └── Column: Epicerie Fine
│   ├── Section: Plateaux (id=plateaux)
│   │   └── Platter Cards [4]
│   └── Section: Contact (id=contact)
│       ├── Business Info
│       ├── Opening Hours
│       └── Map Embed
└── Footer
    ├── Logo reminder
    ├── Copyright (dynamic year)
    └── Legal links
```
