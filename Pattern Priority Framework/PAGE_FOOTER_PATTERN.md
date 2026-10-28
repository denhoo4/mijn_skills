---
name: Page Footer Pattern — Canonical Structure Reference
description: Describes the Page Footer design pattern with two variants (Simple and Advanced with Bulk Actions) used in eUI-based applications. Covers layout rules, flexbox structure, required components, and accessibility guidelines.
label: page-footer-pattern
category: pattern
applies-to: page footer with action buttons, bulk actions footer with selection counter
triggered-when: generating a page that requires footer actions (save, cancel, submit) or bulk actions (export, archive, delete) on selected items
requires: EUI page components, eui-button, eui-icon, eui-dropdown, EuiGrowlService, EuiTooltipDirective (advanced only)
outputs: a page footer following the Simple or Advanced (Bulk Actions) footer pattern
related-skills: SIMPLE_LAYOUT_PATTERN, FLUID_LAYOUT_PATTERN, PAGE_LIST_PATTERN
---

# EUI Page Footer Pattern — Canonical Structure Reference

## Purpose

This document describes the **Page Footer** design pattern — the sticky bottom action bar used across eUI-based applications. The footer groups together actions the user can perform depending on the page context.

### What is this pattern?

The Page Footer pattern provides a consistent location for page-level actions. It has **two variants**:

1. **Simple Page Footer** — Always visible, provides standard page actions (Save, Cancel, Submit) regardless of content state.
2. **Advanced Page Footer with Bulk Actions** — Conditionally rendered when items are selected, with `euiHighlighted` styling, a selection counter, and bulk operation buttons.

---

## Recommended Usage

### Simple Footer

Use when:

- A form page needs Save/Cancel/Submit buttons
- A detail page needs navigation or confirmation actions
- Actions are always available and do not depend on selection state
- No multi-selection or bulk operations are needed

### Advanced Footer

Use when:

- The page supports multi-selection (selectable cards or table rows)
- Bulk actions should appear only when items are selected
- The user needs to perform batch operations (export, archive, delete)
- A selection counter and reset mechanism are required

---

## ASCII Structure Overview

### Simple Footer

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page-footer                                                         │
│  ┌──────────────────────────────┬────────────────────────────────────┐  │
│  │ LEFT CONTENT                 │ RIGHT CONTENT                      │  │
│  │ Tertiary action (Cancel)     │ [Secondary] [Primary]              │  │
│  └──────────────────────────────┴────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

### Advanced Footer (Bulk Actions)

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page-footer euiHighlighted                                          │
│  ┌──────────────────────────────┬────────────────────────────────────┐  │
│  │ LEFT CONTENT                 │ RIGHT CONTENT                      │  │
│  │ [Reset] N selected item(s)   │ [Secondary] [Primary] [⋮ More]    │  │
│  └──────────────────────────────┴────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Footer | `eui-page-footer` | Yes | Footer container. Must be a direct child of `eui-page`. Supports `euiHighlighted` directive for bulk actions variant. |
| 2 | Inner Flex Wrapper | `div.eui-u-flex.eui-u-flex-gap-m` | Yes | Top-level flex container that separates left and right content groups. |
| 3 | Footer Left Content | `div.eui-u-flex.eui-u-flex-gap-s` | No | Contains dismissive/tertiary actions (Cancel, Reset) and optionally a selection counter. |
| 4 | Footer Right Content | `div.eui-u-flex.eui-u-flex-justify-content-end.eui-u-flex-gap-s` | Yes | Contains affirmative actions (Secondary, Primary) and optional overflow dropdown. |

---

## Component Hierarchy (DOM nesting order)

### Simple Footer

```
eui-page
├── eui-page-breadcrumb (optional)
├── eui-page-content
└── eui-page-footer
    └── div.eui-u-flex.eui-u-flex-gap-m
        ├── div.eui-u-flex.eui-u-flex-gap-s              ← Left content
        │   └── button[euiButton][euiBasicButton]        ← Tertiary action
        └── div.eui-u-flex.eui-u-flex-justify-content-end.eui-u-flex-gap-s  ← Right content
            ├── button[euiButton][euiSecondary]           ← Secondary action
            └── button[euiButton][euiPrimary]             ← Primary action
```

### Advanced Footer (Bulk Actions)

```
eui-page
├── eui-page-breadcrumb (optional)
├── eui-page-content
└── @if (selectedCount() > 0)
    └── eui-page-footer[euiHighlighted]
        └── div.eui-u-flex.eui-u-flex-gap-m
            ├── div.eui-u-flex.eui-u-flex-gap-s              ← Left content
            │   ├── button[euiButton][euiBasicButton]        ← Reset/Tertiary action
            │   └── div.eui-u-display-flex                   ← Selection counter
            │       └── span.eui-u-f-bold + text
            └── div.eui-u-flex.eui-u-flex-justify-content-end.eui-u-flex-gap-s  ← Right content
                ├── button[euiButton][euiSecondary]           ← Cancel/Secondary
                │   └── eui-icon-svg[icon]
                ├── button[euiButton][euiPrimary]             ← Primary bulk action
                │   └── eui-icon-svg[icon]
                └── eui-dropdown                              ← Optional more actions
                    ├── button[euiButton][euiRounded][euiIconButton][euiBasicButton][euiPrimary]
                    │   └── eui-icon-svg[icon="eui-ellipsis-vertical"]
                    └── eui-dropdown-content
                        └── button[euiDropdownItem] (×N)
```

---

## Variant 1: Simple Page Footer

### Flexbox Layout Rules

The simple footer uses a two-zone flex layout:

- **Outer wrapper**: `eui-u-flex eui-u-flex-gap-m` — Creates the horizontal flex container with medium gap between left and right zones.
- **Left zone**: `eui-u-flex eui-u-flex-gap-s` — Contains tertiary/dismissive actions with small gap spacing.
- **Right zone**: `eui-u-flex eui-u-flex-justify-content-end eui-u-flex-gap-s` — Pushes affirmative actions to the right with small gap spacing.

### Rules

1. Use `eui-u-flex eui-u-flex-gap-m` on the inner wrapper div to create horizontal separation between zones.
2. Place dismissive actions (Cancel, Back, Reset) on the **left** side using `euiBasicButton` style.
3. Place affirmative actions (Save, Submit, Export) on the **right** side.
4. Use `eui-u-flex-justify-content-end` on the right container to align buttons to the far right.
5. Use `eui-u-flex-gap-s` on both left and right containers for consistent button spacing.
6. Order right-side actions from least important (secondary) to most important (primary), left to right.
7. Do NOT use `euiHighlighted` on simple page footers — reserved for bulk action footers.
8. Do NOT conditionally show/hide simple page footers — they must always be visible.
9. Icons inside buttons are optional but recommended for visual clarity.

### MCP Retrieval Strategy

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageFooterComponent` | Footer container, inputs, `euiHighlighted` support |
| `get_component_docs` | `EuiGrowlService` | `growl()` method signature and severity options for action feedback |

---

## Variant 2: Advanced Page Footer with Bulk Actions

### Flexbox Layout Rules

The advanced footer uses the same two-zone flex layout as the simple footer, but adds:

- **Outer wrapper**: `eui-u-flex eui-u-flex-gap-m` — Same horizontal flex container.
- **Left zone**: `eui-u-flex eui-u-flex-gap-s` — Contains the reset button and a selection counter (`eui-u-display-flex` for inline counter).
- **Right zone**: `eui-u-flex eui-u-flex-justify-content-end eui-u-flex-gap-s` — Contains secondary, primary, and optional dropdown overflow actions.

### Rules

1. Always wrap in `@if (selectedCount() > 0)` — this footer must only appear when items are selected.
2. Always apply the `euiHighlighted` directive on `eui-page-footer` to visually distinguish from simple footers.
3. Use `eui-u-flex eui-u-flex-gap-m` on the inner wrapper div (same as simple footer).
4. Left content must include a Reset/Tertiary button (`euiBasicButton`) and a selection counter.
5. The selection counter uses `eui-u-display-flex` with a `span.eui-u-f-bold` for the count value.
6. Right content must include action buttons with icons (`eui-icon-svg`) for visual clarity.
7. Use `eui-u-flex-justify-content-end eui-u-flex-gap-s` on the right container.
8. Optionally include a "More actions" `eui-dropdown` for additional bulk operations beyond the primary action.
9. The dropdown trigger must use `euiRounded euiIconButton euiBasicButton euiPrimary` with `eui-icon-svg[icon="eui-ellipsis-vertical"]`.
10. Always provide `[attr.aria-label]` on the dropdown trigger and `aria-label` on each dropdown item.
11. Use `[euiTooltip]` on the dropdown trigger button to display "More actions" tooltip on hover.
12. Use Angular signals (`signal()`) for the selection count to enable reactive updates.

### MCP Retrieval Strategy

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageFooterComponent` | Footer container with `euiHighlighted` support |
| `get_component_docs` | `EuiDropdownComponent` | Overflow actions menu, positioning, and accessibility |
| `get_component_docs` | `EuiTooltipDirective` | Tooltip on icon-only buttons |
| `get_component_docs` | `EuiGrowlService` | Toast notifications for bulk action feedback |

---

## EuiGrowlService Usage

Retrieve full API documentation via `get_component_docs("EuiGrowlService")`.

### Method Signatures

| Method | Signature | Description |
|--------|-----------|-------------|
| `growl` | `growl(msg: EuiGrowlMessage, isSticky?, isMultiple?, life?, position?, callback?, ariaLive?)` | Full growl with configurable options |
| `growlSuccess` | `growlSuccess(msg: string, position?)` | Green success notification |
| `growlInfo` | `growlInfo(msg: string, position?)` | Blue info notification |
| `growlWarning` | `growlWarning(msg: string, position?)` | Yellow warning notification |
| `growlError` | `growlError(msg: string, position?)` | Red error notification (sticky by default) |
| `clearGrowl` | `clearGrowl()` | Removes all current notifications |

### EuiGrowlMessage Object

The message object uses the following shape: `{ severity, summary, detail }` where severity is one of `success`, `info`, `warning`, or `danger`.

---

## Generation Rules

When generating a page footer following this pattern, an AI tool **must**:

### General Rules

1. **Always place `eui-page-footer`** as a direct child of `eui-page`.
2. **Use `eui-u-flex eui-u-flex-gap-m`** on the inner wrapper div to create the two-zone layout.
3. **Left zone** uses `eui-u-flex eui-u-flex-gap-s` for dismissive/tertiary actions.
4. **Right zone** uses `eui-u-flex eui-u-flex-justify-content-end eui-u-flex-gap-s` for affirmative actions.
5. **Use `ChangeDetectionStrategy.OnPush`** on the component.
6. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_BUTTON`).
7. **Use `inject()`** for service injection (e.g., `EuiGrowlService`).
8. **Retrieve component documentation** from MCP tools (`get_component_docs`) before generating code.

### Simple Footer Rules

9. Do NOT conditionally render the footer — it must always be visible.
10. Do NOT use `euiHighlighted` on simple footers.
11. Use `euiBasicButton` style for tertiary/dismissive actions on the left.
12. Use `euiSecondary` and `euiPrimary` for right-side affirmative actions.

### Advanced Footer Rules

13. Always wrap in `@if (selectedCount() > 0)`.
14. Always apply `euiHighlighted` on `eui-page-footer`.
15. Include a selection counter in the left zone using `span.eui-u-f-bold` for the count.
16. Use Angular signals (`signal()`) for reactive selection count.
17. Include icons (`eui-icon-svg`) in the right-side action buttons.
18. Optionally include an overflow `eui-dropdown` for additional bulk operations.
19. Import `EuiTooltipDirective` from `@eui/components/directives` when using `[euiTooltip]`.

### Accessibility

20. All icon-only buttons must have `[attr.aria-label]` or `[euiTooltip]`.
21. Each dropdown action item must have `aria-label`.
22. Ensure footer actions are keyboard accessible.
23. Use `role="contentinfo"` on the footer for proper document structure (handled by the component).

---

## Key Differences Between Variants

| Aspect | Simple Footer | Advanced Footer (Bulk Actions) |
|--------|--------------|-------------------------------|
| Visibility | Always visible | Conditionally shown (`@if`) |
| `euiHighlighted` | No | Yes |
| Left content | Tertiary action only | Reset button + selection counter |
| Right content | Secondary + Primary buttons | Secondary + Primary + optional dropdown |
| Icons in buttons | Optional | Recommended |
| Selection state | None | `signal()` based counter |
| Dropdown overflow | Not used | Optional "More actions" menu |
| Additional imports | None | `EuiTooltipDirective` from `@eui/components/directives` |
| Use case | Forms, detail pages | Selectable lists, bulk operations |
