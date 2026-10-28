---
name: Table List Pattern
description: Two-column search & results page with collapsible filter sidebar, sortable/selectable paginated data table, per-row actions, filter criteria chips, inline search, and conditional highlighted page footer with bulk actions.
label: table-list-pattern
category: pattern
applies-to: table list pages with filter sidebar, sortable/selectable table, per-row and bulk actions
triggered-when: generating a table list page, a data table with filters, or a searchable paginated list with row selection and bulk operations
requires: eUI page components, eui-table, eui-paginator, eui-fieldset, eui-chip-list, EuiAppShellService, AsyncPipe, FormsModule
outputs: a two-column table list page with selectable rows, dimmer highlight, and conditional page footer bulk actions
related-skills: PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN, COLUMNS_LAYOUT_PATTERN, CARDS_LIST_SIMPLE_PATTERN, CARDS_SELECTION_PATTERN, CARDS_FILTER_PATTERN
---

# EUI Table List Pattern

## Purpose

Two-column search & results page: collapsible filter sidebar on the left, paginated data table on the right. Used when a user needs to browse, search, filter, sort, and act upon large datasets.

---

## Recommended Usage

Use this pattern when:

- Displaying tabular data with sorting and pagination
- Filter sidebar with text search, quick filters, and advanced filters is required
- Row selection with bulk actions is needed
- Per-row inline actions (edit, delete, more) are needed

---

## Related Patterns

This pattern composes two sub-patterns that must be applied:

| Sub-Pattern | File | Usage in this pattern |
|-------------|------|-----------------------|
| **PAGE_HEADER_PATTERN** | `PAGE_HEADER_PATTERN.md` | Simple variant — breadcrumb + title + subtitle + action buttons + overflow dropdown |
| **PAGE_FOOTER_PATTERN** | `PAGE_FOOTER_PATTERN.md` | Advanced variant (Bulk Actions) — conditional highlighted footer with selection counter and batch actions |

Refer to those files for the full canonical structure, zone descriptions, component hierarchy, and generation rules of the header and footer.

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 1. PAGE HEADER (see PAGE_HEADER_PATTERN — Simple variant)         │  │
│  │    Breadcrumb + Title + Subtitle + Action buttons + Overflow      │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ eui-page-content > eui-page-columns                               │  │
│  │  ┌──────────────────────┐  ┌──────────────────────────────────┐   │  │
│  │  │ 2. FILTER COLUMN     │  │ 3. RESULT COLUMN                 │   │  │
│  │  │  (collapsible)       │  │    Title + N results found       │   │  │
│  │  │  [Search btn]        │  │    [euiHighlighted] on selection │   │  │
│  │  │  ┌────────────────┐  │  │                                  │   │  │
│  │  │  │ Text search    │  │  ├──────────────────────────────────┤   │  │
│  │  │  │ + helper text  │  │  │ 4. FILTER CRITERIA CHIPS         │   │  │
│  │  │  │ + search icon  │  │  │    Selected: [chip×] Clear all   │   │  │
│  │  │  └────────────────┘  │  ├──────────────────────────────────┤   │  │
│  │  │  ┌────────────────┐  │  │ 5. COLUMN ACTIONS                │   │  │
│  │  │  │ Quick Filters  │  │  │    [Refresh] [Add] [Table filter]│   │  │
│  │  │  │ (expandable)   │  │  ├──────────────────────────────────┤   │  │
│  │  │  │ ☑ Status 1     │  │  │ 6. DATA TABLE                    │   │  │
│  │  │  │ ☑ Status 2     │  │  │    (sortable, selectable)        │   │  │
│  │  │  │ [Dept ▼]       │  │  │    Per-row: [✎] [🗑] [⋮]        │   │  │
│  │  │  └────────────────┘  │  │    No-data template              │   │  │
│  │  │  ┌────────────────┐  │  ├──────────────────────────────────┤   │  │
│  │  │  │ Advanced       │  │  │ 7. PAGINATOR                     │   │  │
│  │  │  │ (collapsed)    │  │  │    (with page numbers)           │   │  │
│  │  │  │ [Type ▼]       │  │  │                                  │   │  │
│  │  │  └────────────────┘  │  │                                  │   │  │
│  │  └──────────────────────┘  └──────────────────────────────────┘   │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 8. PAGE FOOTER (see PAGE_FOOTER_PATTERN — Advanced variant)       │  │
│  │    @if selectedRows.length > 0                                    │  │
│  │    [Reset] N selected     [Cancel] [Primary action] [▼ More]      │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Header | See **PAGE_HEADER_PATTERN** (Simple variant) | Yes | Breadcrumb with home icon + navigation trail. Page title with `label` and `subLabel`. Action items: secondary button (Export), primary button (New), overflow dropdown with icon trigger (`eui-chevron-down`) containing additional actions. |
| 2 | Filter Column | `eui-page-column` [label, euiSize3XL, isCollapsible, isAutocloseOnMobile] | Yes | Left sidebar with: header right content containing a "Search" button (`euiButton euiBasicButton euiPrimary euiSizeS`). Body contains a flex-column layout with text search (label + helper text + input-group-addon with text input and icon button), quick filters fieldset (expanded, with status checkboxes in flex-wrap layout and a department select), and advanced filters fieldset (collapsed, with a type select). |
| 3 | Result Column | `eui-page-column` [euiHighlighted] | Yes | Binds `[euiHighlighted]` to `(appShellService.state$ | async)?.isDimmerActive`. Header left content shows title (bold) and a result count with dynamic number. |
| 4 | Filter Criteria Chips | `eui-page-column-header-body` | Conditional | Shown when active filters exist (`@if`). Contains a flex row with "Selected criteria:" text + "Clear all" text link + `eui-chip-list` with `isChipsRemovable` and `euiSizeS`. Chips rendered via `@for` loop. |
| 5 | Column Actions | `eui-page-column-header-right-content` | No | Flex container with action buttons (secondary S, primary S) and an `eui-table-filter` bound to the table via template reference. |
| 6 | Data Table | `eui-page-column-body` | Yes | Scrollable wrapper containing `eui-table` with `isTableResponsive`, `[data]`, `[filter]`, `[paginator]`, `(rowsSelect)`, `(sortChange)`. Header template: selectable row with sortable columns + Actions column. Body template: selectable data rows with cells (badge for ID, text link for title, status chip with conditional color directives, number pipe for currency), and per-row actions cell (edit icon button, delete icon button, overflow dropdown). Includes a no-data template with colspan message. |
| 7 | Paginator | `eui-page-column-footer` > `eui-paginator` | Yes | Paginator with `[length]`, `[pageSize]`, `[pageSizeOptions]`, and `[hasPageNumberNavigation]="true"`. |
| 8 | Page Footer | See **PAGE_FOOTER_PATTERN** (Advanced variant) | Conditional | `@if (selectedRows.length > 0)`. Uses `euiHighlighted`. Outer flex with justify-between and align-center. Left group: Reset basic button + "N selected contract(s)" text (bold number). Right group: Cancel secondary button (with close icon) + Primary action button (with download icon) + More actions dropdown (rounded icon button with tooltip). |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── [PAGE HEADER — See PAGE_HEADER_PATTERN Simple variant]
│   ├── eui-page-breadcrumb > eui-breadcrumb > eui-breadcrumb-item (×N)
│   │   ├── item: iconSvgName="eui-home", link="/", ariaLabel="Home"
│   │   └── item: label (current page)
│   ├── eui-page-header [label][subLabel]
│   │   └── eui-page-header-action-items
│   │       ├── button[euiButton][euiSecondary] → "Export"
│   │       ├── button[euiButton][euiPrimary] → "New item"
│   │       └── eui-dropdown (overflow)
│   │           ├── button[euiButton][euiPrimary][euiOutline][euiTooltip][attr.aria-label]
│   │           │   ├── text label → "Other actions"
│   │           │   └── eui-icon-svg [icon="eui-chevron-down"]
│   │           └── eui-dropdown-content
│   │               └── button[euiDropdownItem][aria-label](click) (×N)
├── eui-page-content
│   └── eui-page-columns [hasPreventMobileRendering]
│       ├── eui-page-column [label][euiSize3XL][isCollapsible][isAutocloseOnMobile]  ← FILTER
│       │   ├── eui-page-column-header-right-content
│       │   │   └── button[euiButton][euiBasicButton][euiPrimary][euiSizeS] → "Search"
│       │   └── eui-page-column-body
│       │       └── div.eui-u-flex.eui-u-flex-column
│       │           ├── div[euiInputGroup]  ← Text search
│       │           │   ├── label[euiLabel][for]
│       │           │   ├── div.eui-u-f-s.eui-u-mb-2xs (helper text)
│       │           │   └── div[euiInputGroupAddOn]
│       │           │       ├── input[euiInputText][id][placeholder]
│       │           │       └── button[euiButton][euiIconButton][euiPrimary][euiOutline][aria-label]
│       │           │           └── eui-icon-svg [icon="eui-search"]
│       │           ├── eui-fieldset [label][isLarge][isExpandable]  ← Quick filters
│       │           │   ├── div[euiInputGroup] (Status checkboxes)
│       │           │   │   ├── label[euiLabel] → "Status"
│       │           │   │   └── div.eui-u-flex.eui-u-flex-wrap.eui-u-flex-gap-s
│       │           │   │       └── (×N) div.eui-u-inline-flex
│       │           │   │           ├── input[euiInputCheckBox][id][(ngModel)]
│       │           │   │           └── label[euiLabel][for]
│       │           │   └── div[euiInputGroup] (Department select)
│       │           │       ├── label[euiLabel][for]
│       │           │       └── select[euiSelect][id][(ngModel)]
│       │           │           ├── option[value=""] (default "All" option)
│       │           │           └── option (×N)
│       │           └── eui-fieldset [label][isLarge][isExpandable][isExpanded=false]  ← Advanced
│       │               └── div.eui-u-flex.eui-u-flex-column.eui-u-mt-m
│       │                   └── div[euiInputGroup]
│       │                       ├── label[euiLabel][for]
│       │                       └── select[euiSelect][id][(ngModel)]
│       │                           ├── option[value=""] (default "All" option)
│       │                           └── option (×N)
│       └── eui-page-column [euiHighlighted]  ← RESULTS
│           ├── eui-page-column-header-left-content
│           │   ├── div.eui-u-f-l → Title text
│           │   └── div → strong "N" + "results found"
│           ├── @if (activeFilters.length > 0)
│           │   └── eui-page-column-header-body  ← Criteria chips
│           │       └── div.eui-u-flex.eui-u-flex-gap-m.eui-u-flex-align-items-center
│           │           ├── div.eui-u-f-s → "Selected criteria:" + a.eui-u-text-link "Clear all"
│           │           └── eui-chip-list [isChipsRemovable][euiSizeS][ariaLabel](chipRemoved)
│           │               └── @for (filter of activeFilters; track filter)
│           │                   └── eui-chip → filter text
│           ├── eui-page-column-header-right-content
│           │   └── div.eui-u-flex.eui-u-flex-align-items-center.eui-u-flex-gap-s
│           │       ├── button[euiButton][euiSecondary][euiSizeS] → "Refresh"
│           │       ├── button[euiButton][euiPrimary][euiSizeS] → "Add item"
│           │       └── eui-table-filter #filter [placeholder](filterChange)
│           ├── eui-page-column-body
│           │   └── div.eui-table__scrollable-wrapper
│           │       └── table[euiTable][isTableResponsive][data][filter][paginator](rowsSelect)(sortChange)
│           │           ├── ng-template[euiTemplate="header"]
│           │           │   └── tr[isHeaderSelectable="true"]
│           │           │       ├── th[isSortable][sortOn] (×N data columns)
│           │           │       └── th.eui-u-text-center → "Actions"
│           │           ├── ng-template[let-row][euiTemplate="body"]
│           │           │   └── tr[isDataSelectable]
│           │           │       ├── td[data-col-label] → span[euiBadge] (ID badge)
│           │           │       ├── td[data-col-label] → a.eui-u-text-link[euiTooltip] (title link)
│           │           │       ├── td[data-col-label] (×N plain text cells)
│           │           │       ├── td[data-col-label] → eui-chip[status directives][euiSizeS] (status)
│           │           │       ├── td[data-col-label] → value with number pipe + currency symbol
│           │           │       └── td[data-col-label="Actions"]
│           │           │           └── div.eui-u-flex.eui-u-flex-justify-content-center.eui-u-flex-gap-2xs
│           │           │               ├── button[euiButton][euiBasicButton][euiRounded][euiIconButton][euiPrimary][euiTooltip][aria-label]
│           │           │               │   └── eui-icon-svg [icon="eui-edit"][fillColor="primary"]
│           │           │               ├── button[euiButton][euiBasicButton][euiRounded][euiIconButton][euiDanger][euiTooltip][aria-label]
│           │           │               │   └── eui-icon-svg [icon="eui-trash"][fillColor="danger"]
│           │           │               └── eui-dropdown
│           │           │                   ├── button[euiButton][euiIconButton][euiBasicButton][euiRounded][euiPrimary][attr.aria-label]
│           │           │                   │   └── eui-icon-svg [icon="eui-ellipsis-vertical"][size="s"]
│           │           │                   └── eui-dropdown-content
│           │           │                       └── button[euiDropdownItem][aria-label](click) (×N)
│           │           └── ng-template[euiTemplate="noData"]
│           │               └── tr > td[colspan].eui-u-text-center → no-data message
│           └── eui-page-column-footer
│               └── eui-paginator #paginator [length][pageSize][pageSizeOptions][hasPageNumberNavigation]
└── [PAGE FOOTER — See PAGE_FOOTER_PATTERN Advanced variant]
    └── @if (selectedRows.length > 0)
        └── eui-page-footer [euiHighlighted]
            └── div.eui-u-flex.eui-u-flex-justify-content-between.eui-u-flex-align-items-center
                ├── div.eui-u-flex.eui-u-flex-gap-m.eui-u-flex-align-items-center  ← Left group
                │   ├── button[euiButton][euiBasicButton] → "Reset"
                │   └── div → span.eui-u-f-bold "N" + "selected item(s)"
                └── div.eui-u-display-flex.eui-u-flex-gap-s.eui-u-ml-auto  ← Right group
                    ├── button[euiButton][euiSecondary][aria-label]
                    │   ├── eui-icon-svg [icon="eui-close"][size="s"]
                    │   └── "Cancel"
                    ├── button[euiButton][euiPrimary][aria-label]
                    │   ├── eui-icon-svg [icon="eui-download"][size="s"]
                    │   └── "Export selected" (primary bulk action label)
                    └── eui-dropdown
                        ├── button[euiButton][euiRounded][euiIconButton][euiBasicButton][euiPrimary][attr.aria-label][euiTooltip]
                        │   └── eui-icon-svg [icon="eui-ellipsis-vertical"][size="s"]
                        └── eui-dropdown-content
                            └── button[euiDropdownItem][aria-label](click) (×N)
```

---

## Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-home` | `eui-breadcrumb-item` | Breadcrumb home item (`iconSvgName`) |
| `eui-chevron-down` | `eui-icon-svg` | Overflow dropdown trigger in page header actions |
| `eui-search` | `eui-icon-svg` | Text search button in filter column |
| `eui-edit` | `eui-icon-svg` | Per-row edit action button (`fillColor="primary"`) |
| `eui-trash` | `eui-icon-svg` | Per-row delete action button (`fillColor="danger"`) |
| `eui-ellipsis-vertical` | `eui-icon-svg` | Per-row overflow dropdown + Footer "More actions" (size="s") |
| `eui-close` | `eui-icon-svg` | Cancel button icon in footer (size="s") |
| `eui-download` | `eui-icon-svg` | Primary bulk action icon in footer (size="s") |

---

## MCP Retrieval Strategy

All component APIs, inputs, outputs, and usage examples must be retrieved from the **eUI MCP Compodoc** tool before generating code. Do NOT rely on inline code samples.

### Table & Pagination Components

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiTableComponent` | Table: `[data]`, `[filter]`, `[paginator]`, `[isTableResponsive]`, `(rowsSelect)`, `(sortChange)`, `[isHeaderSelectable]`, `[isDataSelectable]` |
| `get_component_docs` | `EuiPaginatorComponent` | Paginator: `[length]`, `[pageSize]`, `[pageSizeOptions]`, `[hasPageNumberNavigation]`, `(pageChange)` |
| `get_component_docs` | `EuiTableFilterComponent` | Inline table filter: `placeholder`, `(filterChange)` |

### Filter Column Components

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageColumnComponent` | Collapsible column: `label`, `isCollapsible`, `isAutocloseOnMobile`, `euiSize3XL`, `[euiHighlighted]` |
| `get_component_docs` | `EuiFieldsetComponent` | Expandable filter sections: `label`, `isExpandable`, `isExpanded`, `isLarge` |
| `get_component_docs` | `EuiChipListComponent` | Filter criteria chips: `ariaLabel`, `isChipsRemovable`, `euiSizeS`, `(chipRemoved)` |
| `get_component_docs` | `EuiChipComponent` | Individual chips in chip list and status chips in table rows |

### Page Structure Components

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageHeaderComponent` | Page header: `label`, `subLabel` — follow PAGE_HEADER_PATTERN |
| `get_component_docs` | `EuiPageFooterComponent` | Page footer: `euiHighlighted` — follow PAGE_FOOTER_PATTERN |
| `get_component_docs` | `EuiDropdownComponent` | Overflow actions menu: per-row, page-level, and footer bulk actions |
| `get_component_docs` | `EuiBreadcrumbComponent` | Navigation breadcrumb trail |
| `get_component_docs` | `EuiBreadcrumbItemComponent` | Breadcrumb items: `link`, `label`, `iconSvgName`, `ariaLabel` |

### Services

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiAppShellService` | Dimmer state management: `isDimmerActive`, `state$` |
| `get_component_docs` | `EuiGrowlService` | Toast notifications for action feedback |

---

## Required Angular Import Tokens

Retrieve full import paths via MCP `get_component_docs` for each component. The following tokens must be spread in the component `imports` array:

- `AsyncPipe` from `@angular/common`
- `DecimalPipe` from `@angular/common`
- `FormsModule` from `@angular/forms`
- `EuiTooltipDirective` from `@eui/components/directives`
- `EUI_PAGE` from `@eui/components/eui-page`
- `EUI_BREADCRUMB` from `@eui/components/eui-breadcrumb`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EUI_TABLE` from `@eui/components/eui-table`
- `EUI_PAGINATOR` from `@eui/components/eui-paginator`
- `EUI_ICON` from `@eui/components/eui-icon`
- `EUI_DROPDOWN` from `@eui/components/eui-dropdown`
- `EUI_BADGE` from `@eui/components/eui-badge`
- `EUI_CHIP` from `@eui/components/eui-chip`
- `EUI_CHIP_LIST` from `@eui/components/eui-chip-list`
- `EUI_FIELDSET` from `@eui/components/eui-fieldset`
- `EUI_INPUT_CHECKBOX` from `@eui/components/eui-input-checkbox`
- `EUI_SELECT` from `@eui/components/eui-select`
- `EUI_LABEL` from `@eui/components/eui-label`
- `EUI_INPUT_GROUP` from `@eui/components/eui-input-group`
- `EUI_INPUT_TEXT` from `@eui/components/eui-input-text`

Services (injected via `inject()`):
- `EuiAppShellService` from `@eui/core`
- `EuiGrowlService` from `@eui/core`

---

## Status Chip Mapping

| Status Value | Directive | Visual |
|-------------|-----------|--------|
| Active | `[euiSuccess]` | Green chip |
| Under Review | `[euiWarning]` | Orange/amber chip |
| Expired | `[euiDanger]` | Red chip |
| Draft | `[euiInfo]` | Blue chip |

Status chips use conditional binding: `[euiSuccess]="row.status === 'Active'"` pattern with `euiSizeS` for compact display.

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### Layout Rules

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: header (per PAGE_HEADER_PATTERN) → page-content (columns) → conditional footer (per PAGE_FOOTER_PATTERN).
3. **Use `eui-page-columns` with `hasPreventMobileRendering`** inside `eui-page-content`.
4. **Apply the PAGE_HEADER_PATTERN** (Simple variant) for breadcrumb, title, subtitle, and action items (secondary + primary buttons + overflow dropdown with chevron-down icon trigger and text label).
5. **Apply the PAGE_FOOTER_PATTERN** (Advanced variant) for the conditional highlighted footer with bulk actions.

### Filter Column Rules (Left)

6. **Filter column is always the first `eui-page-column`** with a descriptive `label`, `euiSize3XL`, `isCollapsible`, and `isAutocloseOnMobile`.
7. **Header right content** contains a single "Search" button (`euiButton euiBasicButton euiPrimary euiSizeS`).
8. **Body is wrapped in a single flex-column div** containing all filter sections.
9. **Text search** uses `div[euiInputGroup]` with a `label[euiLabel]`, a helper text div (`eui-u-f-s eui-u-mb-2xs`), and a `div[euiInputGroupAddOn]` containing `input[euiInputText]` (with placeholder) and a search icon button.
10. **Quick filters** use `eui-fieldset` with `isExpandable` and `isLarge` (expanded by default). Contains multiple `div[euiInputGroup]` blocks: one for status checkboxes (flex-wrap layout, each checkbox in `div.eui-u-inline-flex` with `input[euiInputCheckBox][(ngModel)]` + `label[euiLabel]`) and one for a category select.
11. **Advanced filters** use `eui-fieldset` with `isExpandable`, `isLarge`, and `[isExpanded]="false"` (collapsed by default). Contains selects wrapped in a flex-column div with top margin.
12. **Use `FormsModule` with `[(ngModel)]`** for all filter inputs (two-way binding).

### Result Column Rules (Right)

13. **Result column is the second `eui-page-column`** with `[euiHighlighted]` bound to `(appShellService.state$ | async)?.isDimmerActive`.
14. **Header left content** contains a title in `div.eui-u-f-l` and a result count div with `strong` for the number.
15. **Filter criteria chips** are conditionally shown (`@if`) in `eui-page-column-header-body`. Layout: flex container with "Selected criteria:" text + "Clear all" link (`a.eui-u-text-link`) + `eui-chip-list[isChipsRemovable][euiSizeS][ariaLabel]` with `(chipRemoved)` event. Chips rendered via `@for` loop.
16. **Header right content** contains a flex container with action buttons (`euiSecondary euiSizeS`, `euiPrimary euiSizeS`) and an `eui-table-filter` with template reference variable and placeholder.

### Table Rules

17. **Table is wrapped in `div.eui-table__scrollable-wrapper`** inside `eui-page-column-body`.
18. **Table element** uses `euiTable`, `isTableResponsive`, `[data]`, `[filter]` (bound to table-filter ref), `[paginator]` (bound to paginator ref), `(rowsSelect)`, and `(sortChange)`.
19. **Header template** (`euiTemplate="header"`) contains a single `tr[isHeaderSelectable="true"]` with `th[isSortable][sortOn]` for each sortable data column and a final `th` for "Actions" (centered via `eui-u-text-center`).
20. **Body template** (`euiTemplate="body"` with `let-row`) contains a `tr[isDataSelectable]` with:
    - Data cells using `td[data-col-label]` for responsive labeling
    - ID cell: `span[euiBadge]` for visual distinction
    - Title cell: `a.eui-u-text-link[euiTooltip]` for navigation
    - Status cell: `eui-chip` with conditional status directives (`[euiSuccess]`, `[euiWarning]`, `[euiDanger]`, `[euiInfo]`) and `euiSizeS`
    - Value cell: number pipe with currency/unit suffix
    - Actions cell: flex container (centered, gap-2xs) with edit icon button (`euiBasicButton euiRounded euiIconButton euiPrimary`), delete icon button (`euiBasicButton euiRounded euiIconButton euiDanger`), and overflow dropdown
21. **No-data template** (`euiTemplate="noData"`) contains a single row with a centered `td[colspan]` spanning all columns.
22. **Per-row action buttons** use `euiBasicButton euiRounded euiIconButton` with the appropriate color directive. Edit uses `eui-edit` icon with `fillColor="primary"`. Delete uses `eui-trash` icon with `fillColor="danger"`.
23. **Per-row overflow dropdown** trigger uses `euiButton euiIconButton euiBasicButton euiRounded euiPrimary` with dynamic `[attr.aria-label]` referencing the row item.

### Paginator Rules

24. **Paginator** is placed in `eui-page-column-footer` with a template reference variable.
25. **Paginator inputs**: `[length]` (data source length), `[pageSize]`, `[pageSizeOptions]` (array), and `[hasPageNumberNavigation]="true"`.

### Footer Rules (Bulk Actions)

26. **Page footer is conditional**: `@if (selectedRows.length > 0)`.
27. **Footer uses `euiHighlighted`** directive for visual emphasis.
28. **Footer outer layout** uses `eui-u-flex eui-u-flex-justify-content-between eui-u-flex-align-items-center`.
29. **Left group** (`eui-u-flex eui-u-flex-gap-m eui-u-flex-align-items-center`): Reset button (`euiButton euiBasicButton`) + selection count div with bold number.
30. **Right group** (`eui-u-display-flex eui-u-flex-gap-s eui-u-ml-auto`): Cancel button (`euiSecondary` with `eui-close` icon size "s") + Primary bulk action button (`euiPrimary` with `eui-download` icon size "s") + overflow dropdown (`euiRounded euiIconButton euiBasicButton euiPrimary` with `euiTooltip`).
31. **Refer to PAGE_FOOTER_PATTERN** Advanced variant for additional guidance on footer conventions.

### Component Configuration Rules

32. **Use `ChangeDetectionStrategy.OnPush`** on the component.
33. **Inject `EuiAppShellService`** as a **public** property (required for template access to `state$`).
34. **Inject `EuiGrowlService`** as private for action feedback.
35. **Use `viewChild`** for table and paginator template references.
36. **Spread EUI token arrays** in the component `imports`.
37. **Use `@for` control flow** (Angular 17+) for any iterable rendering (chips, table rows).
38. **Use `@if` control flow** for conditional rendering (chips section, footer).
39. **All data models and mock data are user-defined** — this pattern is data-agnostic.

### Accessibility Rules

40. All icon-only buttons must have `aria-label` and `euiTooltip`.
41. Breadcrumb home item must have `ariaLabel="Home"`.
42. Table header cells with sorting must use `isSortable` with `sortOn` for proper keyboard interaction.
43. Each dropdown action item must have `aria-label`.
44. Per-row overflow dropdown trigger must have dynamic `[attr.aria-label]` referencing the row item name.
45. The chip list must have an `ariaLabel` describing its purpose.
46. Page-level overflow dropdown trigger must have `[attr.aria-label]` and `euiTooltip`.

---

## Key Features Summary

| Feature | Implementation |
|---------|---------------|
| Collapsible filter sidebar | `eui-page-column` with `isCollapsible`, `isAutocloseOnMobile`, and `euiSize3XL` |
| Text search with helper text | `euiInputGroup` + `euiInputText` + helper text div + icon search button |
| Quick filters (expanded) | `eui-fieldset[isExpandable][isLarge]` with checkboxes (ngModel) and selects |
| Advanced filters (collapsed) | `eui-fieldset[isExpandable][isLarge][isExpanded=false]` with selects |
| Active filter criteria chips | `eui-chip-list[isChipsRemovable][euiSizeS]` with `(chipRemoved)` + "Clear all" link |
| Sortable columns | `th[isSortable][sortOn="propertyName"]` with `(sortChange)` on table |
| Row selection | `[isHeaderSelectable]="true"` + `[isDataSelectable]` on body rows |
| Inline table filter | `eui-table-filter` bound to table via `[filter]` template ref |
| Pagination with page numbers | `eui-paginator[length][pageSize][pageSizeOptions][hasPageNumberNavigation]` |
| ID badge display | `span[euiBadge]` in ID column cell |
| Title as clickable link | `a.eui-u-text-link[euiTooltip]` in title column cell |
| Status color chips | `eui-chip` with conditional `[euiSuccess]`/`[euiWarning]`/`[euiDanger]`/`[euiInfo]` |
| Per-row actions | Rounded icon buttons (edit, delete) + overflow `eui-dropdown` |
| No-data template | `euiTemplate="noData"` with centered colspan message |
| Dimmer on selection | `[euiHighlighted]="(appShellService.state$ | async)?.isDimmerActive"` |
| Conditional bulk footer | `@if (selectedRows.length > 0)` + `eui-page-footer[euiHighlighted]` |
| Footer layout | Justify-between with left group (reset + count) and right group (cancel + action + overflow) |
| Action feedback | `EuiGrowlService` for toast notifications |
| Page header overflow | Dropdown with text label + chevron-down icon trigger |
| Scrollable table wrapper | `div.eui-table__scrollable-wrapper` around the table |
