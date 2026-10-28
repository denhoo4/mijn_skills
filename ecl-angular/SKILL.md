---
name: ecl-angular
description: Guide for building public-facing European Commission websites using ECL (Europa Component Library) with Angular. Use when building sites on ec.europa.eu or europa.eu, following DG COMM guidelines, or using ECL components (ecl-button, ecl-card, ecl-menu, ecl-site-header, ecl-site-footer, etc.).
---

# ECL Angular

Guide for building public-facing European Commission websites with ECL (Europa Component Library).

## When to use ECL

Use ECL for **public-facing** sites on ec.europa.eu or europa.eu that must follow DG COMM guidelines.

For internal EC/EU apps and dashboards, use eUI instead.
For mobile apps, use eUI-Mobile (Ionic).

## Reference Guides

| Topic | Guide |
|-------|-------|
| Components | [ecl-components.md](ecl-components.md) |
| Styles | [ecl-styles.md](ecl-styles.md) |
| Version & purpose | [home.md](home.md) |

## Component Documentation

All ECL component docs are in `components/` — read the relevant file before using any component.

- `components/ecl-site-header.md` — site header structure
- `components/ecl-site-footer.md` — site footer structure
- `components/ecl-menu.md` — main navigation menu
- `components/ecl-page-header.md` — page header
- `components/ecl-button.md` — buttons
- `components/ecl-card.md` — cards
- `components/ecl-form-group.md` — form groups
- `components/ecl-text-input.md` — text inputs
- `components/ecl-select.md` — selects
- `components/ecl-checkbox.md` — checkboxes
- `components/ecl-table.md` — tables
- `components/ecl-tabs.md` — tabs
- `components/ecl-accordion.md` — accordions
- `components/ecl-modal.md` — modals
- `components/ecl-notification.md` — notifications
- `components/ecl-breadcrumb.md` — breadcrumbs
- `components/ecl-pagination.md` — pagination
- `components/index.md` — full component index

## Critical Rules

1. **Read the component file first** — never guess ECL component APIs.
2. **Use ECL utility classes** (`ecl-u-*`) for spacing, typography, and layout.
3. **Always import the ECL stylesheet** — see [ecl-styles.md](ecl-styles.md) for setup.
4. **Spread ECL token arrays** in component `imports` (e.g., `...ECL_BUTTON`, `...ECL_CARD`).
5. **Do not mix ECL and eUI components** on the same page.
