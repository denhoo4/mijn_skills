---
name: Page List Cards Simple Pattern
description: A single-column paginated card list page without filter sidebar. Features page header with actions, a column header with title/count/contextual actions, an iterable cards content body with status chips and per-card action dropdowns, and a paginator footer.
label: page-list-cards-simple-ai
category: pattern
applies-to: single-column list pages displaying items as cards without a filter sidebar
triggered-when: generating a page that lists items in a single column with pagination, status indicators, and per-item actions
requires: eUI page components, eui-card, eui-chip, eui-dropdown, eui-paginator, EuiGrowlService
outputs: a single-column page list following the cards-list-simple pattern
related-skills: PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN, PAGE_LIST_PATTERN, SIMPLE_LAYOUT_PATTERN, COLUMNS_LAYOUT_PATTERN
---

# EUI Page List Cards Simple Pattern — Canonical Structure Reference

## Purpose

This document describes the **Page List Cards Simple** design pattern — a single-column list page
without a filter sidebar. The component is domain-agnostic; data models and content are provided by the user.

### What is this pattern?

A single-column results page containing:
- Page scaffolding (breadcrumb, header with actions) — follow the **PAGE_HEADER_PATTERN** (Simple variant)
- A column header (title + result count + contextual actions)
- A cards list body with status chips and per-card action dropdowns
- A paginator footer
- Optionally a page footer — follow the **PAGE_FOOTER_PATTERN** when footer actions are needed

Use this layout whenever a user needs to **display a list of items without search or filter sidebar**.

---

## Recommended Usage

Use this pattern when:
- Displaying a paginated list of items as cards
- No filter sidebar or advanced search is required
- Per-item actions (view, edit, delete) are needed
- Status indicators (chips) should be visible per item
- The page needs primary and contextual actions at both page and column level

---

## Related Patterns

| Pattern | When to Use |
|---------|-------------|
| **PAGE_HEADER_PATTERN** (Simple variant) | For the page breadcrumb, title, subtitle, and page-level action buttons. Always apply to the top section of this page. |
| **PAGE_FOOTER_PATTERN** (Simple or Advanced variant) | When the page requires footer actions (Save, Cancel) or bulk actions on selected items. |

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 1. PAGE BREADCRUMB  (eui-page-breadcrumb)                         │  │
│  │    [eui-home] Home > Section > Current page                       │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────┬────────────────────────────────────┐  │
│  │ 2. PAGE HEADER               │ 3. PAGE ACTIONS                    │  │
│  │    Page title                 │    [Secondary] [Primary]           │  │
│  │    Page subtitle              │    [Other actions ▼]               │  │
│  └──────────────────────────────┴────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ eui-page-content > eui-page-columns                               │  │
│  │  ┌───────────────────────────────────────────────────────────┐    │  │
│  │  │ 4. COLUMN HEADER LEFT        5. COLUMN HEADER RIGHT       │    │  │
│  │  │    Title + N results          [Action S] [Action S]        │    │  │
│  │  ├───────────────────────────────────────────────────────────┤    │  │
│  │  │ 6. COLUMN BODY  (cards list)                              │    │  │
│  │  │                                                           │    │  │
│  │  │  ┌─────────────────────────────────────────────────────┐  │    │  │
│  │  │  │ eui-card (×N iterable)                              │  │    │  │
│  │  │  │   Title (link)        [Status chip] [Actions ▼]     │  │    │  │
│  │  │  │   Subtitle — secondary info                         │  │    │  │
│  │  │  └─────────────────────────────────────────────────────┘  │    │  │
│  │  │                                                           │    │  │
│  │  ├───────────────────────────────────────────────────────────┤    │  │
│  │  │ 7. PAGINATOR                                              │    │  │
│  │  │    eui-paginator                                          │    │  │
│  │  └───────────────────────────────────────────────────────────┘    │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 8. PAGE FOOTER (optional — see PAGE_FOOTER_PATTERN)               │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item` | No | Navigation trail. See **PAGE_HEADER_PATTERN** for breadcrumb rules. |
| 2 | Page Header | `eui-page-header` [label, subLabel] | Yes | Page title and subtitle. See **PAGE_HEADER_PATTERN** (Simple variant). |
| 3 | Page Actions | `eui-page-header-action-items` | Yes | Secondary action, primary action, and optional overflow dropdown. See **PAGE_HEADER_PATTERN** for action items rules. |
| 4 | Column Header Left | `eui-page-column-header-left-content` | Yes | Title and result count. |
| 5 | Column Header Right | `eui-page-column-header-right-content` | Yes | Contextual action buttons (secondary S and primary S). |
| 6 | Column Body | `eui-page-column-body` | Yes | Iterable cards list with status chips and action dropdowns. |
| 7 | Paginator | `eui-page-column-footer` > `eui-paginator` | Yes | Pagination bound to total items length. |
| 8 | Page Footer | `eui-page-footer` | No | Optional footer actions. Follow **PAGE_FOOTER_PATTERN** when needed. |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── eui-page-breadcrumb                          ← See PAGE_HEADER_PATTERN
│   └── eui-breadcrumb
│       ├── eui-breadcrumb-item [link="/", iconSvgName="eui-home", ariaLabel="Home"]
│       ├── eui-breadcrumb-item [label="...", link="..."]
│       └── eui-breadcrumb-item [label="Current page"]
├── eui-page-header [label][subLabel]            ← See PAGE_HEADER_PATTERN (Simple variant)
│   └── eui-page-header-action-items
│       ├── button[euiButton][euiSecondary] → secondary action
│       ├── button[euiButton][euiPrimary] → primary action
│       └── eui-dropdown
│           ├── button[euiButton][euiPrimary][euiOutline][euiTooltip="More actions"] + eui-icon-svg[icon="eui-chevron-down"]
│           └── eui-dropdown-content
│               └── button[euiDropdownItem] (×N)
├── eui-page-content
│   └── eui-page-columns [hasPreventMobileRendering]
│       └── eui-page-column
│           ├── eui-page-column-header-left-content
│           │   ├── div.eui-u-f-l → column title
│           │   └── div → "{{ items.length }} results found"
│           ├── eui-page-column-header-right-content
│           │   └── div.eui-u-flex
│           │       ├── button[euiButton][euiSecondary][euiSizeS] → contextual action
│           │       └── button[euiButton][euiPrimary][euiSizeS] → contextual action
│           ├── eui-page-column-body
│           │   └── @for (item of items; track item.id)
│           │       └── eui-card.eui-u-mb-m
│           │           └── eui-card-header
│           │               ├── eui-card-header-title
│           │               │   └── a.eui-u-text-link → "{{ item.title }}"
│           │               ├── eui-card-header-subtitle → secondary info
│           │               └── eui-card-header-right-content
│           │                   ├── eui-chip [euiSuccess/euiWarning/euiDanger/euiInfo]
│           │                   └── eui-dropdown
│           │                       ├── button[euiBasicButton][euiPrimary][euiOutline][euiSizeS] + span[euiIconSvg]
│           │                       └── eui-dropdown-content
│           │                           ├── button[euiDropdownItem] → View (icon: eye:regular)
│           │                           ├── button[euiDropdownItem] → Edit (icon: eui-edit)
│           │                           └── button[euiDropdownItem] → Delete (icon: eui-trash)
│           └── eui-page-column-footer
│               └── eui-paginator [length]="items.length"
└── eui-page-footer (optional)                   ← See PAGE_FOOTER_PATTERN
```

---

## Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-home` | `eui-breadcrumb-item` | Breadcrumb home item (`iconSvgName`) |
| `eui-chevron-down` | `eui-icon-svg` / `span[euiIconSvg]` | Page-level overflow dropdown + card action dropdown trigger |
| `eye:regular` | `eui-icon-svg` | View action in card dropdown |
| `eui-edit` | `eui-icon-svg` | Edit action in card dropdown |
| `eui-trash` | `eui-icon-svg` | Delete action in card dropdown |

---

## MCP Retrieval Strategy

Before generating code for this pattern, retrieve component documentation from MCP tools:

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageHeaderComponent` | Page header inputs: `label`, `subLabel` |
| `get_component_docs` | `EuiPageBreadcrumbComponent` | Breadcrumb container, placement rules |
| `get_component_docs` | `EuiBreadcrumbComponent` | Breadcrumb navigation |
| `get_component_docs` | `EuiBreadcrumbItemComponent` | Item inputs: `link`, `label`, `iconSvgName`, `ariaLabel` |
| `get_component_docs` | `EuiPageHeaderActionItemsComponent` | Action items container |
| `get_component_docs` | `EuiPageColumnComponent` | Column structure: header, body, footer sections |
| `get_component_docs` | `EuiCardHeaderComponent` | Card header: title, subtitle, left/right content |
| `get_component_docs` | `EuiChipComponent` | Status chip: `euiSizeS`, `euiSuccess`, `euiWarning`, `euiDanger`, `euiInfo` |
| `get_component_docs` | `EuiDropdownComponent` | Dropdown for per-card actions and page-level overflow |
| `get_component_docs` | `EuiPaginatorComponent` | Paginator: `length`, `pageSize`, `pageChange` output |
| `get_component_docs` | `EuiPageFooterComponent` | Footer container with `euiHighlighted` support |
| `get_component_docs` | `EuiGrowlService` | Toast notifications for action feedback |

---

## Required Angular Imports

Retrieve via MCP `get_component_docs` for each component. The following tokens must be spread in the component `imports` array:

- `EUI_PAGE` from `@eui/components/eui-page`
- `EUI_BREADCRUMB` from `@eui/components/eui-breadcrumb`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EUI_ICON` from `@eui/components/eui-icon`
- `EUI_CARD` from `@eui/components/eui-card`
- `EUI_CHIP` from `@eui/components/eui-chip`
- `EUI_DROPDOWN` from `@eui/components/eui-dropdown`
- `EUI_PAGINATOR` from `@eui/components/eui-paginator`
- `EuiTooltipDirective` from `@eui/components/directives`
- `EuiGrowlService` from `@eui/core` (injected via `inject()`)

---

## Status Chip Mapping

Status chips use conditional directives on `eui-chip`. The user defines the status values and their mapping:

| Directive | Visual | Usage |
|-----------|--------|-------|
| `[euiSuccess]` | Green chip | Positive/active states |
| `[euiWarning]` | Orange/amber chip | Pending/review states |
| `[euiDanger]` | Red chip | Negative/expired states |
| `[euiInfo]` | Blue chip | Neutral/informational states |

Bind conditionally based on the item's status field, e.g. `[euiSuccess]="item.status === 'Active'"`.

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### Page Header Rules (delegate to PAGE_HEADER_PATTERN)

1. **Always use `eui-page` as the root element.**
2. **Apply the PAGE_HEADER_PATTERN (Simple variant)** for breadcrumb, title, subtitle, and page-level actions.
3. **Page header must use `label` and optionally `subLabel`** inputs on `eui-page-header`.
4. **Page actions go inside `eui-page-header-action-items`** with primary/secondary buttons and overflow `eui-dropdown`.

### Column Content Rules

5. **Use `eui-page-columns` with `hasPreventMobileRendering`** inside `eui-page-content`.
6. **Single `eui-page-column`** — no filter sidebar.
7. **Column header left** contains the title and result count.
8. **Column header right** contains contextual action buttons with `euiSizeS`.
9. **Use `eui-card`** for each list item with title link, subtitle, status chip, and action dropdown.
10. **Use `@for` control flow** (Angular 17+), not `*ngFor`. Track by item `id`.
11. **Status chips** use conditional directives: `[euiSuccess]`, `[euiWarning]`, `[euiDanger]`, `[euiInfo]`.
12. **Per-card action dropdown** uses `euiBasicButton euiPrimary euiOutline euiSizeS` with `eui-chevron-down` icon.
13. **Card title** is wrapped in `<a class="eui-u-text-link">` for navigation.
14. **Card subtitle** shows secondary descriptive information.
15. **Use `eui-paginator`** in the column footer bound to the total items length.

### Page Footer Rules (delegate to PAGE_FOOTER_PATTERN)

16. **When footer actions are needed**, apply the **PAGE_FOOTER_PATTERN** (Simple or Advanced variant depending on context).
17. **Place `eui-page-footer`** as a direct child of `eui-page`, after `eui-page-content`.

### Self-Containment Rules

18. **Define all data models inline** in the component file — no external imports to shared folders.
19. **Only import from `@angular/*` and `@eui/*`** packages.
20. **Data is user-defined** — the pattern is domain-agnostic. The user provides the interface and data.

### Common Rules

21. **Button hierarchy**: primary uses `euiPrimary`, secondary uses `euiSecondary`. Buttons inside columns use `euiSizeS`.
22. **Spread EUI token arrays** in the component `imports`.
23. **Use `ChangeDetectionStrategy.OnPush`** on the component.
24. **Export `ModuleComponent`** alias for lazy loading via `loadComponent`.
25. **Accessibility**: all action buttons must have `aria-label`. Breadcrumb home item must have `ariaLabel="Home"`.
26. **Retrieve component documentation** from MCP tools (`get_component_docs`) before generating code to ensure correct API usage.
27. **Use `inject()`** for service injection (e.g., `EuiGrowlService`).

---

## Key Differences from Other Patterns

| Aspect | Cards List Simple (this) | Page List Anatomy (full) | Columns Layout |
|--------|--------------------------|--------------------------|----------------|
| Filter column | Not present | Present (collapsible) | Present |
| Filter criteria chips | Not present | Present | Not present |
| Page footer | Optional (see PAGE_FOOTER_PATTERN) | Present | Optional |
| Column count | Single column | Two columns | Two+ columns |
| Content body | Cards list with chips | Fixed cards list | Fixed content |
| Search mechanism | None | Advanced search | Sidebar filters |
