# Quickstart: Landing Page Premium Lait Fromageres

**Branch**: `001-premium-landing` | **Date**: 2026-02-21

## Prerequisites

- A modern web browser (Chrome, Firefox, Safari, or Edge)
- A text editor (VS Code recommended)
- No build tools, Node.js, or package manager required

## Getting Started

### 1. Clone and checkout

```bash
git clone <repository-url>
cd LT
git checkout 001-premium-landing
```

### 2. Open the page

Simply open `index.html` in your browser:

```bash
# On Windows
start index.html

# Or use VS Code Live Server extension for auto-reload
```

### 3. Project structure

```text
/
├── index.html              # The entire landing page
├── assets/
│   └── images/
│       └── hero-placeholder.jpg
└── specs/
    └── 001-premium-landing/
        ├── spec.md
        ├── plan.md
        ├── research.md
        ├── data-model.md
        └── quickstart.md    # This file
```

## Development Workflow

1. Edit `index.html` in your text editor
2. Refresh the browser to see changes (or use Live Server for auto-reload)
3. Use browser DevTools to test responsive breakpoints:
   - Mobile: 375px (iPhone SE)
   - Tablet: 768px (iPad)
   - Desktop: 1280px+
4. Check the browser console for any errors

## Key Technical Notes

- **Tailwind CSS**: Loaded via CDN, custom config is inline in a
  `<script>` tag — no build step needed
- **Google Fonts**: Loaded via `<link>` tags in `<head>`
- **JavaScript**: Minimal, inline at the bottom of `<body>` —
  only handles hamburger menu toggle and smooth scrolling
- **No dependencies to install**: Everything loads from CDNs

## Validation Checklist

After making changes, verify:

- [ ] Page renders correctly at 375px, 768px, and 1280px widths
- [ ] Navigation links scroll smoothly to their sections
- [ ] Hamburger menu opens/closes on mobile
- [ ] All text uses correct fonts (Playfair Display for headings,
      Montserrat for body)
- [ ] Gold accent color (#D1B054 / #C5A059) appears on buttons,
      borders, and hover states
- [ ] No horizontal scrollbar at any viewport width
- [ ] Run Lighthouse audit: target 90+ on all categories
