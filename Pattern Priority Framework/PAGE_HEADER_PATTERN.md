---
name: Page Header Pattern — Canonical Structure Reference
description: Describes the Page Header design pattern with two variants (Simple and Advanced) used in eUI-based applications. Covers layout rules, component hierarchy, required imports, and accessibility guidelines.
label: page-header-pattern
category: pattern
applies-to: page header with title, breadcrumb, actions, metadata, and collapsible body
triggered-when: generating a page that requires a header with title, subtitle, breadcrumb, action buttons, or rich metadata (category, status, tags)
requires: EUI page components, eui-breadcrumb, eui-button, eui-icon, eui-dropdown, eui-card, eui-chip, eui-chip-list, eui-icon-toggle
outputs: a page header following the Simple or Advanced page header pattern
related-skills: SIMPLE_LAYOUT_PATTERN, FLUID_LAYOUT_PATTERN, PAGE_FOOTER_PATTERN, PAGE_LIST_PATTERN
---

# EUI Page Header Pattern — Canonical Structure Reference

## Purpose

This document describes the **Page Header** design pattern — the structured title area at the top of pages in all EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

### What is this pattern?

The Page Header pattern provides a consistent location for page identity, navigation context, and page-level actions. It has **two variants**:

1. **Simple Page Header** — A minimal header with breadcrumb, title, subtitle (via `subLabel` input), and up to two direct action buttons. No collapsible behavior, no metadata, no tags, no overflow dropdown.
2. **Advanced Page Header** — A feature-rich, collapsible header with breadcrumb, title, sub-label area (category badge, status chip, description, tags), action items (buttons, overflow dropdown, favorite toggle), and a collapsible body section with summary content.

---

## Recommended Usage

### Simple Header

Use when:

- A page needs only a title, subtitle, and up to two action buttons
- No collapsible behavior is required
- No structured metadata (category, status, tags) needs to be displayed
- The page context is straightforward (list pages, simple forms, landing pages)

### Advanced Header

Use when:

- The page displays detailed entity information (case detail, document overview, profile)
- Structured metadata is needed: category badge, status chip, tags
- More than two actions are required (overflow dropdown)
- A favorite/bookmark toggle is needed
- A collapsible summary body section is appropriate
- The header needs expand/collapse behavior to save vertical space

---

## Visual Anatomy

### Simple Header

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 1. PAGE BREADCRUMB  (eui-page-breadcrumb)                         │  │
│  │    [eui-home] Home > Section > Current page                       │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────┬────────────────────────────────────┐  │
│  │ 2. PAGE HEADER TITLE         │ 3. PAGE HEADER ACTIONS             │  │
│  │    Page Title - Lorem ipsum  │    [Secondary action] [Primary]    │  │
│  │                              │                                    │  │
│  │ 4. PAGE HEADER SUBTITLE      │                                    │  │
│  │    Page Sub-title - Lorem... │                                    │  │
│  └──────────────────────────────┴────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

### Advanced Header

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                           │
│  ┌───────────────────────────────────────────────────────────────────────────────┐ │
│  │ 1. BREADCRUMB                                                                 │ │
│  │    eui-home > Section > Current page                                          │ │
│  └───────────────────────────────────────────────────────────────────────────────┘ │
│  ┌───────────────────────────────────────────────────┬───────────────────────────┐ │
│  │ 2. PAGE TITLE (isCollapsible)                     │ 4. ACTION ITEMS           │ │
│  │    "Page Title - Lorem ipsum..."                  │  [Secondary] [Primary]    │ │
│  │                                                   │  [eui-ellipsis-vertical]  │ │
│  │                                                   │  [eui-star toggle]        │ │
│  ├───────────────────────────────────────────────────┤                           │ │
│  │ 3. SUB-LABEL                                      │                           │ │
│  │  ┌──────────┐ ┌────────┐                          │                           │ │
│  │  │ CATEGORY │ │ STATUS │  Description text...     │                           │ │
│  │  └──────────┘ └────────┘                          │                           │ │
│  │                                                   │                           │ │
│  │  tag:regular [Tag01] [Tag02] [Tag03] [>] [Manage] │                           │ │
│  └───────────────────────────────────────────────────┴───────────────────────────┘ │
│  ┌───────────────────────────────────────────────────────────────────────────────┐ │
│  │ 5. HEADER BODY (collapsible)                                                  │ │
│  │  ┌─────────────────────────────────────────────────────────────────────────┐  │ │
│  │  │ eui-card — Summary content...                                           │  │ │
│  │  └─────────────────────────────────────────────────────────────────────────┘  │ │
│  └───────────────────────────────────────────────────────────────────────────────┘ │
└────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

### Simple Header Zones

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item` | No | Navigation trail. First item uses `iconSvgName="eui-home"` with `ariaLabel="Home"`. Last item has no `link` (current page). |
| 2 | Page Header Title | `eui-page-header` with `label` | Yes | Main page title via the `label` input. No `isCollapsible` — the title is always visible. |
| 3 | Page Header Actions | `eui-page-header-action-items` | No | Right-aligned action area. Contains only direct buttons (secondary and/or primary). No overflow dropdown, no icon toggle. |
| 4 | Page Header Subtitle | `eui-page-header` with `subLabel` | No | Subtitle text via the `subLabel` input directly on `eui-page-header`. Plain text only. |

### Advanced Header Zones

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item` | No | Navigation trail. First item uses `iconSvgName="eui-home"` with `ariaLabel="Home"`. Last item has no `link` (current page). |
| 2 | Page Header Title | `eui-page-header` with `label`, `isCollapsible`, `expandedLabel`, `collapsedLabel` | Yes | Collapsible page title. `[isCollapsed]="false"` sets initial state to expanded. |
| 3 | Sub-Label | `eui-page-header-sub-label` with `class="eui-u-flex-gap-2xs"` | No | Contains two rows: subtitle row (category + status + text) and metadata/tags row. |
| 3a | Category | `div` with `eui-u-c-bg-secondary-surface eui-u-ph-s eui-u-pv-4xs` | No | Category badge as a styled div — NOT an `eui-chip`. |
| 3b | Status Chip | `eui-chip` with `euiSizeS` and status directive | No | Status indicator. Uses `euiInfo`, `euiSuccess`, `euiWarning`, or `euiDanger`. |
| 3c | Description | Free text inside the first row div | No | Description text after category and status. |
| 3d | Tags | `eui-icon-svg` + `eui-chip-list` + `eui-chip-list-additional-content` | No | Tag icon (`tag:regular`) followed by chip list with expand/collapse and optional "Manage" button. |
| 4 | Action Items | `eui-page-header-action-items` | No | Secondary/primary buttons, overflow dropdown (`eui-ellipsis-vertical`), and favorite toggle (`eui-icon-toggle` with `eui-star`). |
| 5 | Header Body | `eui-page-header-body` | No | Collapsible content area with `eui-card` > `eui-card-content` for summary information. |

---

## Icons Reference

All EUI icon values used across both variants:

| Context | EUI Icon Value | Component | Usage |
|---------|---------------|-----------|-------|
| Breadcrumb home | `eui-home` | `eui-breadcrumb-item` | `iconSvgName="eui-home"` — both variants |
| Tag icon | `tag:regular` | `eui-icon-svg` | `icon="tag:regular"` — advanced only, before the chip list |
| Tag expand | `eui-chevron-right` | `eui-icon-svg` | `icon="eui-chevron-right"` — expand tags button |
| Tag collapse | `eui-chevron-left` | `eui-icon-svg` | `icon="eui-chevron-left"` — collapse tags button |
| Overflow menu trigger | `eui-ellipsis-vertical` | `eui-icon-svg` | `icon="eui-ellipsis-vertical"` — more actions button |
| Dropdown item prefix | `eui-chevron-right` | `eui-icon-svg` | `icon="eui-chevron-right"` with `size="s"` — before each dropdown item label |
| Favorite toggle | `eui-star` | `eui-icon-toggle` | `iconSvgNameOn="eui-star"` and `iconSvgNameOff="eui-star"` |

---

## Component Hierarchy (DOM nesting order)

### Simple Header

```
eui-page
├── eui-page-breadcrumb
│   └── eui-breadcrumb
│       └── eui-breadcrumb-item (×N)
├── eui-page-header [label, subLabel]
│   └── eui-page-header-action-items
│       ├── button[euiButton][euiSecondary]
│       └── button[euiButton][euiPrimary]
```

### Advanced Header

```
eui-page
├── eui-page-breadcrumb
│   └── eui-breadcrumb
│       └── eui-breadcrumb-item (×N)
├── eui-page-header [label][isCollapsible][isCollapsed=false][expandedLabel][collapsedLabel]
│   ├── eui-page-header-sub-label .eui-u-flex-gap-2xs
│   │   ├── div.eui-u-flex.eui-u-flex-gap-m                            ← first row
│   │   │   ├── div.eui-u-c-bg-secondary-surface.eui-u-ph-s.eui-u-pv-4xs  ← CATEGORY
│   │   │   ├── eui-chip [euiSizeS][euiInfo]                           ← STATUS
│   │   │   └── (description text)
│   │   └── div.eui-u-flex.eui-u-flex-align-items-start.eui-u-flex-gap-xs  ← second row
│   │       ├── eui-icon-svg [icon="tag:regular"]
│   │       ├── eui-chip-list
│   │       │   ├── @for → eui-chip [euiSizeS] (×N, with maxVisibleChipsCount logic)
│   │       │   └── eui-chip-list-additional-content
│   │       │       └── button[euiButton][euiBasicButton][euiSecondary][euiSizeS]
│   │       │           └── eui-icon-svg [icon="eui-chevron-right" or "eui-chevron-left"]
│   │       └── button[euiButton][euiBasicButton][euiPrimary][euiSizeS]  ← "Manage"
│   ├── eui-page-header-action-items
│   │   ├── button[euiButton][euiSecondary]
│   │   ├── button[euiButton][euiPrimary]
│   │   ├── eui-dropdown
│   │   │   ├── button[euiButton][euiPrimary][euiBasicButton][euiRounded][euiIconButton]
│   │   │   │   └── eui-icon-svg [icon="eui-ellipsis-vertical"]
│   │   │   └── eui-dropdown-content
│   │   │       └── button[euiDropdownItem] (×N)
│   │   │           └── eui-icon-svg [icon="eui-chevron-right"][size="s"] + label text
│   │   └── eui-icon-toggle [iconSvgNameOn="eui-star"][iconSvgNameOff="eui-star"]
│   └── eui-page-header-body
│       └── eui-card
│           └── eui-card-content
│               └── (summary content)
```

---

## Variant 1: Simple Page Header

### Description

The Simple Page Header is the lightest variant: a breadcrumb navigation trail followed by a non-collapsible title, a subtitle (via `subLabel` input), and one or two direct action buttons. It contains no collapsible behavior, no metadata, no tags, no overflow dropdown, and no expandable body.

### Rules

1. Use `eui-page-header` with `label` and `subLabel` inputs — do NOT use `isCollapsible`, `expandedLabel`, or `collapsedLabel`.
2. Do NOT use `eui-page-header-sub-label` — the subtitle is provided via the `subLabel` input directly on `eui-page-header`.
3. Action items contain only direct buttons inside `eui-page-header-action-items`. No `eui-dropdown` overflow menu, no `eui-icon-toggle` favorite star.
4. If more than two actions are needed, switch to the **Advanced** variant instead.
5. Button hierarchy: primary actions use `euiPrimary`, secondary use `euiSecondary`. No size directive needed (default size).

### MCP Retrieval Strategy

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageHeaderComponent` | Page header inputs: `label`, `subLabel`, `isCollapsible`, collapse outputs |
| `get_component_docs` | `EuiPageBreadcrumbComponent` | Breadcrumb container, placement rules |
| `get_component_docs` | `EuiBreadcrumbComponent` | Breadcrumb navigation, item relationships |
| `get_component_docs` | `EuiBreadcrumbItemComponent` | Item inputs: `link`, `label`, `iconSvgName`, `ariaLabel` |
| `get_component_docs` | `EuiPageHeaderActionItemsComponent` | Action items container, positioning |

### Required Angular Imports (Simple)

Retrieve via MCP `get_component_docs` for each component. The following tokens must be spread in the component `imports` array:

- `EUI_PAGE` from `@eui/components/eui-page`
- `EUI_BREADCRUMB` from `@eui/components/eui-breadcrumb`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EUI_ICON` from `@eui/components/eui-icon`

---

## Variant 2: Advanced Page Header

### Description

The Advanced Page Header is the feature-rich variant that includes a breadcrumb, a collapsible title, a sub-label area with category badge, status chip, description text, and a tag list with expand/collapse control, page-level action buttons with an overflow dropdown and a favorite toggle, and a collapsible body area containing summary content inside a card. It is the go-to layout whenever a page needs to display detailed entity information at the top — such as a case detail page, a document overview, a profile page, or any page where the header carries structured metadata alongside a collapsible summary section.

### Rules

1. Use `eui-page-header` with `isCollapsible` to enable the expand/collapse toggle. Set `[isCollapsed]="false"` for initially expanded, provide `expandedLabel` and `collapsedLabel` for the toggle button labels.
2. Use `eui-page-header-sub-label` with `class="eui-u-flex-gap-2xs"` for the metadata area. Organize content in two rows: first row for category + status + description, second row for tags.
3. Render the category as a plain `div` with utility classes `eui-u-c-bg-secondary-surface eui-u-ph-s eui-u-pv-4xs`. Do NOT use a chip for the category.
4. Render the status as an `eui-chip` with `euiSizeS` and a status directive (`euiInfo`, `euiSuccess`, `euiWarning`, or `euiDanger`).
5. Render tags using `eui-icon-svg` with `icon="tag:regular"` followed by `eui-chip-list` with `eui-chip` items. Use `@for` control flow (Angular 17+) with `maxVisibleChipsCount` logic. Place the expand/collapse button inside `eui-chip-list-additional-content`.
6. The overflow dropdown trigger uses a **rounded icon button**: `euiButton euiPrimary euiBasicButton euiRounded euiIconButton` with `eui-ellipsis-vertical` icon. Dropdown items are prefixed with `eui-icon-svg icon="eui-chevron-right" size="s"`.
7. Use `eui-icon-toggle` for the favorite/star toggle with `iconSvgNameOn="eui-star"` and `iconSvgNameOff="eui-star"`. Place it as the last child of `eui-page-header-action-items`.
8. Use `eui-page-header-body` for the collapsible summary content. Place an `eui-card` > `eui-card-content` inside it.

### MCP Retrieval Strategy

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageHeaderComponent` | Page header: `label`, `isCollapsible`, `isCollapsed`, `expandedLabel`, `collapsedLabel`, `collapse` output |
| `get_component_docs` | `EuiPageBreadcrumbComponent` | Breadcrumb container |
| `get_component_docs` | `EuiBreadcrumbComponent` | Breadcrumb navigation |
| `get_component_docs` | `EuiBreadcrumbItemComponent` | Item inputs: `link`, `label`, `iconSvgName`, `ariaLabel` |
| `get_component_docs` | `EuiPageHeaderSubLabelComponent` | Sub-label container for metadata |
| `get_component_docs` | `EuiPageHeaderActionItemsComponent` | Action items container |
| `get_component_docs` | `EuiPageHeaderBodyComponent` | Collapsible body area |
| `get_component_docs` | `EuiChipComponent` | Chip: `euiSizeS`, status directives, `euiInfo`/`euiSuccess`/`euiWarning`/`euiDanger` |
| `get_component_docs` | `EuiChipListComponent` | Chip list: `ariaLabel`, max visible chips pattern |
| `get_component_docs` | `EuiDropdownComponent` | Overflow dropdown: positioning, accessibility, ARIA menu pattern |
| `get_component_docs` | `EuiIconToggleComponent` | Favorite toggle: `iconSvgNameOn`, `iconSvgNameOff`, `isChecked`, `ariaLabel` |

### Required Angular Imports (Advanced)

Retrieve via MCP `get_component_docs` for each component. The following tokens must be spread in the component `imports` array:

- `EUI_PAGE` from `@eui/components/eui-page`
- `EUI_BREADCRUMB` from `@eui/components/eui-breadcrumb`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EUI_ICON` from `@eui/components/eui-icon`
- `EUI_DROPDOWN` from `@eui/components/eui-dropdown`
- `EUI_CARD` from `@eui/components/eui-card`
- `EUI_CHIP` from `@eui/components/eui-chip`
- `EUI_CHIP_LIST` from `@eui/components/eui-chip-list`
- `EUI_ICON_TOGGLE` from `@eui/components/eui-icon-toggle`

---

## Generation Rules

When generating a page header following this pattern, an AI tool **must**:

### General Rules (both variants)

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: breadcrumb → header (with title, optional sub-label, action items, body).
3. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_BUTTON`).
4. **Use `ChangeDetectionStrategy.OnPush`** on the component.
5. **Use `@for` control flow** (Angular 17+) for iterating over chips, not `*ngFor`.
6. **Omit optional zones** only if explicitly not needed by the user's requirements. When in doubt, include all zones.
7. **Retrieve component documentation** from MCP tools (`get_component_docs`) before generating code to ensure correct API usage.
8. **Accessibility**: breadcrumb home item must have `ariaLabel="Home"`.

### Simple Header Rules

9. Use `eui-page-header` with `label` and `subLabel` inputs — do NOT use `isCollapsible`, `expandedLabel`, or `collapsedLabel`.
10. Do NOT use `eui-page-header-sub-label` — the subtitle is provided via the `subLabel` input.
11. Action items contain only direct buttons. No `eui-dropdown`, no `eui-icon-toggle`.
12. Button hierarchy: `euiPrimary` for primary, `euiSecondary` for secondary. Default size.
13. Maximum of two action buttons. If more are needed, use the **Advanced** variant.

### Advanced Header Rules

14. Use `eui-page-header` with `isCollapsible`, `[isCollapsed]="false"`, `expandedLabel`, and `collapsedLabel`.
15. Use `eui-page-header-sub-label` with `class="eui-u-flex-gap-2xs"` containing two rows.
16. Category badge is a styled `div` with `eui-u-c-bg-secondary-surface eui-u-ph-s eui-u-pv-4xs` — NOT an `eui-chip`.
17. Status uses `eui-chip` with `euiSizeS` and a semantic directive (`euiInfo`, `euiSuccess`, `euiWarning`, `euiDanger`).
18. Tags use `eui-chip-list` with `@for` control flow, conditional rendering based on `maxVisibleChipsCount`, and expand/collapse button in `eui-chip-list-additional-content`.
19. Overflow dropdown uses a rounded icon button: `euiButton euiPrimary euiBasicButton euiRounded euiIconButton` with `eui-ellipsis-vertical`. Dropdown items prefixed with `eui-icon-svg icon="eui-chevron-right" size="s"`.
20. Favorite toggle uses `eui-icon-toggle` with `iconSvgNameOn="eui-star"` and `iconSvgNameOff="eui-star"`.
21. Header body uses `eui-page-header-body` containing `eui-card` > `eui-card-content`.
22. The overflow dropdown button must have `euiTooltip="More actions"` and `[attr.aria-label]="'More actions menu'"`.
23. The tag expand/collapse button must have `[aria-label]` bound to a dynamic expression reflecting the current state.

---

## Key Differences Between Variants

| Aspect | Simple Header | Advanced Header |
|--------|--------------|-----------------|
| Collapsible | No | Yes (`isCollapsible`, `expandedLabel`, `collapsedLabel`) |
| Subtitle | `subLabel` input on `eui-page-header` | `eui-page-header-sub-label` with structured content |
| Category badge | Not used | Styled `div` with utility classes |
| Status chip | Not used | `eui-chip` with `euiSizeS` + status directive |
| Tags | Not used | `eui-chip-list` with expand/collapse logic |
| Actions | Up to 2 direct buttons | Buttons + overflow dropdown + favorite toggle |
| Overflow dropdown | Not used | Rounded icon button with `eui-ellipsis-vertical` |
| Favorite toggle | Not used | `eui-icon-toggle` with `eui-star` |
| Header body | Not used | Collapsible `eui-card` summary area |
| Additional imports | `EUI_PAGE`, `EUI_BREADCRUMB`, `EUI_BUTTON`, `EUI_ICON` | Adds: `EUI_DROPDOWN`, `EUI_CARD`, `EUI_CHIP`, `EUI_CHIP_LIST`, `EUI_ICON_TOGGLE` |
| Use case | Simple pages, list pages, forms | Detail pages, entity views, profile pages |

---

## Variant Selection Guide

When the user prompt specifies a page header, determine which variant to use:

- **Choose Simple** if the prompt mentions only: title, subtitle, and one or two buttons. Keywords: "simple", "basic", "minimal", "just a title", "few actions".
- **Choose Advanced** if the prompt mentions any of: collapsible, category, status, tags, metadata, overflow menu, more actions, favorite/bookmark, summary card, expandable body. Keywords: "advanced", "full", "detailed", "rich", "entity", "case", "document", "profile".
- **When in doubt**, ask the user for clarification. If no clarification is possible, default to the **Advanced** variant as it is the more complete pattern.

---

## MCP Component Documentation Summary

The following components are used in this pattern. Always retrieve their full documentation via the `get_component_docs` MCP tool before generating code:

| Component | Selector | Key Inputs | Purpose |
|-----------|----------|------------|---------|
| `EuiPageHeaderComponent` | `eui-page-header` | `label`, `subLabel`, `isCollapsible`, `isCollapsed`, `expandedLabel`, `collapsedLabel`, `labelTooltip`, `subLabelTooltip`, `isHeaderMultilines` | Main page header with title and collapse behavior |
| `EuiPageBreadcrumbComponent` | `eui-page-breadcrumb` | — | Breadcrumb container within `eui-page` |
| `EuiBreadcrumbComponent` | `eui-breadcrumb` | — | Breadcrumb navigation, manages item relationships |
| `EuiBreadcrumbItemComponent` | `eui-breadcrumb-item` | `id`, `label`, `link`, `iconSvgName`, `ariaLabel`, `navigationExtras` | Individual breadcrumb segment |
| `EuiPageHeaderSubLabelComponent` | `eui-page-header-sub-label` | — | Secondary metadata area below title (advanced only) |
| `EuiPageHeaderActionItemsComponent` | `eui-page-header-action-items` | — | Container for page-level action buttons |
| `EuiPageHeaderBodyComponent` | `eui-page-header-body` | — | Collapsible body content area (advanced only) |
| `EuiChipComponent` | `eui-chip` | `euiSizeS`, `euiInfo`, `euiSuccess`, `euiWarning`, `euiDanger`, `isChipRemovable`, `isFilled` | Compact status/tag indicator |
| `EuiChipListComponent` | `eui-chip-list` | `ariaLabel` | Container for multiple chip elements |
| `EuiDropdownComponent` | `eui-dropdown` | `position`, `hasClosedOnClickInside`, `isDropDownRightAligned` | Overflow actions menu |
| `EuiIconToggleComponent` | `eui-icon-toggle` | `iconSvgNameOn`, `iconSvgNameOff`, `isChecked`, `ariaLabel`, `iconSvgFillColorOn`, `iconSvgFillColorOff` | Toggleable icon button (favorite star) |
