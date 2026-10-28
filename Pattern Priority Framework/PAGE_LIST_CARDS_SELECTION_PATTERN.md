---
name: Page List Cards Selection Pattern
description: A single-column selectable list page with multi-select capabilities, dimmer overlay, and a contextual highlighted footer for batch actions.
label: page-list-cards-selection-ai
category: pattern
applies-to: single-column list pages requiring multi-select and batch operations on items displayed as cards
triggered-when: generating a page that lists selectable items with bulk action capabilities, checkboxes, dimmer effect, and a conditional footer
requires: eUI page components, eui-card, eui-chip, eui-dropdown, eui-paginator, eui-input-checkbox, EuiAppShellService, EuiGrowlService
outputs: a single-column page list following the cards-selection pattern
related-skills: PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN, PAGE_LIST_CARDS_SIMPLE_PATTERN, COLUMNS_LAYOUT_PATTERN
---

# EUI Page List Cards Selection Pattern — Canonical Structure Reference

## Purpose

This document describes the **Page List Cards Selection** design pattern — a single-column list page
with multi-select capabilities, a highlighted dimmer overlay, and a contextual footer for batch actions.

### What is this pattern?

A single-column results page containing:
- Page header following the **PAGE_HEADER_PATTERN** (Simple variant)
- A column header (title + result count + contextual actions)
- A **select all / unselect all toggle** with indeterminate state support
- A selectable cards list with per-card checkboxes
- A paginator footer
- A **conditional highlighted page footer** following the **PAGE_FOOTER_PATTERN** (Advanced variant with Bulk Actions)

Use this layout whenever a user needs to **select multiple items from a list and perform batch actions**.

---

## Related Patterns

This pattern composes two sub-patterns that must be retrieved from eUI skills:

| Sub-Pattern | File | Usage in this pattern |
|-------------|------|-----------------------|
| **PAGE_HEADER_PATTERN** | `PAGE_HEADER_PATTERN.md` | Simple variant — breadcrumb + title + subtitle + action buttons + overflow dropdown |
| **PAGE_FOOTER_PATTERN** | `PAGE_FOOTER_PATTERN.md` | Advanced variant (Bulk Actions) — conditional highlighted footer with selection counter and batch actions |

Refer to those files for the full canonical structure, zone descriptions, component hierarchy, and generation rules of the header and footer.

---

## Recommended Usage

Use this pattern when:
- Displaying a paginated list of items that users need to select for batch operations
- Per-item selection checkboxes and a "select all" toggle are required
- Visual feedback (dimmer overlay + highlighted cards) is needed when items are selected
- A contextual footer with bulk action buttons should appear on selection
- No filter sidebar or advanced search is required

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 1. PAGE HEADER (see PAGE_HEADER_PATTERN — Simple variant)         │  │
│  │    Breadcrumb + Title + Subtitle + Action buttons + Dropdown      │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ eui-page-content > eui-page-columns                               │  │
│  │  ┌───────────────────────────────────────────────────────────────┐│  │
│  │  │ 2. COLUMN HEADER LEFT        3. COLUMN HEADER RIGHT          ││  │
│  │  │    Title + result count       [Refresh] [Add item]            ││  │
│  │  ├───────────────────────────────────────────────────────────────┤│  │
│  │  │ 4. SELECT ALL TOGGLE  [euiHighlighted on column]             ││  │
│  │  │    [✓] Select all — N selected out of M                      ││  │
│  │  ├───────────────────────────────────────────────────────────────┤│  │
│  │  │ 5. COLUMN BODY  (selectable cards list)                      ││  │
│  │  │                                                              ││  │
│  │  │  ┌─────────────────────────────────────────────────────────┐ ││  │
│  │  │  │ eui-card [euiSelected] (×N iterable)                    │ ││  │
│  │  │  │   [✓] Title (link)    [Status chip] [Actions ▼]        │ ││  │
│  │  │  │       Subtitle                                         │ ││  │
│  │  │  └─────────────────────────────────────────────────────────┘ ││  │
│  │  │                                                              ││  │
│  │  ├───────────────────────────────────────────────────────────────┤│  │
│  │  │ 6. PAGINATOR                                                 ││  │
│  │  └───────────────────────────────────────────────────────────────┘│  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 7. PAGE FOOTER (see PAGE_FOOTER_PATTERN — Advanced variant)       │  │
│  │    @if selectedCount() > 0                                        │  │
│  │    [Reset] N selected   │   [Cancel] [Export] [More actions ▼]   │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Header | See **PAGE_HEADER_PATTERN** (Simple variant) | Yes | Breadcrumb, page title with `label` and `subLabel`, action items with buttons and overflow dropdown. |
| 2 | Column Header Left | `eui-page-column-header-left-content` | Yes | Column title and result count. |
| 3 | Column Header Right | `eui-page-column-header-right-content` | No | Contextual action buttons (secondary S + primary S). |
| 4 | Select All Toggle | `div` inside `eui-page-column-body` (before content list) | Yes | Checkbox (`euiInputCheckBox`) with `[indeterminate]` support and label showing "Select all" / "Unselect all" with selection count. |
| 5 | Column Body | `eui-page-column-body` | Yes | Selectable cards list with per-card checkboxes. |
| 6 | Paginator | `eui-page-column-footer` > `eui-paginator` | No | Pagination control bound to total item count. |
| 7 | Page Footer | See **PAGE_FOOTER_PATTERN** (Advanced variant) | Yes | Conditional footer (`@if selectedCount() > 0`) with `euiHighlighted`, left section (Reset + count), right section (Cancel + Primary + overflow dropdown). |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── [PAGE HEADER — See PAGE_HEADER_PATTERN Simple variant]
│   ├── eui-page-breadcrumb > eui-breadcrumb > eui-breadcrumb-item (×N)
│   ├── eui-page-header [label][subLabel]
│   │   └── eui-page-header-action-items
│   │       ├── button[euiButton][euiSecondary]
│   │       ├── button[euiButton][euiPrimary]
│   │       └── eui-dropdown (overflow actions)
├── eui-page-content
│   └── eui-page-columns [hasPreventMobileRendering]
│       └── eui-page-column [euiHighlighted]="(appShellService.state$ | async)?.isDimmerActive"
│           ├── eui-page-column-header-left-content
│           │   ├── div.eui-u-f-l → column title
│           │   └── div → "{{ items.length }} results found"
│           ├── eui-page-column-header-right-content
│           │   └── div.eui-u-flex
│           │       ├── button[euiButton][euiSecondary][euiSizeS]
│           │       └── button[euiButton][euiPrimary][euiSizeS]
│           ├── eui-page-column-body
│           │   ├── div.eui-u-flex.eui-u-mb-m.eui-u-ml-m  ← select all toggle
│           │   │   ├── input[euiInputCheckBox][checked][indeterminate]
│           │   │   └── label[euiLabel]  ← "Select all / Unselect all — N selected out of M"
│           │   └── @for (item of items; track item.id)
│           │       └── eui-card[euiSelected].eui-u-mb-m
│           │           └── eui-card-header
│           │               ├── eui-card-header-left-content
│           │               │   └── div.eui-u-flex.eui-u-flex-justify-content-center
│           │               │       └── input[euiInputCheckBox]
│           │               ├── eui-card-header-title
│           │               │   └── a.eui-u-text-link
│           │               ├── eui-card-header-subtitle
│           │               └── eui-card-header-right-content
│           │                   └── div.eui-u-flex.eui-u-flex-align-items-center.eui-u-flex-gap-s (click)="$event.stopPropagation()"
│           │                       ├── eui-chip [status directives]
│           │                       └── eui-dropdown (per-card actions)
│           └── eui-page-column-footer
│               └── eui-paginator [length]="items.length"
└── [PAGE FOOTER — See PAGE_FOOTER_PATTERN Advanced variant]
    └── @if (selectedCount() > 0)
        └── eui-page-footer [euiHighlighted]
            └── left/right flex layout with Reset, selection count, action buttons, overflow dropdown
```

---

## Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-home` | `eui-breadcrumb-item` | Breadcrumb home item (`iconSvgName`) |
| `eui-chevron-down` | `eui-icon-svg` / `span[euiIconSvg]` | Page-level overflow dropdown + card action dropdown trigger |
| `eui-ellipsis-vertical` | `eui-icon-svg` | Footer "More actions" overflow dropdown trigger |
| `eui-edit` | `eui-icon-svg` | Edit action in item dropdown |
| `eui-trash` | `eui-icon-svg` | Delete action in item dropdown |
| `eye:regular` | `eui-icon-svg` | View action in item dropdown |
| `eui-close` | `eui-icon-svg` | Cancel button icon in footer |
| `eui-download` | `eui-icon-svg` | Primary bulk action icon in footer |

---

## MCP Retrieval Strategy

All component APIs, inputs, outputs, and usage examples must be retrieved from the **eUI MCP Compodoc** tool before generating code. Do NOT rely on inline code samples.

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageHeaderComponent` | Page header: `label`, `subLabel` inputs |
| `get_component_docs` | `EuiPageBreadcrumbComponent` | Breadcrumb container |
| `get_component_docs` | `EuiBreadcrumbComponent` | Breadcrumb navigation |
| `get_component_docs` | `EuiBreadcrumbItemComponent` | Item inputs: `link`, `label`, `iconSvgName`, `ariaLabel` |
| `get_component_docs` | `EuiPageHeaderActionItemsComponent` | Action items container |
| `get_component_docs` | `EuiPageContentComponent` | Page content container |
| `get_component_docs` | `EuiPageColumnsComponent` | Columns layout with `hasPreventMobileRendering` |
| `get_component_docs` | `EuiPageColumnComponent` | Single column with `euiHighlighted` support |
| `get_component_docs` | `EuiCardComponent` | Card: `euiSelected`, card structure |
| `get_component_docs` | `EuiCardHeaderComponent` | Card header structure |
| `get_component_docs` | `EuiChipComponent` | Status chips: `euiSuccess`, `euiWarning`, `euiDanger`, `euiInfo` |
| `get_component_docs` | `EuiDropdownComponent` | Overflow dropdown menus |
| `get_component_docs` | `EuiPaginatorComponent` | Paginator: `length` input |
| `get_component_docs` | `EuiPageFooterComponent` | Footer with `euiHighlighted` support |
| `get_component_docs` | `EuiInputCheckboxComponent` | Checkbox: `checked`, `indeterminate` inputs |
| `get_component_docs` | `EuiGrowlService` | Toast notifications for action feedback |
| `get_component_docs` | `EuiTooltipDirective` | Tooltip on icon-only buttons |

---

## Required Angular Imports

Retrieve via MCP `get_component_docs` for each component. The following tokens must be spread in the component `imports` array:

- `AsyncPipe` from `@angular/common`
- `EUI_PAGE` from `@eui/components/eui-page`
- `EUI_BREADCRUMB` from `@eui/components/eui-breadcrumb`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EUI_CARD` from `@eui/components/eui-card`
- `EUI_CHIP` from `@eui/components/eui-chip`
- `EUI_DROPDOWN` from `@eui/components/eui-dropdown`
- `EUI_ICON` from `@eui/components/eui-icon`
- `EUI_INPUT_CHECKBOX` from `@eui/components/eui-input-checkbox`
- `EUI_LABEL` from `@eui/components/eui-label`
- `EUI_PAGINATOR` from `@eui/components/eui-paginator`
- `EuiTooltipDirective` from `@eui/components/directives`

Services (injected via `inject()`):
- `EuiAppShellService` from `@eui/core`
- `EuiGrowlService` from `@eui/core`

---

## Selection State Management (Signals-based)

The selection logic uses Angular signals for reactive state management. The implementation must include:

- A `signal<Set<number>>` holding the set of selected item IDs
- A `computed` for `selectedCount` derived from the signal's size
- A `computed` for `isAllSelected` comparing selection count to total items
- A `computed` for `isIndeterminate` (some but not all selected)
- An `effect()` to activate/deactivate the dimmer via `EuiAppShellService.isDimmerActive` based on `selectedCount() > 0`

### Required Selection Methods

| Method | Description |
|--------|-------------|
| `isCardSelected(id)` | Returns whether a specific item is selected |
| `toggleCardSelection(id)` | Toggles an individual item's selection state |
| `toggleSelectAll()` | Toggles all items selected/deselected |
| `clearSelection()` | Clears all selections (used by Reset/Cancel) |

---

## Status Chip Mapping

| Status Value | Directive | Visual |
|-------------|-----------|--------|
| Active | `[euiSuccess]` | Green chip |
| Under Review / Pending | `[euiWarning]` | Orange/amber chip |
| Expired / Rejected | `[euiDanger]` | Red chip |
| Draft / New | `[euiInfo]` | Blue chip |

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### Layout Rules

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: header (per PAGE_HEADER_PATTERN) → page-content (single column) → conditional footer (per PAGE_FOOTER_PATTERN).
3. **Use `eui-page-columns` with `hasPreventMobileRendering`** inside `eui-page-content`.
4. **Single `eui-page-column` with `[euiHighlighted]`** bound to `(appShellService.state$ | async)?.isDimmerActive` for dimmer overlay effect.
5. **Apply the PAGE_HEADER_PATTERN** (Simple variant) for breadcrumb, title, subtitle, and action items.
6. **Apply the PAGE_FOOTER_PATTERN** (Advanced variant) for the conditional highlighted footer with bulk actions.

### Selection Rules

7. **Include a "Select all" toggle** above the content list using `euiInputCheckBox` with `[indeterminate]` support and conditional label text ("Select all" / "Unselect all").
8. **Use Angular signals** (`signal`, `computed`, `effect`) for reactive selection state management.
9. **Activate the dimmer** via `EuiAppShellService.isDimmerActive` using an `effect()` bound to the `selectedCount()` signal.
10. **Inject `EuiAppShellService`** as a **public** property (required for template access to `state$`).
11. **Use `AsyncPipe`** for the `state$` observable binding in the template.

### Content Body Rules

12. **Use `eui-card` with `[euiSelected]`** bound to per-card selection state for each list item.
13. **Each card must have `eui-card-header-left-content`** containing a checkbox (`euiInputCheckBox`) for per-card selection.
14. **Use `@for` control flow** (Angular 17+), not `*ngFor`. Track by item `id`.
15. **Status chips** use conditional directives: `[euiSuccess]`, `[euiWarning]`, `[euiDanger]`, `[euiInfo]`.
16. **Per-card action dropdown** in `eui-card-header-right-content`, wrapped in a container with `(click)="$event.stopPropagation()"` to prevent card collapse toggling.
17. **Card title** is wrapped in `<a class="eui-u-text-link">` for navigation.

### Footer Rules

18. **Page footer is conditional** (`@if selectedCount() > 0`) with `euiHighlighted` directive.
19. **Footer uses left/right layout**: refer to PAGE_FOOTER_PATTERN Advanced variant for exact flex structure.
20. **Footer left section** contains: Reset button (`euiBasicButton`) + selection count text.
21. **Footer right section** contains: Cancel button (`euiSecondary` + `eui-close` icon) + Primary action button (`euiPrimary` + icon) + More actions overflow dropdown (`euiRounded euiIconButton euiBasicButton euiPrimary` + `eui-ellipsis-vertical` icon).

### Common Rules

22. **Use `eui-paginator`** in the column footer bound to the total items count.
23. **Button hierarchy**: primary uses `euiPrimary`, secondary uses `euiSecondary`. Buttons inside columns use `euiSizeS`.
24. **Spread EUI token arrays** in the component `imports`.
25. **Use `ChangeDetectionStrategy.OnPush`** on the component.
26. **Export `ModuleComponent`** alias for lazy loading via `loadComponent`.
27. **Accessibility**: all icon-only buttons must have `aria-label`. Breadcrumb home item must have `ariaLabel="Home"`. Per-card checkboxes must have `[attr.aria-label]` describing the item.
28. **Use `@if` for conditional rendering** (Angular 17+), not `*ngIf`.
29. **Retrieve all component documentation** from MCP tools (`get_component_docs`) before generating code to ensure correct API usage.
30. **Data is user-provided and agnostic** — define a simple interface with an `id` field and any domain-specific fields. The pattern does not prescribe a fixed data model.

---

## Key Differences from Other Patterns

| Aspect | Cards Selection (this) | Cards List Simple | Page List Anatomy (full) |
|--------|------------------------|-------------------|--------------------------|
| Filter column | Not present | Not present | Present (collapsible) |
| Card left content | Checkbox for selection | Not present | Not present |
| Select all toggle | Present (with indeterminate) | Not present | Not present |
| Column highlighting | `[euiHighlighted]` bound to dimmer | Not present | Not present |
| Card visual state | `[euiSelected]` per card | Not present | Not present |
| Page footer | Conditional + highlighted (PAGE_FOOTER_PATTERN Advanced) | Not present | Static (always visible) |
| Services | `EuiAppShellService` + `EuiGrowlService` | `EuiGrowlService` only | None |
| Selection state | Signals (`signal`, `computed`, `effect`) | None | None |
