---
name: Page List Cards Filter Pattern
description: A two-column search & results page with a collapsible filter sidebar, selectable collapsible cards list, removable criteria chips, dimmer highlight on selection, and a conditional highlighted page footer for bulk actions.
label: page-list-cards-filter-ai
category: pattern
applies-to: two-column search and results page with filter sidebar, selectable collapsible cards, and bulk action footer
triggered-when: generating a filterable list page with selectable items and bulk actions, a search page with advanced filters, or a page with multi-criteria filtering and batch processing
requires: eUI page components, filter components, eui-card, eui-chip, eui-chip-list, eui-fieldset, eui-input-text, eui-select, EuiAppShellService, EuiGrowlService
outputs: a two-column page following the Cards Filter pattern
related-skills: PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN, PAGE_LIST_CARDS_SELECTION_PATTERN, PAGE_LIST_CARDS_SIMPLE_PATTERN, COLUMNS_LAYOUT_PATTERN
---

# EUI Page List Cards Filter Pattern — Canonical Structure Reference

## Purpose

This document describes the **Page List Cards Filter** design pattern — a two-column search & results page
with a collapsible filter sidebar and a main content column with selectable cards, bulk actions in a highlighted page footer.

### What is this pattern?

A two-column search & results page containing:
- Page header following the **PAGE_HEADER_PATTERN** (Simple variant)
- A **collapsible filter sidebar** (left column) with text search, quick filters (checkboxes), and advanced expandable filters (selects)
- A **results column** (right column) with label/subLabel header, removable filter criteria chips, selectable collapsible cards list, and pagination
- A **select all / unselect all toggle** with indeterminate state support
- A selectable collapsible cards list with per-card checkboxes, expandable card content, status chips, and per-card action dropdowns
- **Dimmer highlight** on the result column when items are selected
- A **conditional highlighted page footer** following the **PAGE_FOOTER_PATTERN** (Advanced variant with Bulk Actions)

Use this layout whenever a user needs to **filter a list and perform batch operations on selected items**.

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
- A page needs advanced multi-criteria filtering with a sidebar
- Items must be selectable for batch/bulk operations (export, delete, archive)
- Active filter criteria should be visible and removable as chips
- A conditional footer bar is needed for bulk actions on selection

Do not use when:
- No filtering is needed (use Cards List Simple or Cards Selection instead)
- No selection/bulk actions are needed (use the base cards-filter pattern without selection)
- A single-column list suffices without a sidebar

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 1. PAGE HEADER (see PAGE_HEADER_PATTERN — Simple variant)         │  │
│  │    Breadcrumb + Title + Subtitle + Action buttons                 │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ eui-page-content > eui-page-columns                               │  │
│  │  ┌──────────────────────┐  ┌──────────────────────────────────┐   │  │
│  │  │ 2. FILTER COLUMN     │  │ 3. RESULT COLUMN                 │   │  │
│  │  │  (collapsible)       │  │    Title + N results found       │   │  │
│  │  │  [Reset filters btn] │  │    [euiHighlighted] on selection │   │  │
│  │  │  ┌────────────────┐  │  │                      4. ACTIONS  │   │  │
│  │  │  │ Text search    │  │  ├──────────────────────────────────┤   │  │
│  │  │  │ [euiClearable] │  │  │ 5. FILTER CRITERIA CHIPS         │   │  │
│  │  │  │ [eui-search]   │  │  │    Selected: [chip×] Clear all   │   │  │
│  │  │  └────────────────┘  │  ├──────────────────────────────────┤   │  │
│  │  │  ┌────────────────┐  │  │ 6. SELECT ALL TOGGLE             │   │  │
│  │  │  │ Quick Filters  │  │  │    [✓] Select all — N selected   │   │  │
│  │  │  │ (expandable)   │  │  ├──────────────────────────────────┤   │  │
│  │  │  │ ☑ Status 1     │  │  │ 7. SELECTABLE COLLAPSIBLE CARDS  │   │  │
│  │  │  │ ☑ Status 2     │  │  │  ┌────────────────────────────┐  │   │  │
│  │  │  └────────────────┘  │  │  │ [✓] eui-card   [Status] ▼  │  │   │  │
│  │  │  ┌────────────────┐  │  │  │  Title (link)  Actions     │  │   │  │
│  │  │  │ Advanced       │  │  │  │  Subtitle line             │  │   │  │
│  │  │  │ (collapsed)    │  │  │  │  ─── bottom expander ───   │  │   │  │
│  │  │  │ [Dept ▼]       │  │  │  │  [Card content details]   │  │   │  │
│  │  │  └────────────────┘  │  │  └────────────────────────────┘  │   │  │
│  │  │                      │  ├──────────────────────────────────┤   │  │
│  │  │                      │  │ 8. PAGINATOR (with page numbers) │   │  │
│  │  └──────────────────────┘  └──────────────────────────────────┘   │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 9. PAGE FOOTER (see PAGE_FOOTER_PATTERN — Advanced variant)       │  │
│  │    @if selectedCount() > 0                                        │  │
│  │    [Reset] N selected     [Cancel] [Primary action] [▼ More]      │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Header | See **PAGE_HEADER_PATTERN** (Simple variant) | Yes | Breadcrumb, page title with `label` and `subLabel`, action items with secondary and primary buttons (no overflow dropdown). |
| 2 | Filter Column | `eui-page-column` [label, euiSize3XL, isCollapsible] | Yes | Left sidebar with text search (`euiInputText` + `euiClearable`), quick filters (`eui-fieldset` with `isExpandable`, status checkboxes), and advanced filters (`eui-fieldset` with `[isExpanded]="false"`, department select). Header right content is a "Reset filters" button (`euiButton euiPrimary euiBasicButton euiSizeS`). |
| 3 | Result Column | `eui-page-column` [label, subLabel=dynamic, euiHighlighted] | Yes | Uses `label` and `[subLabel]` inputs directly. Binds `[euiHighlighted]` to `(appShellService.state$ | async)?.isDimmerActive`. |
| 4 | Column Actions | `eui-page-column-header-right-content` | No | Contextual action buttons (secondary S + primary S) in a flex container with gap. |
| 5 | Filter Criteria Chips | `eui-page-column-header-body` | No | Conditionally shown when active filters exist. Contains "Selected criteria:" text + "Clear all" link + `eui-chip-list` with `isChipsRemovable` and `euiSizeS`. Each chip has `[isChipRemovable]="true"` and binds `(remove)` event. Chip content uses `<span euiLabel>`. |
| 6 | Select All Toggle | Inside `eui-page-column-body` (before cards list) | Yes | Checkbox (`euiInputCheckBox`) with `[checked]`, `[indeterminate]`, and `(change)` bindings. Label shows "Select all" / "Unselect all" with count. |
| 7 | Selectable Collapsible Cards List | `eui-page-column-body` | Yes | `@for` loop of `eui-card[euiSelected][euiCollapsible][euiCollapsed]` with `hasBottomExpander` on card header, per-card checkbox, title link, subtitle, status chip (`euiSizeS` with `<span euiLabel>`), per-card action dropdown (trigger button with label text + icon), and expandable card content section. |
| 8 | Paginator | `eui-page-column-footer` > `eui-paginator` | No | Pagination control bound to filtered items count, with `pageSize`, `page`, `hasPageNumberNavigation`, and `(pageChange)` bindings. |
| 9 | Page Footer | See **PAGE_FOOTER_PATTERN** (Advanced variant) | Conditional | `@if (selectedCount() > 0)`. Left group: Reset basic button + "N selected item(s)" text. Right group: Cancel (secondary with close icon) + Primary action (with icon) + More actions dropdown (rounded icon button with tooltip). |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── [PAGE HEADER — See PAGE_HEADER_PATTERN Simple variant]
│   ├── eui-page-breadcrumb > eui-breadcrumb > eui-breadcrumb-item (×N)
│   ├── eui-page-header [label][subLabel]
│   │   └── eui-page-header-action-items
│   │       ├── button[euiButton][euiSecondary]
│   │       └── button[euiButton][euiPrimary]
├── eui-page-content
│   └── eui-page-columns [hasPreventMobileRendering]
│       ├── eui-page-column [label="Search filter"][euiSize3XL][isCollapsible]  ← FILTER
│       │   ├── eui-page-column-header-right-content
│       │   │   └── button[euiButton][euiPrimary][euiBasicButton][euiSizeS] → "Reset filters"
│       │   └── eui-page-column-body
│       │       └── div.eui-u-flex.eui-u-flex-column
│       │           ├── div[euiInputGroup]  ← Text search
│       │           │   ├── label[euiLabel]
│       │           │   ├── div (helper text, class eui-u-f-s)
│       │           │   └── div[euiInputGroupAddOn]
│       │           │       ├── input[euiInputText][euiClearable][value][placeholder]
│       │           │       └── button[euiButton][euiIconButton][euiPrimary][euiOutline] + eui-icon-svg[icon="eui-search"]
│       │           ├── eui-fieldset [label][isLarge][isExpandable]  ← Quick filters (status checkboxes)
│       │           │   └── div[euiInputGroup]
│       │           │       └── div.eui-u-flex.eui-u-flex-wrap.eui-u-flex-gap-s
│       │           │           └── @for (status of statuses; track status)
│       │           │               └── div.eui-u-inline-flex
│       │           │                   ├── input[euiInputCheckBox][id][checked](change)
│       │           │                   └── label[for][euiLabel]
│       │           └── eui-fieldset [label][isLarge][isExpandable][isExpanded=false]  ← Advanced filters
│       │               └── div.eui-u-flex.eui-u-flex-column.eui-u-mt-m
│       │                   └── div[euiInputGroup]
│       │                       ├── label[euiLabel]
│       │                       └── select[euiSelect][value](change)
│       │                           ├── option[value=""] (default "All" option)
│       │                           └── @for option (×N)
│       └── eui-page-column [label][subLabel][euiHighlighted]  ← RESULTS
│           ├── @if (activeFilters().length > 0)
│           │   └── eui-page-column-header-body  ← Criteria chips
│           │       └── div.eui-u-flex.eui-u-flex-gap-m.eui-u-flex-align-items-center
│           │           ├── div.eui-u-f-s → "Selected criteria:" + a.eui-u-text-link "Clear all"
│           │           └── eui-chip-list [isChipsRemovable][euiSizeS][ariaLabel]
│           │               └── @for (filter of activeFilters(); track filter.label)
│           │                   └── eui-chip [isChipRemovable]="true" (remove)
│           │                       └── span[euiLabel]
│           ├── eui-page-column-header-right-content
│           │   └── div.eui-u-flex.eui-u-flex-gap-s
│           │       ├── button[euiButton][euiSecondary][euiSizeS]
│           │       └── button[euiButton][euiPrimary][euiSizeS]
│           ├── eui-page-column-body
│           │   ├── div.eui-u-flex.eui-u-m-m  ← select all toggle
│           │   │   ├── input[euiInputCheckBox][id][checked][indeterminate](change)[aria-label]
│           │   │   └── label[for][euiLabel]  ← "Select all / Unselect all — N selected out of M"
│           │   └── @for (item of paginatedItems(); track item.id)
│           │       └── eui-card[euiSelected][euiCollapsible][euiCollapsed].eui-u-mb-m
│           │           ├── eui-card-header [hasBottomExpander]
│           │           │   ├── eui-card-header-left-content
│           │           │   │   └── div.eui-u-flex.eui-u-flex-justify-content-center
│           │           │   │       └── input[euiInputCheckBox][id][checked](change)[attr.aria-label]
│           │           │   ├── eui-card-header-title
│           │           │   │   └── a.eui-u-text-link (click)
│           │           │   ├── eui-card-header-subtitle
│           │           │   └── eui-card-header-right-content
│           │           │       └── div.eui-u-flex.eui-u-flex-align-items-center.eui-u-flex-gap-s (click)="$event.stopPropagation()"
│           │           │           ├── eui-chip [status directives][euiSizeS]
│           │           │           │   └── span[euiLabel]
│           │           │           └── eui-dropdown
│           │           │               ├── button[euiButton][euiPrimary][euiOutline][euiSizeS][attr.aria-label]
│           │           │               │   ├── span[euiLabel] → "Actions"
│           │           │               │   └── eui-icon-svg [icon="eui-ellipsis-vertical"][size="s"]
│           │           │               └── eui-dropdown-content
│           │           │                   └── button[euiDropdownItem](click)[aria-label] (×N)
│           │           └── eui-card-content
│           │               └── div.row > div.col-md-* (detail fields layout)
│           └── eui-page-column-footer
│               └── eui-paginator [length][pageSize][page][hasPageNumberNavigation](pageChange)
└── [PAGE FOOTER — See PAGE_FOOTER_PATTERN Advanced variant]
    └── @if (selectedCount() > 0)
        └── eui-page-footer [euiHighlighted]
            └── div.eui-u-flex.eui-u-flex-gap-m
                ├── div.eui-u-flex.eui-u-flex-gap-s  ← Left group
                │   ├── button[euiButton][euiBasicButton] → "Reset"
                │   └── div.eui-u-display-flex → span.eui-u-f-bold "N" + "selected item(s)"
                └── div.eui-u-flex.eui-u-flex-justify-content-end.eui-u-flex-gap-s  ← Right group
                    ├── button[euiButton][euiSecondary][aria-label]
                    │   ├── eui-icon-svg [icon="eui-close"]
                    │   └── "Cancel"
                    ├── button[euiButton][euiPrimary][aria-label]
                    │   ├── eui-icon-svg [icon="eui-download"]
                    │   └── "Export" (or primary bulk action label)
                    └── eui-dropdown
                        ├── button[euiButton][euiRounded][euiIconButton][euiBasicButton][euiPrimary][attr.aria-label][euiTooltip]
                        │   └── eui-icon-svg [icon="eui-ellipsis-vertical"]
                        └── eui-dropdown-content
                            └── button[euiDropdownItem](click)[aria-label] (×N)
```

---

## Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-home` | `eui-breadcrumb-item` | Breadcrumb home item (`iconSvgName`) |
| `eui-search` | `eui-icon-svg` | Text search button in filter column |
| `eui-ellipsis-vertical` | `eui-icon-svg` | Per-card action dropdown trigger (size="s") + Footer "More actions" overflow dropdown trigger |
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
| `get_component_docs` | `EuiPageColumnComponent` | Single column: `label`, `subLabel`, `euiSize3XL`, `isCollapsible`, `euiHighlighted` |
| `get_component_docs` | `EuiFieldsetComponent` | Fieldset: `label`, `isExpandable`, `isExpanded`, `isLarge` |
| `get_component_docs` | `EuiCardComponent` | Card: `euiSelected`, `euiCollapsible`, `euiCollapsed` |
| `get_component_docs` | `EuiCardHeaderComponent` | Card header: `hasBottomExpander` |
| `get_component_docs` | `EuiCardContentComponent` | Card expandable content body |
| `get_component_docs` | `EuiChipComponent` | Status chips: `euiSuccess`, `euiWarning`, `euiDanger`, `euiInfo`, `euiSizeS`, `isChipRemovable` |
| `get_component_docs` | `EuiChipListComponent` | Chip list: `isChipsRemovable`, `euiSizeS`, `ariaLabel` |
| `get_component_docs` | `EuiDropdownComponent` | Overflow dropdown menus |
| `get_component_docs` | `EuiDropdownContentComponent` | Dropdown content container |
| `get_component_docs` | `EuiPaginatorComponent` | Paginator: `length`, `pageSize`, `page`, `hasPageNumberNavigation`, `(pageChange)` |
| `get_component_docs` | `EuiPageFooterComponent` | Footer with `euiHighlighted` support |
| `get_component_docs` | `EuiInputCheckboxComponent` | Checkbox: `checked`, `indeterminate` inputs |
| `get_component_docs` | `EuiInputTextComponent` | Text input with `euiClearable` |
| `get_component_docs` | `EuiSelectComponent` | Select dropdown for filter categories |
| `get_component_docs` | `EuiGrowlService` | Toast notifications for action feedback |
| `get_component_docs` | `EuiTooltipDirective` | Tooltip on icon-only buttons |

---

## Required Angular Imports

Retrieve via MCP `get_component_docs` for each component. The following tokens must be spread in the component `imports` array:

- `AsyncPipe` from `@angular/common`
- `DecimalPipe` from `@angular/common` (if currency/number formatting is needed)
- `EUI_PAGE` from `@eui/components/eui-page`
- `EUI_BREADCRUMB` from `@eui/components/eui-breadcrumb`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EUI_CARD` from `@eui/components/eui-card`
- `EUI_CHIP` from `@eui/components/eui-chip`
- `EUI_CHIP_LIST` from `@eui/components/eui-chip-list`
- `EUI_DROPDOWN` from `@eui/components/eui-dropdown`
- `EUI_FIELDSET` from `@eui/components/eui-fieldset`
- `EUI_ICON` from `@eui/components/eui-icon`
- `EUI_INPUT_CHECKBOX` from `@eui/components/eui-input-checkbox`
- `EUI_INPUT_GROUP` from `@eui/components/eui-input-group`
- `EUI_INPUT_TEXT` from `@eui/components/eui-input-text`
- `EUI_LABEL` from `@eui/components/eui-label`
- `EUI_PAGINATOR` from `@eui/components/eui-paginator`
- `EUI_SELECT` from `@eui/components/eui-select`
- `EuiTooltipDirective` from `@eui/components/directives`

Services (injected via `inject()`):
- `EuiAppShellService` from `@eui/core`
- `EuiGrowlService` from `@eui/core`

---

## Filter Architecture (Left Column — Angular Signals)

The filter column uses Angular signals for reactive state management. The implementation must include:

- A `signal<string>` for text search input (minimum 3 characters to trigger filtering)
- A `signal<Set<string>>` for multi-select status checkboxes
- A `signal<string | null>` for each category/department select filter
- A `computed()` for the filtered items list that reacts to all filter signals
- A `computed()` for paginated items derived from filtered items, current page, and page size
- A `computed()` for active filter labels (used to render removable criteria chips)

### Required Filter Methods

| Method | Trigger | Description |
|--------|---------|-------------|
| `onSearch(event)` | Text search input `(input)` event | Updates search signal, clears selection, resets page |
| `toggleStatus(status, checked)` | Status checkboxes `(change)` event | Toggles status in the set, clears selection, resets page |
| `onDepartmentChange(event)` | Department select `(change)` event | Updates department filter, clears selection, resets page |
| `clearAllFilters()` | "Reset filters" button / "Clear all" link | Resets all filters, clears selection, resets page |
| `removeFilter(filter)` | Criteria chip `(remove)` event | Removes a single filter, clears selection, resets page |
| `isStatusChecked(status)` | Checkbox `[checked]` binding | Returns whether a specific status is in the selected set |

**Important:** Always clear selection and reset pagination when any filter changes to prevent stale selections referencing items no longer in the filtered list.

---

## Selection State Management (Signals-based)

The selection logic uses Angular signals for reactive state management. The implementation must include:

- A `signal<Set<number>>` holding the set of selected item IDs
- A `signal<number>` for current page index (zero-based)
- A `signal<number>` for page size
- A `computed` for `selectedCount` derived from the signal's size
- A `computed` for `isAllSelected` comparing selection count to filtered items length
- A `computed` for `isIndeterminate` (some but not all selected)
- A `computed` for `paginatedItems` slicing filtered items by current page and page size
- An `effect()` to activate/deactivate the dimmer via `EuiAppShellService.isDimmerActive` based on `selectedCount() > 0`

### Required Selection Methods

| Method | Description |
|--------|-------------|
| `isCardSelected(id)` | Returns whether a specific item is selected |
| `toggleCardSelection(id)` | Toggles an individual item's selection state |
| `toggleSelectAll()` | Toggles all filtered items selected/deselected |
| `clearSelection()` | Clears all selections (used by Reset/Cancel) |
| `onPageChange(event)` | Updates currentPage and pageSize from paginator event |

---

## Status Chip Mapping

| Status Value | Directive | Visual |
|-------------|-----------|--------|
| Active / Approved | `[euiSuccess]` | Green chip |
| Under Review / Pending | `[euiWarning]` | Orange/amber chip |
| Expired / Rejected | `[euiDanger]` | Red chip |
| Draft / New | `[euiInfo]` | Blue chip |

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### Layout Rules

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: header (per PAGE_HEADER_PATTERN) → page-content (columns) → conditional footer (per PAGE_FOOTER_PATTERN).
3. **Use `eui-page-columns` with `hasPreventMobileRendering`** inside `eui-page-content`.
4. **Apply the PAGE_HEADER_PATTERN** (Simple variant) for breadcrumb, title, subtitle, and action items (secondary + primary buttons, no overflow dropdown at page header level).
5. **Apply the PAGE_FOOTER_PATTERN** (Advanced variant) for the conditional highlighted footer with bulk actions.
6. **Filter column is always the first `eui-page-column`** with a descriptive `label`, `euiSize3XL`, and `isCollapsible`. The header action is a button (`button[euiButton][euiPrimary][euiBasicButton][euiSizeS]`) for resetting filters.
7. **Result column uses `label` and `[subLabel]` inputs** directly on `eui-page-column` for the header title and dynamic result count.
8. **Result column binds `[euiHighlighted]`** to `(appShellService.state$ | async)?.isDimmerActive` for selection visual feedback.
9. **Use `ChangeDetectionStrategy.OnPush`** on the component.
10. **Spread EUI token arrays** in the component `imports`.
11. **Include `AsyncPipe`** in imports for the dimmer state observable binding.

### Filter Rules (Left Column)

12. **Text search uses `div[euiInputGroupAddOn]`** with `input[euiInputText][euiClearable]` bound to `[value]` and `(input)`, with a `placeholder` attribute, and a search icon button (`euiButton euiIconButton euiPrimary euiOutline`).
13. **Quick filters use `eui-fieldset` with `isExpandable` and `isLarge`** expanded by default, containing a single `div[euiInputGroup]` with status checkboxes in a flex-wrap layout.
14. **Advanced filters use `eui-fieldset` with `[isExpanded]="false"` and `isLarge`** (collapsed by default), containing a select with a default "All" empty-value option.
15. **Use Angular signals** for all filter state and `computed()` for filtered data.
16. **Clear selection and reset pagination when any filter changes** to prevent stale selections.

### Filter Criteria Chips Rules

17. **Use `eui-chip-list` with `isChipsRemovable`, `euiSizeS`, and `ariaLabel`** at the list level.
18. **Conditionally show chips** only when active filters exist using `@if`.
19. **Each chip uses `[isChipRemovable]="true"` and binds `(remove)` event** to remove the corresponding filter. Chip display text is wrapped in `<span euiLabel>`.
20. **Include a "Clear all" text link** (`a.eui-u-text-link`) to reset all filters.
21. **Wrap chips area in a flex container** with `eui-u-flex-align-items-center` for vertical alignment.

### Selection Rules

22. **Place select-all toggle at the top of `eui-page-column-body`** in a `div.eui-u-flex.eui-u-m-m` with `[checked]`, `[indeterminate]`, and `(change)` bindings.
23. **Each card has a per-card checkbox** in `eui-card-header-left-content` bound to the selection signal set.
24. **Cards use `[euiSelected]`** directive for visual selection state, plus `euiCollapsible` and `euiCollapsed` for expandable content.
25. **Use `EuiAppShellService.isDimmerActive`** via an `effect()` to activate the dimmer when items are selected.
26. **Select-all operates on filtered items only** (not all items).
27. **Inject `EuiAppShellService`** as a **public** property (required for template access to `state$`).

### Content Body Rules

28. **Use `@for` with `track item.id`** for the cards list (Angular 17+ control flow), iterating over `paginatedItems()` (not the full filtered list).
29. **Cards use `eui-card-header` with `hasBottomExpander`** to enable the expand/collapse toggle on the card.
30. **Per-card action dropdown** in `eui-card-header-right-content`, wrapped in a container with `(click)="$event.stopPropagation()"`. The dropdown trigger is a button with a text label (`<span euiLabel>Actions</span>`) and an icon (`eui-ellipsis-vertical` size="s"). Dropdown items are `button[euiDropdownItem]` elements with text labels (no icons inside dropdown items).
31. **Card title** is wrapped in `<a class="eui-u-text-link">` for navigation.
32. **Status chip** in card header uses `euiSizeS` directive with `<span euiLabel>` for status text.
33. **Card content** (`eui-card-content`) contains a grid layout (row/col) for detail fields that displays when expanded.
34. **Always include `eui-paginator`** in `eui-page-column-footer` with `[length]`, `[pageSize]`, `[page]`, `[hasPageNumberNavigation]="true"`, and `(pageChange)` bindings.

### Footer Rules

35. **Page footer is conditional**: `@if (selectedCount() > 0)`.
36. **Footer uses `euiHighlighted`** directive for visual emphasis.
37. **Footer layout** uses a single outer flex container (`eui-u-flex eui-u-flex-gap-m`) with two inner groups:
    - **Left group** (`eui-u-flex eui-u-flex-gap-s`): Reset basic button (`euiButton euiBasicButton`) + selection count text (`span.eui-u-f-bold` for the number).
    - **Right group** (`eui-u-flex eui-u-flex-justify-content-end eui-u-flex-gap-s`): Cancel secondary button (with `eui-close` icon) + Primary action button (with icon) + More actions dropdown (rounded icon button with `euiTooltip`).
38. **Refer to PAGE_FOOTER_PATTERN** Advanced variant for additional guidance on footer conventions.

### Common Rules

39. **Button hierarchy**: primary uses `euiPrimary`, secondary uses `euiSecondary`. Buttons inside columns use `euiSizeS`. Footer "More actions" trigger uses `euiRounded euiIconButton euiBasicButton euiPrimary`.
40. **Export `ModuleComponent`** alias for lazy loading via `loadComponent`.
41. **Use `@if` for conditional rendering** (Angular 17+), not `*ngIf`.
42. **Retrieve all component documentation** from MCP tools (`get_component_docs`) before generating code to ensure correct API usage.
43. **Data is user-provided and agnostic** — define a simple interface with an `id` field and any domain-specific fields. The pattern does not prescribe a fixed data model.
44. **Only import from `@angular/*` and `@eui/*`** packages.

### Accessibility

45. All icon-only buttons must have `aria-label`.
46. Breadcrumb home item must have `ariaLabel="Home"`.
47. Dropdown triggers must have `[attr.aria-label]` or `euiTooltip`.
48. Per-card checkboxes must have dynamic `[attr.aria-label]` describing the item.
49. Select-all checkbox must have a descriptive `aria-label`.
50. Chip list must have an `ariaLabel` describing its purpose.

---

## Key Differences from Other Patterns

| Aspect | Cards Filter (this) | Cards Selection | Cards List Simple |
|--------|---------------------|-----------------|-------------------|
| Filter sidebar | ✅ Collapsible (text + checkboxes + selects) | ❌ None | ❌ None |
| Criteria chips | ✅ Removable at chip-list level with `(remove)` | ❌ None | ❌ None |
| Selectable items | ✅ Per-card checkbox | ✅ Per-card checkbox | ❌ None |
| Collapsible cards | ✅ `euiCollapsible` + `euiCollapsed` + `hasBottomExpander` | ❌ None | ❌ None |
| Card content section | ✅ `eui-card-content` with detail fields | ❌ None | ❌ None |
| Dimmer highlight | ✅ On selection | ✅ On selection | ❌ None |
| Bulk action footer | ✅ Conditional highlighted (PAGE_FOOTER_PATTERN Advanced) | ✅ Conditional highlighted (PAGE_FOOTER_PATTERN Advanced) | ❌ None |
| Column header style | `label` + `[subLabel]` inputs | Manual markup (left/right content) | Manual markup |
| Services | `EuiAppShellService` + `EuiGrowlService` | `EuiAppShellService` + `EuiGrowlService` | `EuiGrowlService` only |
| Filter state | Signals (searchText, statuses, department) | None | None |
| Pagination | ✅ With `hasPageNumberNavigation`, `pageSize`, `page` | Optional | Optional |
| Per-card dropdown style | Button with label text + icon | Icon-only button | N/A |
| Reset filters control | Button (`euiBasicButton euiPrimary euiSizeS`) | N/A | N/A |
| Additional components | `EUI_FIELDSET`, `EUI_INPUT_GROUP`, `EUI_INPUT_TEXT`, `EUI_SELECT`, `EUI_CHIP_LIST` | None | None |
