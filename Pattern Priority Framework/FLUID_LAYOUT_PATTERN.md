---
name: Fluid Layout Pattern -- Canonical Structure Reference
description: Canonical reference for the EUI Fluid Layout design pattern -- a multi-column page layout with a collapsible filters sidebar, a pluggable main content column (cards list or data table) with multi-select and sort/display controls, and an optional resizable detail panel column. Includes dimmer effect on bulk selection, inline preview panel, and growl notifications for user actions.
label: fluid-layout-pattern
category: pattern
applies-to: fluid multi-column page layout with collapsible filters sidebar, pluggable main content (cards list or data table), detail panel, sort/display toggle, and bulk actions
triggered-when: generating a fluid layout page, a master-detail page with inline preview panel, a selectable cards list or data table with filters, or a page requiring multi-select with bulk actions
requires: EUI page components, eui-card, eui-chip, eui-button-group, eui-dropdown, EuiResizableDirective, EuiAppShellService (dimmer), EuiGrowlService (notifications), PAGE_HEADER_PATTERN (eUI Skill), PAGE_FOOTER_PATTERN (eUI Skill)
outputs: a fluid multi-column page following the Fluid Layout pattern with filter sidebar, selectable cards, resizable detail panel, and bulk actions footer
related-skills: SIMPLE_LAYOUT_PATTERN, COLUMNS_LAYOUT_PATTERN, NAVIGATION_LAYOUT_PATTERN, PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN
---

# EUI Fluid Layout Pattern -- Canonical Structure Reference

## Purpose

This document describes the **Fluid Layout** design pattern -- a multi-column page layout used for master-detail scenarios with inline preview. It serves as the canonical reference for AI code generation.

### What is this pattern?

The Fluid Layout pattern represents a **multi-column content page** with nested sub-columns inside a master column, plus an optional resizable detail panel:

- **Master column** -- contains nested sub-columns (filters + main content)
- **Filters sub-column** -- collapsible sidebar with search and filter controls, with a reset link in the column header right content
- **Main content sub-column** -- **pluggable** area that can host a selectable cards list (with sort, display toggle, per-card actions) or a data table (with sortable columns, paginator, row actions, display toggle)
- **Detail panel column** -- resizable from left, appears when an item is selected for preview
- **Page footer** -- bulk action bar that appears when items are selected (with dimmer effect), including a dropdown for additional actions

### Key Differentiator from Columns Layout

Unlike the Columns Layout which has two flat sibling columns, the Fluid Layout uses **nested `eui-page-columns`** inside the master column, creating three distinct zones. The detail panel is conditionally rendered and resizable.

---

## Recommended Usage

Use this pattern when:

- A page needs a master-detail layout with inline preview panel
- Items (cards or table rows) should be selectable with bulk actions
- Filters need a dedicated collapsible sidebar alongside the content
- The main content area needs to display either a cards list or a data table
- A resizable detail/preview panel is needed for quick data inspection
- Sort and display mode (list vs grid) toggling is required (cards list)
- Sortable columns with paginator are needed (data table)
- Multi-select with bulk operations (export, archive, delete, etc.) is needed
- The detail view should open in a side panel without leaving the page
- Actions (view, edit, delete) should provide feedback via growl notifications without external navigation

**Do not use** when:
- A simple two-column layout suffices (use Columns Layout instead)
- No inline preview panel is needed
- No multi-select/bulk actions are required
- A navigation sidebar is the primary left column (use Navigation Layout instead)

---

## ASCII Structure Overview

```
┌───────────────────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                              │
│  ┌────────────────────────────────────────────────────────────────────────────────┐   │
│  │ 1. PAGE BREADCRUMB                                                             │   │
│  │    Home > Current page                                                         │   │
│  └────────────────────────────────────────────────────────────────────────────────┘   │
│  ┌────────────────────────────────────────────────────────────────────────────────┐   │
│  │ eui-page-content > eui-page-columns [hasPreventMobileRendering]                │   │
│  │                                                                                │   │
│  │  ┌──────────────────────────────────────────────────────────┐  ┌─────────────┐ │   │
│  │  │ 2. MASTER COLUMN [hasSubColumns]                         │  │ 5. DETAIL   │ │   │
│  │  │  ┌────────────────────────────────────────────────────┐  │  │    PANEL    │ │   │
│  │  │  │ 2a. PAGE HEADER (inside master)                    │  │  │ (resizable) │ │   │
│  │  │  │     Title / Sub-title                              │  │  │             │ │   │
│  │  │  └────────────────────────────────────────────────────┘  │  │  Item       │ │   │
│  │  │  ┌────────────────────────────────────────────────────┐  │  │  summary    │ │   │
│  │  │  │ eui-page-columns (nested)                          │  │  │  preview    │ │   │
│  │  │  │  ┌─────────────┐  ┌────────────────────────────┐  │  │  │             │ │   │
│  │  │  │  │ 3. FILTERS  │  │ 4. MAIN CONTENT            │  │  │  │  [Delete]   │ │   │
│  │  │  │  │ (collapsible│  │    (PLUGGABLE)              │  │  │  │  [Edit]     │ │   │
│  │  │  │  │  sidebar)   │  │                             │  │  │  │             │ │   │
│  │  │  │  │             │  │  Header: select-all,        │  │  │  └─────────────┘ │   │
│  │  │  │  │  Search     │  │    layout display toggle,   │  │  │                  │   │
│  │  │  │  │  Status     │  │    sort field + direction   │  │  │                  │   │
│  │  │  │  │  Department │  │                             │  │  │                  │   │
│  │  │  │  │  Risk Level │  │  Body:                      │  │  │                  │   │
│  │  │  │  │  [Reset]    │  │    Option A (default):      │  │  │                  │   │
│  │  │  │  │             │  │      Cards list             │  │  │                  │   │
│  │  │  │  │ Header:     │  │    Option B:                │  │  │                  │   │
│  │  │  │  │ [Reset link]│  │      Data table             │  │  │                  │   │
│  │  │  │  └─────────────┘  └────────────────────────────┘  │  │                  │   │
│  │  │  └────────────────────────────────────────────────────┘  │                  │   │
│  │  └──────────────────────────────────────────────────────────┘                  │   │
│  └────────────────────────────────────────────────────────────────────────────────┘   │
│  ┌────────────────────────────────────────────────────────────────────────────────┐   │
│  │ 6. PAGE FOOTER (conditional -- shown when items selected)                      │   │
│  │    [Reset] N selected items          [Cancel] [Export] [More actions dropdown] │   │
│  └────────────────────────────────────────────────────────────────────────────────┘   │
└───────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item` | No | Navigation trail. First item uses `iconSvgName="eui-home"` with `ariaLabel="Home"`. |
| 2 | Master Column | `eui-page-column` [hasSubColumns] | Yes | Container for page header body and nested sub-columns. Uses `hasSubColumns` to enable nested layout. |
| 2a | Page Header | See **PAGE_HEADER_PATTERN** eUI Skill | Yes | Page title and subtitle. Follow the Simple or Advanced variant of the Page Header pattern as appropriate. Retrieve the full pattern from the PAGE_HEADER_PATTERN eUI Skill for structure, rules, and MCP retrieval strategy. |
| 3 | Filters Sub-Column | `eui-page-column` [label, subLabel, euiSize2XL, isCollapsible, isAutocloseOnMobile] | Yes | Collapsible sidebar with search input, select dropdowns, and reset button. The column header includes `eui-page-column-header-right-content` with a "Reset filters" text link. |
| 4 | Main Content Sub-Column | `eui-page-column` [label, subLabel (dynamic), euiHighlighted (dimmer)] | Yes | **Pluggable** main content area. The `eui-page-column-header-body` contains a flex row split into two groups: (1) a **select-all toggle** on the left with a checkbox supporting `checked` and `indeterminate` states plus a label showing "Select all / Unselect all — N selected", and (2) **layout display toggle and sort controls** on the right containing a "Layout display" label, a list/grid `eui-button-group` with `isRadioButtons`, and a sort group with a sort field `select` wrapped in `euiInputGroupAddOn` together with an ascending/descending direction toggle button. The `eui-page-column-body` hosts the pluggable content — either a cards list or a data table. |
| 5 | Detail Panel | `eui-page-column` [euiResizable, euiResizablePosition="left", euiSize4XL] | No | Conditionally rendered resizable panel for previewing selected item. Uses `eui-page-header` with `eui-page-header-action-items` (close button) in the header, a grid of summary fields in the body, and action buttons (Delete, Edit) in the footer. |
| 6 | Page Footer | See **PAGE_FOOTER_PATTERN** eUI Skill | No | Conditional bulk actions bar shown when items are selected. Follow the Advanced (Bulk Actions) variant of the Page Footer pattern. Retrieve the full pattern from the PAGE_FOOTER_PATTERN eUI Skill for structure, rules, and MCP retrieval strategy. Uses dimmer effect via `EuiAppShellService`. Includes a dropdown for additional actions (Archive, Delete). |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── eui-page-breadcrumb
│   └── eui-breadcrumb
│       └── eui-breadcrumb-item (×N)
├── eui-page-content
│   └── eui-page-columns [hasPreventMobileRendering]
│       ├── eui-page-column [hasSubColumns]                         ← MASTER
│       │   ├── eui-page-column-header-body
│       │   │   └── eui-page-header [label][subLabel]
│       │   │       (Simple variant — title + subtitle only)
│       │   └── eui-page-column-body
│       │       └── eui-page-columns (nested)
│       │           ├── eui-page-column [label][subLabel][euiSize2XL][isCollapsible][isAutocloseOnMobile]  ← FILTERS
│       │           │   ├── eui-page-column-header-right-content
│       │           │   │   └── a.eui-u-text-link ("Reset filters")
│       │           │   └── eui-page-column-body
│       │           │       └── div.flex-column
│       │           │           ├── div[euiInputGroup] (search with euiInputGroupAddOn: input + icon button)
│       │           │           ├── div[euiInputGroup] (status select)
│       │           │           ├── div[euiInputGroup] (department select)
│       │           │           ├── div[euiInputGroup] (risk level select)
│       │           │           └── button[euiButton][euiSecondary][euiSizeS] ("Reset all filters")
│       │           └── eui-page-column [label][subLabel][euiHighlighted]  ← MAIN CONTENT (PLUGGABLE)
│       │               ├── eui-page-column-header-body
│       │               │   └── div.flex
│       │               │       ├── div.flex.align-items-center.wrap.gap-s (LEFT: SELECT ALL)
│       │               │       │   └── div.flex.align-items-center
│       │               │       │       ├── input[euiInputCheckBox][checked][indeterminate]
│       │               │       │       └── label[euiLabel] ("Select all / Unselect all — N selected")
│       │               │       └── div.flex.justify-end.align-items-center.wrap.gap-s (RIGHT: CONTROLS)
│       │               │           ├── div.inline-flex (LAYOUT DISPLAY)
│       │               │           │   ├── span.text-small ("Layout display")
│       │               │           │   └── eui-button-group[isRadioButtons]
│       │               │           │       ├── button[euiButton][euiIconButton] id="list" (list-bullets:regular icon)
│       │               │           │       └── button[euiButton][euiIconButton] id="grid" (grid-four:regular icon)
│       │               │           └── div.inline-flex.align-items-center.gap-s (SORT CONTROLS)
│       │               │               └── div[euiInputGroup]
│       │               │                   └── div[euiInputGroupAddOn]
│       │               │                       ├── select[euiSelect] (sort field options)
│       │               │                       └── button[euiButton][euiIconButton][euiPrimary][euiOutline][euiSizeS] (sort direction)
│       │               └── eui-page-column-body
│       │                   └── ⟨⟨ PLUGGABLE CONTENT ⟩⟩
│       │                       Option A: Cards List (div.row > @for + div.col with eui-card)
│       │                       Option B: Data Table (eui-table + paginator)
│       └── @if (selectedContract())                                ← DETAIL PANEL (conditional)
│           └── eui-page-column [euiResizable][euiResizablePosition="left"][euiSize4XL]
│               ├── eui-page-column-header-body
│               │   └── eui-page-header [label][subLabel]
│               │       └── eui-page-header-action-items
│               │           └── button (close icon button)
│               ├── eui-page-column-body
│               │   └── div.row (grid of summary fields using col-md-6)
│               └── eui-page-column-footer
│                   └── div.flex.gap-s.justify-end
│                       ├── button[euiDanger][euiOutline][euiSizeS] (Delete with icon)
│                       └── button[euiPrimary][euiSizeS] (Edit with icon)
└── @if (selectedCount() > 0)                                       ← PAGE FOOTER (conditional)
    └── eui-page-footer [euiHighlighted]
        └── div.flex.justify-between.align-items-center
            ├── div.flex.gap-m.align-items-center (LEFT)
            │   ├── button[euiBasicButton] ("Reset")
            │   └── div ("N selected contract(s)")
            └── div.flex.gap-s (RIGHT)
                ├── button[euiSecondary] (Cancel with close icon)
                ├── button[euiPrimary] (Export with download icon)
                └── eui-dropdown (More actions)
                    ├── button[euiRounded][euiIconButton][euiBasicButton][euiPrimary] (ellipsis icon)
                    └── eui-dropdown-content
                        ├── button[euiDropdownItem] ("Archive selected")
                        └── button[euiDropdownItem] ("Delete selected")
```

---

## MCP EUI Compodoc Tool -- Component Documentation Retrieval

> **IMPORTANT**: This pattern does NOT include inline code samples. Before generating code for this pattern, the AI tool **must** retrieve up-to-date component documentation, inputs, outputs, and examples from the **MCP EUI Compodoc tool**.

### Required Tool Calls

When implementing this pattern, use the following MCP EUI Compodoc tool calls to retrieve component APIs and examples:

#### Page Layout Components

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiPageComponent` | Root page structure, inputs, usage examples |
| `get_component_docs` | `EuiPageContentComponent` | Page content container |
| `get_component_docs` | `EuiPageColumnsComponent` | Multi-column layout container (hasPreventMobileRendering) |
| `get_component_docs` | `EuiPageColumnComponent` | Individual column (hasSubColumns, euiSize, isCollapsible, isAutocloseOnMobile) |

#### Page Header Components

> **Refer to the PAGE_HEADER_PATTERN eUI Skill** for the full component hierarchy, MCP retrieval strategy, and generation rules for the page header. Use the Simple or Advanced variant as appropriate.

#### Page Footer Components

> **Refer to the PAGE_FOOTER_PATTERN eUI Skill** for the full component hierarchy, MCP retrieval strategy, and generation rules for the page footer. Use the Advanced (Bulk Actions) variant for this pattern.

#### Breadcrumb Components

> **Refer to the PAGE_HEADER_PATTERN eUI Skill** for breadcrumb usage, which is part of the Page Header pattern.

#### Card Components (Cards List Content)

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiCardComponent` | Card container (euiSelected) |
| `get_component_docs` | `EuiCardHeaderComponent` | Card header |
| `get_component_inputs` | `EuiCardComponent` | All card inputs for selection state |
| `get_component_examples` | `EuiCardComponent` | Card usage examples |

#### Table Components (Data Table Content)

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiTableComponent` | Data table with sort, filter, paginator bindings |
| `get_component_inputs` | `EuiTableComponent` | Table inputs (data, filter, paginator, isTableResponsive) |
| `get_component_outputs` | `EuiTableComponent` | Table outputs (sortChange, filterChange) |
| `get_component_docs` | `EuiPaginatorComponent` | Paginator (hasPageNumberNavigation, pageSizeOptions, pageSize) |
| `get_component_examples` | `EuiTableComponent` | Table usage examples |

#### UI Components

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiChipComponent` | Status/risk level chips |
| `get_component_docs` | `EuiButtonGroupComponent` | Display mode toggle (isRadioButtons) |
| `get_component_docs` | `EuiDropdownComponent` | Action menus and bulk actions overflow |
| `get_component_docs` | `EuiInputCheckboxComponent` | Select-all and per-item checkboxes (indeterminate) |
| `get_component_docs` | `EuiSelectComponent` | Filter and sort dropdowns |
| `get_component_docs` | `EuiInputTextComponent` | Search text input |
| `get_component_docs` | `EuiBadgeComponent` | Status/risk level badges |

#### Directives

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiResizableDirective` | Detail panel resizable behavior |
| `get_component_docs` | `EuiTooltipDirective` | Icon button tooltips |
| `get_component_docs` | `EuiHighlightedDirective` | Dimmer highlight effect on columns |
| `get_component_docs` | `EuiTemplateDirective` | Table header/body/noData templates |

#### Services (from @eui/core)

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiAppShellService` | Dimmer effect (isDimmerActive) for multi-select |
| `get_component_docs` | `EuiGrowlService` | Growl notifications for actions (view, edit, delete) |

### Retrieval Strategy

1. **Before writing any component code**, call `get_component_docs` for each EUI component used in the pattern.
2. **For inputs/outputs details**, call `get_component_inputs` and `get_component_outputs` on the primary interactive components (EuiCardComponent, EuiTableComponent, EuiPageColumnComponent, EuiPaginatorComponent).
3. **For usage examples**, call `get_component_examples` on the main content components (EuiCardComponent, EuiTableComponent, EuiPageComponent).
4. **Use `search_components`** if you need to find related components by keyword (e.g., search "resizable" to find EuiResizableDirective).
5. **For accessibility requirements**, call `get_component_accessibility` on interactive components (EuiCardComponent, EuiTableComponent, EuiInputCheckboxComponent, EuiDropdownComponent).
6. **For the page header**, follow the MCP Retrieval Strategy in the **PAGE_HEADER_PATTERN eUI Skill** (Simple or Advanced variant).
7. **For the page footer**, follow the MCP Retrieval Strategy in the **PAGE_FOOTER_PATTERN eUI Skill** (Simple or Advanced Bulk Actions variant).

---

## Key Features

### Multi-Select with Dimmer Effect

When items are selected via checkboxes, `EuiAppShellService.isDimmerActive` is set to `true`, which dims the background and highlights the cards column via `[euiHighlighted]`.

**Implementation approach:**
- Retrieve `EuiAppShellService` docs via `get_component_docs("EuiAppShellService")` for the `isDimmerActive` property and `state$` observable.
- Use Angular `signal` for `selectedIds` (a `Set<number>`), `computed` for `selectedCount`, and `effect()` to sync dimmer state.
- Bind `[euiHighlighted]` on the main content column using the async pipe on `appShellService.state$`.

### Resizable Detail Panel

The detail panel uses `EuiResizableDirective` for user-resizable width.

**Implementation approach:**
- Retrieve directive docs via `get_component_docs("EuiResizableDirective")` for available inputs (euiResizablePosition, size constraints).
- Apply `euiResizable` and `euiResizablePosition="left"` on the detail `eui-page-column`.
- The panel header uses `eui-page-header` with `eui-page-header-action-items` containing a close button (icon: `eui-close`).
- The panel body displays item summary fields in a responsive grid (using `row` + `col-md-6` columns).
- The panel footer contains action buttons aligned to the end: a danger outline Delete button with trash icon, and a primary Edit button with edit icon.

### Card Title and Action Growl Notifications

Card title links and edit/delete actions use `EuiGrowlService` to display notifications instead of navigating away.

**Implementation approach:**
- Retrieve service docs via `get_component_docs("EuiGrowlService")` for the `growl()` method signature and severity options.
- Inject the service via `inject(EuiGrowlService)` and call `growl({ severity, summary, detail })`.

### Sort and Display Toggle

Sort by field with ascending/descending toggle, plus list/grid display mode.

**Implementation approach:**
- Use Angular `signal` for `sortField`, `isDescending`, and `displayGrid`.
- Retrieve `EuiButtonGroupComponent` docs via `get_component_docs("EuiButtonGroupComponent")` for the `isRadioButtons` toggle pattern.
- The sort select and direction button are grouped inside an `euiInputGroupAddOn` container.

---

## Main Content Column Header Body Structure

The `eui-page-column-header-body` of the main content sub-column (zone 4) contains a horizontal flex container with two groups. This section describes the structural composition without inline code.

### Left Group: Select All Toggle

A flex row with wrapping and gap, containing:

1. **Checkbox input** — uses the `euiInputCheckBox` directive with bindings for `checked` (bound to `isAllSelected()` computed signal), `indeterminate` (bound to `isIndeterminate()` computed signal), and a `(change)` event calling `toggleSelectAll()`. Must include `aria-label` for accessibility.
2. **Label** — uses `euiLabel` directive, displaying conditional text:
   - Shows "Unselect all" when all visible items are selected
   - Shows "Select all" when not all items are selected
   - Appends " — N selected" showing the current selection count from the `selectedCount()` computed signal

### Right Group: Layout Display and Sort Controls

A flex row with end justification, wrapping, and gap, containing the following elements in order:

#### Layout Display Sub-Group

An inline-flex container with end justification and medium gap, containing:

1. **Layout display label** — an inline-flex container with a `span` element styled as small text displaying "Layout" on one line and "display" on a second line (using a line break)
2. **Display mode toggle** — an inline-flex container with an `eui-button-group` with `isRadioButtons` set to true, emitting a `buttonClick` event with the selected mode ID. Contains two buttons:
   - **List button** — uses `list-bullets:regular` icon, `isChecked` bound to `!displayGrid()`, with `aria-label` "List view" and `euiTooltip` "List view", id="list"
   - **Grid button** — uses `grid-four:regular` icon, `isChecked` bound to `displayGrid()`, with `aria-label` "Grid view" and `euiTooltip` "Grid view", id="grid"

#### Sort Controls Sub-Group

An inline-flex container with center alignment and small gap, containing:

1. **Sort field and direction wrapper** — a fixed-width inline-flex container (`eui-u-width-12`) wrapping an `euiInputGroup` (with no bottom margin) containing an `euiInputGroupAddOn` that groups together:
   - **Sort field dropdown** — a `select` element using `euiSelect` directive with auto width, bound to the `sortField` signal via `ngModel`, with a `euiTooltip` of "Sort by". Options include: Title, Supplier, Status, Department, Risk level, Value, Start date.
   - **Sort direction toggle button** — an icon button using `euiButton euiIconButton euiPrimary euiOutline euiSizeS` directives, toggling between ascending and descending sort. Displays `eui-arrow-down` icon when descending and `eui-arrow-up` icon when ascending. Binds `euiTooltip` dynamically ("Sort ascending" / "Sort descending"). Click calls `toggleSortDirection()`.

### Layout Utility Classes

The outer container uses `eui-u-flex` to create a horizontal row. The left group uses `eui-u-flex eui-u-flex-align-items-center eui-u-flex-wrap eui-u-flex-gap-s`. The right group uses `eui-u-flex eui-u-flex-justify-content-end eui-u-flex-align-items-center eui-u-flex-wrap eui-u-flex-gap-s`.

---

## Filters Sub-Column Structure

The filters sub-column (zone 3) has a specific internal layout:

### Column Header

- **label**: "Filters"
- **subLabel**: "Refine list"
- **Header right content**: A text link ("Reset filters") inside `eui-page-column-header-right-content` that calls `resetFilters()`. Styled with `eui-u-text-link` and small font size.

### Column Body

A flex column container with the following input groups in order:

1. **Search by title or supplier** — `euiInputGroup` with a label, helper text ("Type at least 3 characters"), and an `euiInputGroupAddOn` containing the text input and a search icon button
2. **Status filter** — `euiInputGroup` with a label and a `euiSelect` dropdown. First option is "All statuses", followed by dynamically computed distinct status values
3. **Department filter** — `euiInputGroup` with a label and a `euiSelect` dropdown. First option is "All departments", followed by dynamically computed distinct department values
4. **Risk level filter** — `euiInputGroup` with a label and a `euiSelect` dropdown. First option is "All risk levels", followed by static risk level options (Low, Medium, High)
5. **Reset all filters button** — a secondary small button at the bottom with top margin

### Filter Behavior

- When any filter changes, the current selection is cleared (safety measure to prevent stale selections)
- The search input filters on title and supplier fields (case-insensitive substring match)
- Filters are cumulative (AND logic)

---

## Cards List Content Structure (Option A)

The main content body uses a responsive grid (`row` container) with an `@for` loop rendering each card inside a column div.

### Card Grid Layout

- **Grid mode**: Each card occupies `col-md-6` (two cards per row on medium+ screens)
- **List mode**: Each card occupies `col-12` (one card per row, full width)
- Each column div has bottom margin (`eui-u-mb-m`)

### Individual Card Structure

Each `eui-card` uses `[euiSelected]` bound to the card's selection state. Cards are **flat** (not expandable, no collapsible content).

#### Card Header

- **Left content** (`eui-card-header-left-content`): A centered checkbox input for per-card selection with `aria-label` bound to the item title
- **Title** (`eui-card-header-title`): A text link (`<a>` with `eui-u-text-link` class) that triggers a view growl notification on click
- **Subtitle** (`eui-card-header-subtitle`): Displays key metadata in a single line separated by em dashes (e.g., "Supplier — Department — €Value")
- **Right content** (`eui-card-header-right-content`): A flex row with center alignment and small gap (with click propagation stopped), containing:
  1. **Status chip** — `eui-chip` with `euiSizeS` and conditional severity classes (`euiSuccess`, `euiWarning`, `euiDanger`, `euiInfo`) based on status value
  2. **Actions dropdown** — `eui-dropdown` with a button trigger (primary, outline, small, labeled "Actions" with ellipsis-vertical icon) and dropdown content with View, Edit, Delete buttons
  3. **Panel open button** — a secondary outline icon button with `arrow-line-right:regular` icon, tooltip "View detail", that opens the detail panel

### Empty State

When filtered results yield no items, display a centered text block with light-colored text indicating no matching results.

---

## Detail Panel Structure (Zone 5)

The detail panel is conditionally rendered using `@if` with an alias (`as contract`). It is a **sibling** of the master column.

### Panel Header

Uses `eui-page-column-header-body` containing an `eui-page-header` with:
- `[label]` bound to the item title
- `[subLabel]` bound to a secondary field (e.g., supplier)
- `eui-page-header-action-items` containing a close button (basic button, primary, icon-only with `eui-close` icon, with aria-label and tooltip)

### Panel Body

Uses `eui-page-column-body` containing a responsive grid (`div.row`) with summary fields. Each field occupies `col-md-6` with bottom margin and contains:
- A light-colored label div (field name)
- A bold value div or a chip (for status/risk level fields)

The fields displayed include: Status (chip), Department (text), Risk level (chip), Contract value (formatted number with currency), Start date, End date, Supplier.

### Panel Footer

Uses `eui-page-column-footer` containing a flex row aligned to the end with small gap:
- **Delete button** — danger, outline, small, with trash icon and "Delete" text
- **Edit button** — primary, small, with edit icon and "Edit" text

Both buttons trigger growl notifications.

---

## Bulk Actions Footer Structure (Zone 6)

The page footer is conditionally rendered using `@if (selectedCount() > 0)` and uses `euiHighlighted` on the `eui-page-footer` element.

### Footer Layout

A flex row with space-between alignment containing:

#### Left Side
A flex row with medium gap and center alignment:
1. **Reset button** — a basic button labeled "Reset" that clears the selection
2. **Selection counter** — a div showing "N selected contract(s)" with the count in bold

#### Right Side
A flex row with small gap:
1. **Cancel button** — secondary button with close icon and "Cancel" text, clears the selection
2. **Export button** — primary button with download icon and "Export" text, triggers bulk export action
3. **More actions dropdown** — `eui-dropdown` with:
   - Trigger: rounded icon button (basic, primary) with ellipsis-vertical icon, tooltip "More actions"
   - Content: dropdown items for "Archive selected" and "Delete selected"

---

## Required Angular Imports

> **Do not hardcode import paths.** Retrieve the correct module/token imports by calling `get_component_docs` for each component. The response includes the `imports` field with the proper module tokens.

### Import Tokens to Retrieve

The following EUI tokens are needed for this pattern. Use `get_component_docs` to confirm exact import paths:

| Token | Package | Usage |
|-------|---------|-------|
| `EUI_PAGE` | `@eui/components/eui-page` | Page layout structure |
| `EUI_BREADCRUMB` | `@eui/components/eui-breadcrumb` | Breadcrumb navigation |
| `EUI_CARD` | `@eui/components/eui-card` | Card containers (Cards List content) |
| `EUI_CHIP` | `@eui/components/eui-chip` | Status/risk level chips |
| `EUI_BUTTON` | `@eui/components/eui-button` | Action buttons |
| `EUI_BUTTON_GROUP` | `@eui/components/eui-button-group` | Display mode toggle |
| `EUI_ICON` | `@eui/components/eui-icon` | Icon SVGs |
| `EUI_DROPDOWN` | `@eui/components/eui-dropdown` | Action menus |
| `EUI_INPUT_TEXT` | `@eui/components/eui-input-text` | Search input |
| `EUI_SELECT` | `@eui/components/eui-select` | Filter and sort selects |
| `EUI_INPUT_GROUP` | `@eui/components/eui-input-group` | Form input groups |
| `EUI_LABEL` | `@eui/components/eui-label` | Field labels |
| `EUI_INPUT_CHECKBOX` | `@eui/components/eui-input-checkbox` | Selection checkboxes |
| `EuiResizableDirective` | `@eui/components/directives` | Resizable panel |
| `EuiTooltipDirective` | `@eui/components/directives` | Tooltips |
| `EuiAppShellService` | `@eui/core` | Dimmer effect |
| `EuiGrowlService` | `@eui/core` | Growl notifications |

> **For Page Header imports**: see PAGE_HEADER_PATTERN eUI Skill — "Required Angular Imports" section (Simple or Advanced variant).
> **For Page Footer imports**: see PAGE_FOOTER_PATTERN eUI Skill — "Required Angular Imports" section.

### Additional Imports for Data Table Content

| Token | Package | Usage |
|-------|---------|-------|
| `EUI_TABLE` | `@eui/components/eui-table` | Table component + Sort type |
| `EUI_PAGINATOR` | `@eui/components/eui-paginator` | Paginator component |
| `EUI_BADGE` | `@eui/components/eui-badge` | Status/risk badges |
| `EuiTemplateDirective` | `@eui/components/directives` | Table templates |

### Angular Core Imports

- `ChangeDetectionStrategy`, `Component`, `computed`, `effect`, `inject`, `signal` from `@angular/core`
- `AsyncPipe`, `DecimalPipe` from `@angular/common`
- `FormsModule` from `@angular/forms`

---

## Filter Architecture (Angular Signals)

The component state is managed entirely with Angular signals and computed values:

- **Filter state signals**: `searchText`, `selectedStatus`, `selectedDepartment`, `selectedRiskLevel` (all `signal('')`)
- **Sort state signals**: `sortField` (signal of keyof Contract, default `'title'`), `isDescending` (signal boolean, default `false`)
- **Display mode signal**: `displayGrid` (signal boolean, default `false`)
- **Multi-select state signal**: `selectedIds` (signal of `Set<number>`)
- **Detail panel signal**: `selectedContract` (signal of Contract or null)
- **Derived computed values**:
  - `statusOptions` -- distinct status values from all contracts
  - `departmentOptions` -- distinct department values from all contracts
  - `filteredContracts` -- filtered + sorted data
  - `isAllSelected` -- true when all visible items are selected
  - `isIndeterminate` -- true when some but not all visible items are selected
  - `selectedCount` -- number of selected items
- **Side effect**: `effect()` that syncs `appShellService.isDimmerActive` with `selectedCount() > 0`

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### Pre-Generation Step (MCP Tool Retrieval)

0. **Before writing any code**, call the MCP EUI Compodoc tool to retrieve documentation for all components listed in the "Required Tool Calls" section above. Use the retrieved inputs, outputs, and examples as the authoritative source for component APIs.

### Layout Rules

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Use `eui-page-columns` with `hasPreventMobileRendering`** inside `eui-page-content`.
3. **Master column uses `hasSubColumns`** to enable nested `eui-page-columns` inside its body.
4. **Place the page header inside `eui-page-column-header-body`** of the master column -- follow the **PAGE_HEADER_PATTERN eUI Skill** (Simple or Advanced variant) for the header structure, rules, and required imports.
5. **Nested sub-columns** go inside `eui-page-column-body` of the master column.
6. **Filters sub-column** is the first nested column with `euiSize2XL`, `isCollapsible`, `isAutocloseOnMobile`. It must include `eui-page-column-header-right-content` with a "Reset filters" text link.
7. **Main content sub-column** is the second nested column with dynamic `[subLabel]` showing result count. It is **content-agnostic** and can host a cards list or a data table.
8. **Detail panel is a sibling** of the master column (not nested inside it), conditionally rendered with `@if`.
9. **Detail panel uses `euiResizable`** with `euiResizablePosition="left"` and `euiSize4XL`.
10. **Detail panel header** uses `eui-page-header` with `eui-page-header-action-items` containing a close button.
11. **Detail panel body** uses a responsive grid (`row` + `col-md-6`) for summary fields.
12. **Detail panel footer** contains action buttons (Delete danger outline + Edit primary) aligned to the end.
13. **Page footer is conditional** -- only shown when `selectedCount() > 0`. Uses `euiHighlighted` on the `eui-page-footer` element. Follow the **PAGE_FOOTER_PATTERN eUI Skill** (Advanced Bulk Actions variant) for the footer structure, rules, and required imports.
14. **Page footer includes a dropdown** for additional bulk actions beyond the primary buttons.

### Main Content Rules (Pluggable -- Cards List or Data Table)

The main content sub-column body is **content-agnostic**. Choose the content type based on requirements:

#### Option A: Cards List

15. **Each card uses `eui-card`** with `[euiSelected]` only (cards are flat, not expandable).
16. **Card header left content** contains a centered selection checkbox.
17. **Card header title** contains a clickable text link (`<a>` with `eui-u-text-link`) that triggers a growl notification.
18. **Card header subtitle** shows key metadata separated by em dashes in a single line.
19. **Card header right content** contains a flex row (with stopped click propagation) holding: a status chip, an actions dropdown, and a panel open button.
20. **Actions dropdown** uses a labeled button trigger ("Actions" + ellipsis icon) with View, Edit, Delete options.
21. **Panel open button** is a secondary outline icon button with `arrow-line-right:regular` icon.
22. **Grid mode** uses `col-md-6` class; list mode uses `col-12`.
23. **Empty state** is shown when filtered results are empty — centered light-colored text.

#### Option B: Data Table

15. **Use `eui-table`** with `[data]`, `[paginator]`, `(sortChange)`, `isTableResponsive`.
16. **Wrap table in `div.eui-table__scrollable-wrapper`** for responsive scrolling.
17. **Use `euiTemplate="header"`** for sortable column headers (`isSortable`, `sortOn`).
18. **Use `euiTemplate="body" let-row`** for row rendering with `data-col-label` on each `<td>`.
19. **Include a `euiTemplate="noData"`** template for the empty state.
20. **Use `eui-paginator`** below the table with `hasPageNumberNavigation`, `pageSizeOptions`, `pageSize`.
21. **Row actions** use `eui-dropdown` with `euiDropdownItem` buttons.

#### Content Type Decision Guide

| Criteria | Use Cards List | Use Data Table |
|----------|---------------|----------------|
| Items have rich visual content or descriptions | Yes | No |
| Need list/grid display toggle | Yes | No |
| Need sortable columns with structured data | No | Yes |
| Dense tabular data with many fields | No | Yes |
| Items need expandable detail sections | Yes | No |
| Need per-item checkbox selection | Yes (card-level) | Yes (row-level) |
| Need inline status chips/badges | Both work | Both work |
| Mobile-friendly stacked display | Yes (Preferred) | No |

### Multi-Select Rules

24. **Use a `Set<number>` signal** for tracking selected IDs.
25. **Select-all checkbox** with `[indeterminate]` state support.
26. **Selected count** displayed in the select-all label.
27. **Dimmer effect** activated via `EuiAppShellService.isDimmerActive` using an `effect()`.
28. **Bulk actions footer** appears when items are selected, with Reset, Cancel, primary action buttons, and a dropdown for additional actions.
29. **Clear selection when filters change** — safety measure to avoid stale selections after data changes.

### Sort and Display Rules

30. **Display mode toggle** using `eui-button-group` with `isRadioButtons` for list/grid switching (cards list only; omit for data table). Uses `list-bullets:regular` and `grid-four:regular` icons with `isChecked` bindings.
31. **Sort by field** using a `<select>` inside `euiInputGroupAddOn` with sort options (applies to both cards list and data table content).
32. **Sort direction toggle** button grouped with the sort select inside `euiInputGroupAddOn`, with dynamic icon (`eui-arrow-up` / `eui-arrow-down`).
33. **Grid mode** uses `col-md-6` class; list mode uses `col-12` (cards list only).

### Action Rules

34. **Item title link** triggers a growl notification via `EuiGrowlService` (no external navigation).
35. **Edit action** in the dropdown and detail panel footer also triggers a growl notification.
36. **Delete action** in the dropdown and detail panel footer triggers a warning growl notification.
37. **Panel open button** (or View action in dropdown) sets the selected item signal to show the inline preview panel.
38. **Bulk export** triggers an info growl notification.
39. **Extra bulk actions** (from footer dropdown) trigger info growl notifications.

### Accessibility

40. All icon-only buttons must have `aria-label`.
41. Breadcrumb home item must have `ariaLabel="Home"` (see PAGE_HEADER_PATTERN eUI Skill for full breadcrumb accessibility rules).
42. Checkbox inputs must have `aria-label` (e.g., `'Select ' + item.title` for per-card, `'Select all contracts'` for select-all).
43. Dropdown triggers must have `[attr.aria-label]`.
44. Sort direction button must have `aria-label`.
45. Display mode buttons must have `aria-label` and `euiTooltip`.
46. Close panel button must have `aria-label` and `euiTooltip`.
47. Footer dropdown trigger must have `[attr.aria-label]` and `[euiTooltip]`.
48. Use `euiTooltip` for icon buttons that need text explanation.
49. **Retrieve accessibility docs** via `get_component_accessibility` for each interactive component to ensure compliance.
50. **For page footer accessibility**, follow the accessibility rules in the PAGE_FOOTER_PATTERN eUI Skill.

---

## Related Pattern Documentation (eUI Skills)

This pattern delegates the page header and page footer to their own canonical pattern files, maintained as part of the **eUI Skills** library. When implementing a Fluid Layout, always consult these companion patterns:

| Pattern | eUI Skill Name | Usage in Fluid Layout |
|---------|---------------|----------------------|
| **PAGE_HEADER_PATTERN** | `PAGE_HEADER_PATTERN` (eUI Skill) | Defines the page header structure inside the master column's `eui-page-column-header-body`. Use the **Simple** variant for basic title/subtitle or the **Advanced** variant for collapsible headers with metadata, tags, and action items. |
| **PAGE_FOOTER_PATTERN** | `PAGE_FOOTER_PATTERN` (eUI Skill) | Defines the conditional page footer at the bottom of `eui-page`. Use the **Advanced (Bulk Actions)** variant with `euiHighlighted`, selection counter, and bulk operation buttons. |

### How to Use the Companion Patterns

1. **Page Header**: Retrieve the PAGE_HEADER_PATTERN from the eUI Skills library. Place the header structure inside `eui-page-column-header-body` of the master column (zone 2a). The pattern includes its own MCP retrieval strategy, component hierarchy, generation rules, and accessibility requirements.
2. **Page Footer**: Retrieve the PAGE_FOOTER_PATTERN from the eUI Skills library. Place the footer structure as a direct child of `eui-page`, wrapped in `@if (selectedCount() > 0)`. The pattern includes its own MCP retrieval strategy, flexbox layout rules, generation rules, and accessibility requirements.

---

## Comparison with Other Layout Patterns

| Feature | Simple Layout | Columns Layout | Navigation Layout | **Fluid Layout** |
|---------|--------------|----------------|-------------------|-----------------|
| Columns | 1 | 2 (flat) | 2 (sidebar + main) | 2+ (nested + panel) |
| Nested sub-columns | No | No | No | **Yes** |
| Resizable panel | No | No | No | **Yes** |
| Multi-select | No | Optional | No | **Yes** |
| Dimmer effect | No | No | No | **Yes** |
| Bulk actions footer | No | Optional | No | **Yes** |
| Filter sidebar | No | Yes | No | **Yes** |
| Sidebar navigation | No | No | Yes | No |
| Display mode toggle | No | No | No | **Yes** |
| Detail preview panel | No | No | No | **Yes** |
