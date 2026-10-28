---
name: Page List Card Variants Pattern
description: Documents the three standard card layout variants (Standard, Icon Actions, Full Card with Body and Footer) used inside any card-based list page across EUI-based applications.
label: page-list-cards-variants
category: pattern
applies-to: card-based list pages requiring different levels of complexity and information density
triggered-when: generating cards inside a page list body that need action dropdowns, icon buttons, collapsible content, metadata, tags, or favorites
requires: eui-card, eui-chip, eui-chip-list, eui-dropdown, eui-icon, eui-icon-toggle, eui-button, eui-input-checkbox, EuiTooltipDirective
outputs: card components following one of the three standard variants
related-skills: PAGE_LIST_CARDS_SIMPLE_PATTERN, PAGE_LIST_CARDS_SELECTION_PATTERN, PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN
---

# EUI Page List Card Variants Pattern — Canonical Structure Reference

## Purpose

This document describes the **Page List Card Variants** design pattern — the three standard card layout variants used inside any card-based list page across all EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

The component is domain-agnostic; data models and content are provided by the user.

### What is this pattern?

This pattern documents the **three card variants** that can be used inside `eui-page-column-body` in any page list pattern. Each variant represents a different level of complexity and information density:

- **Variant 1 — Standard card**: header-only card with title link, subtitle, status chip, and a text-based action dropdown.
- **Variant 2 — Icon actions card**: header-only card with title link, subtitle, status chip, rounded icon action buttons, and a rounded overflow dropdown.
- **Variant 3 — Full card with body and footer**: collapsible card with full title, structured subtitle (key-value metadata), left checkbox, status chip, expandable body content, footer with tag chip list (expand/collapse), favorite toggle, share button, and action dropdown.

---

## Recommended Usage

### How to select the right variant

| Variant | When to Use |
|---------|-------------|
| **Variant 1 — Standard** | Simple lists with text-based action menus |
| **Variant 2 — Icon Actions** | Lists needing quick icon-based actions (edit, delete) with overflow |
| **Variant 3 — Full Card** | Rich detail cards with metadata, tags, favorites, and expandable content |

---

## Variant 1 — Standard Card

### ASCII Structure

```
┌─────────────────────────────────────────────────────────────────┐
│ eui-card                                                        │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │ eui-card-header                                           │  │
│  │  Title (link)                                             │  │
│  │  Subtitle                                                 │  │
│  │                         [Status][Actions eui-chevron-down]│  │
│  │                                    [eui-edit] Edit        │  │
│  │                                    [eui-trash] Delete     │  │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

### Component Hierarchy

```
eui-card
└── eui-card-header
    ├── eui-card-header-title
    │   └── a.eui-u-text-link
    ├── eui-card-header-subtitle
    └── eui-card-header-right-content
        ├── eui-chip[euiSuccess]  ← status
        └── eui-dropdown
            ├── button[euiButton][euiBasicButton][euiPrimary][euiOutline][euiSizeS]
            │   └── span[euiIconSvg][icon="eui-chevron-down"]
            └── eui-dropdown-content
                ├── button[euiDropdownItem] > eui-icon-svg[icon="eui-edit"] + "Edit"
                └── button[euiDropdownItem] > eui-icon-svg[icon="eui-trash"] + "Delete"
```

### Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-chevron-down` | `span[euiIconSvg]` | Action dropdown trigger |
| `eui-edit` | `eui-icon-svg` | Edit action in dropdown |
| `eui-trash` | `eui-icon-svg` | Delete action in dropdown |

---

## Variant 2 — Icon Actions Card

### ASCII Structure

```
┌─────────────────────────────────────────────────────────────────┐
│ eui-card                                                        │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │ eui-card-header                                           │  │
│  │  Title (link)                                             │  │
│  │  Subtitle                                                 │  │
│  │          [Status] (eui-edit) (eui-trash) (eui-ellipsis-vertical) │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

### Component Hierarchy

```
eui-card
└── eui-card-header
    ├── eui-card-header-title
    │   └── a.eui-u-text-link
    ├── eui-card-header-subtitle
    └── eui-card-header-right-content
        └── div.eui-u-flex
            ├── eui-chip[euiSuccess]  ← status
            ├── button[euiButton][euiRounded][euiIconButton][euiBasicButton][euiPrimary][euiTooltip="Edit"]
            │   └── eui-icon-svg[icon="eui-edit"][fillColor="primary"]
            ├── button[euiButton][euiRounded][euiIconButton][euiBasicButton][euiDanger][euiTooltip="Delete"]
            │   └── eui-icon-svg[icon="eui-trash"][fillColor="danger"]
            └── eui-dropdown
                ├── button[euiButton][euiRounded][euiIconButton][euiBasicButton][euiSecondary][euiTooltip="More options"]
                │   └── eui-icon-svg[icon="eui-ellipsis-vertical"]
                └── eui-dropdown-content
                    └── button[euiDropdownItem] (×N)
```

### Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-edit` | `eui-icon-svg` | Rounded edit icon button (`fillColor="primary"`) |
| `eui-trash` | `eui-icon-svg` | Rounded delete icon button (`fillColor="danger"`) |
| `eui-ellipsis-vertical` | `eui-icon-svg` | Rounded overflow dropdown trigger |

---

## Variant 3 — Full Card with Body and Footer

### ASCII Structure

```
┌─────────────────────────────────────────────────────────────────┐
│ eui-card [euiCollapsible]                                       │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │ eui-card-header [hasFullTitle] [hasBottomExpander]         │  │
│  │  [] (checkbox)  Title (link, full width, tooltip)         │  │
│  │                                               [Status]    │  │
│  │  Key: Value                                               │  │
│  │  Key: Value                                               │  │
│  │  Key: Value                                               │  │
│  └───────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │ eui-card-content (collapsible body)                       │  │
│  │  Two-column metadata grid                                 │  │
│  └───────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │ eui-card-footer                                           │  │
│  │  [Tag] [Tag] [More >]    (★ fav) (share) [Actions ▼]     │  │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

### Component Hierarchy

```
eui-card [euiCollapsible]
├── eui-card-header [hasFullTitle][hasBottomExpander]
│   ├── eui-card-header-title
│   │   └── a.eui-u-text-link [euiTooltip] > strong
│   ├── eui-card-header-subtitle
│   │   └── div.eui-u-flex.eui-u-flex-column  ← key-value metadata rows
│   │       ├── div > span[euiLabel][euiSecondary][euiSizeS] + span.eui-u-f-s
│   │       ├── div > span[euiLabel][euiSecondary][euiSizeS] + span.eui-u-f-s
│   │       └── div > span[euiLabel][euiSecondary][euiSizeS] + span.eui-u-f-s
│   ├── eui-card-header-left-content
│   │   └── input[euiInputCheckBox]  ← selection checkbox
│   └── eui-card-header-right-content.eui-u-flex-column.eui-u-flex-justify-content-start
│       └── eui-chip[euiSuccess][euiSizeS] > span[euiLabel]
├── eui-card-content  ← collapsible body
│   └── div.row > div.col-md-6 (×2)  ← two-column metadata grid
└── eui-card-footer
    └── eui-card-footer-action-buttons.eui-u-flex.eui-u-flex-justify-content-between
        ├── div  ← tag chip list
        │   └── eui-chip-list
        │       ├── @for → eui-chip > span[euiLabel] (×N, conditional on maxVisibleChipsCount)
        │       └── eui-chip-list-additional-content
        │           └── button (expand/collapse with eui-chevron-left / eui-chevron-right)
        └── div.eui-u-ml-auto.eui-u-inline-flex
            ├── eui-card-footer-action-icons
            │   ├── eui-icon-toggle [iconSvgNameOn="eui-star"][iconSvgNameOff="eui-star"]
            │   └── button[euiButton][euiRounded][euiIconButton][euiBasicButton][euiPrimary]
            │       └── eui-icon-svg[icon="share-network:regular"][fillColor="secondary"]
            └── eui-card-footer-menu
                └── eui-dropdown
                    ├── button[euiButton][euiPrimary][euiOutline] + eui-icon-svg[icon="eui-chevron-down"]
                    └── eui-dropdown-content
                        └── button[euiDropdownItem] (×N)
```

### Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-star` | `eui-icon-toggle` | Favorite toggle (`iconSvgNameOn` and `iconSvgNameOff`) |
| `share-network:regular` | `eui-icon-svg` | Share rounded icon button (`fillColor="secondary"`) |
| `eui-chevron-down` | `eui-icon-svg` | Footer action dropdown trigger |
| `eui-chevron-right` | `eui-icon-svg` | Expand tags button |
| `eui-chevron-left` | `eui-icon-svg` | Collapse tags button |

---

## MCP Retrieval Strategy

Before generating code for this pattern, retrieve component documentation from MCP tools:

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiCardComponent` | Card container: `euiCollapsible` directive |
| `get_component_docs` | `EuiCardHeaderComponent` | Card header: `hasFullTitle`, `hasBottomExpander`, title/subtitle/left/right content |
| `get_component_docs` | `EuiCardContentComponent` | Collapsible card body content |
| `get_component_docs` | `EuiCardFooterComponent` | Card footer: action buttons, action icons, action menu |
| `get_component_docs` | `EuiChipComponent` | Status chip: `euiSuccess`, `euiWarning`, `euiDanger`, `euiInfo`, `euiSizeS` |
| `get_component_docs` | `EuiChipListComponent` | Tag chip list container with `ariaLabel` |
| `get_component_docs` | `EuiDropdownComponent` | Action dropdown for per-card actions and overflow menu |
| `get_component_docs` | `EuiIconToggleComponent` | Favorite toggle: `iconSvgNameOn`, `iconSvgNameOff`, `isChecked`, `toggle` output |
| `get_component_docs` | `EuiTooltipDirective` | Tooltip for icon-only buttons and title links |
| `get_component_inputs` | `EuiIconToggleComponent` | Full inputs: `keyboardAccessKey`, `iconSvgFillColorOn`, `iconSvgFillColorOff`, `ariaLabel` |

---

## Required Angular Imports

Retrieve via MCP `get_component_docs` for each component. The following tokens must be spread in the component `imports` array:

### Variant 1 — Standard Card

- `EUI_CARD` from `@eui/components/eui-card`
- `EUI_CHIP` from `@eui/components/eui-chip`
- `EUI_DROPDOWN` from `@eui/components/eui-dropdown`
- `EUI_ICON` from `@eui/components/eui-icon`
- `EUI_BUTTON` from `@eui/components/eui-button`

### Variant 2 — Icon Actions Card

- `EUI_CARD` from `@eui/components/eui-card`
- `EUI_CHIP` from `@eui/components/eui-chip`
- `EUI_DROPDOWN` from `@eui/components/eui-dropdown`
- `EUI_ICON` from `@eui/components/eui-icon`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EuiTooltipDirective` from `@eui/components/directives`

### Variant 3 — Full Card with Body and Footer

- `EUI_CARD` from `@eui/components/eui-card`
- `EUI_CHIP` from `@eui/components/eui-chip`
- `EUI_CHIP_LIST` from `@eui/components/eui-chip-list`
- `EUI_DROPDOWN` from `@eui/components/eui-dropdown`
- `EUI_ICON` from `@eui/components/eui-icon`
- `EUI_ICON_TOGGLE` from `@eui/components/eui-icon-toggle`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EUI_INPUT_CHECKBOX` from `@eui/components/eui-input-checkbox`
- `EuiTooltipDirective` from `@eui/components/directives`

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

When generating cards following these variants, an AI tool **must**:

### Variant Selection

1. **Select the appropriate variant** based on the user's requirements:
   - **Variant 1**: simple list with text-based action dropdown
   - **Variant 2**: list with quick icon actions (edit, delete) and overflow
   - **Variant 3**: rich detail cards with metadata, tags, favorites, and expandable content

### Variant 1 Rules

2. **Card action dropdown** uses `euiBasicButton euiPrimary euiOutline euiSizeS` with `eui-chevron-down` icon.
3. **Card title** is wrapped in `<a class="eui-u-text-link">` for navigation.
4. **Card subtitle** shows secondary descriptive information.

### Variant 2 Rules

5. **Icon buttons must be rounded**: `euiRounded euiIconButton euiBasicButton` with `fillColor` on the icon.
6. **Delete button uses `euiDanger`** (not `euiPrimary`), with `fillColor="danger"` on the icon.
7. **Overflow dropdown trigger** uses `euiSecondary` with `eui-ellipsis-vertical` icon.

### Variant 3 Rules

8. **Must use `euiCollapsible`** on `eui-card` and `hasFullTitle hasBottomExpander` on `eui-card-header`.
9. **Subtitle uses structured key-value metadata** with `span[euiLabel][euiSecondary][euiSizeS]` for labels.
10. **Footer uses `eui-card-footer-action-buttons`** with `eui-u-flex-justify-content-between` for layout.
11. **Tag chips use `eui-chip-list`** with `maxVisibleChipsCount` logic and expand/collapse button in `eui-chip-list-additional-content`.
12. **Footer icons use `eui-card-footer-action-icons`** for the favorite toggle and share button, and `eui-card-footer-menu` for the action dropdown.
13. **Favorite toggle** uses `eui-icon-toggle` with `iconSvgNameOn="eui-star"` and `iconSvgNameOff="eui-star"`, must have `[attr.aria-label]`.

### Common Rules

14. **Use `@for` control flow** (Angular 17+) for iterating over items and chips/tags. Track by item `id`.
15. **Spread EUI token arrays** in the component `imports`.
16. **Use `ChangeDetectionStrategy.OnPush`** on the component.
17. **Accessibility**: all icon-only buttons must have `euiTooltip` and `aria-label`. The favorite toggle must have `[attr.aria-label]`.
18. **Only import from `@angular/*` and `@eui/*`** packages.
19. **Data is user-defined** — the pattern is domain-agnostic. The user provides the interface and data.
20. **Retrieve component documentation** from MCP tools (`get_component_docs`) before generating code to ensure correct API usage.

---

## Key Differences Between Variants

| Aspect | Variant 1 (Standard) | Variant 2 (Icon Actions) | Variant 3 (Full Card) |
|--------|----------------------|--------------------------|------------------------|
| Card body | None (header only) | None (header only) | Collapsible content |
| Card footer | None | None | Tags, favorites, share, actions |
| Actions style | Text dropdown | Rounded icon buttons + overflow | Footer action menu |
| Selection | None | None | Checkbox in header left |
| Metadata | Subtitle only | Subtitle only | Structured key-value in subtitle + body grid |
| Tags | None | None | Chip list with expand/collapse |
| Favorite | None | None | `eui-icon-toggle` star |
