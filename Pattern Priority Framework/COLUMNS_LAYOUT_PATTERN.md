---
name: Columns Layout Pattern — Canonical Structure Reference
description: Canonical reference for the EUI Columns Layout design pattern — a two-column page layout with a collapsible left sidebar (filters, navigation, summary) and a pluggable main right content area (data tables, cards lists, detail views, forms). Includes page header with actions, page footer, and full generation rules.
label: columns-layout-pattern
category: pattern
applies-to: two-column page layout with collapsible sidebar and pluggable right column content (table, cards list, forms, detail views)
triggered-when: generating a columns layout page, a page with a filter sidebar, or a master-detail layout with two content zones
requires: eUI page components (base), plus content-specific components depending on right column content type
outputs: a two-column page following the Columns Layout pattern with page header actions, pluggable column content, and page footer
related-skills: SIMPLE_LAYOUT_PATTERN, FLUID_LAYOUT_PATTERN, PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN
---

# EUI Columns Layout Pattern — Canonical Structure Reference

## Purpose

This document describes the **Columns Layout** design pattern — a multi-column page layout used across EUI-based applications. It serves as the canonical reference for AI code generation.

### What is this pattern?

The Columns Layout pattern represents a **two-column content page** wrapped inside the standard EUI page scaffolding (breadcrumb, page header with actions, content, footer). The left column is collapsible and auto-closes on mobile; the right column is the main **pluggable content area** that can host any type of content:

- **Data table** — sortable, filterable, paginated tabular data
- **Cards list** — selectable card grid with actions
- **Detail view** — rich content display
- **Forms** — data entry with validation
- **Any custom content** — dashboards, charts, lists, etc.

### Left Column — Pluggable Sidebar Content

The left column is a **collapsible sidebar** that can host various pluggable content types:

- **Search filters** — text search input and select dropdowns for filtering the right column data
- **Collapsible navigation** — sidebar menu with expandable sections
- **Summary panel** — key metrics, counts, or overview information
- **Category tree** — hierarchical navigation or taxonomy browser
- **Any custom sidebar content** — legends, contextual help, quick links, etc.

---

## Recommended Usage

Use this pattern when:

- A page needs a sidebar (filters, navigation, summary) alongside a main content area
- A master-detail layout is required (list on left, detail on right)
- Sidebar navigation is needed alongside a content area
- The right column content can be a table, cards list, form, or any other component
- Filters should be collapsible and auto-close on mobile
- The page needs top-level header actions
- A page footer with global actions is required
- Two distinct content zones need to be displayed side-by-side

**Do not use** when:
- A simple single-column layout suffices (use Simple Layout instead)
- No sidebar/secondary content zone is needed
- A fluid multi-column layout with nested sub-columns and a resizable detail panel is needed (use Fluid Layout instead)

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 1–3. PAGE HEADER                                                  │  │
│  │    (See PAGE_HEADER_PATTERN eUI Skill for Simple or Advanced variants)   │  │
│  │    Breadcrumb, Title / Sub-title, Actions, optional Body          │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ eui-page-content > eui-page-columns                               │  │
│  │  ┌──────────────────────┐  ┌──────────────────────────────────┐   │  │
│  │  │ 4. LEFT COLUMN       │  │ 5. RIGHT COLUMN                  │   │  │
│  │  │    Collapsible       │  │    << PLUGGABLE CONTENT >>       │   │  │
│  │  │    sidebar           │  │                                  │   │  │
│  │  ├──────────────────────┤  │  Any content: tables, cards,     │   │  │
│  │  │  << PLUGGABLE >>     │  │  forms, lists, dashboards,       │   │  │
│  │  │  Filters, navigation,│  │  custom components, etc.         │   │  │
│  │  │  summary, category   │  │                                  │   │  │
│  │  │  tree, etc.          │  │                                  │   │  │
│  │  └──────────────────────┘  └──────────────────────────────────┘   │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 6. PAGE FOOTER                                                    │  │
│  │    (See PAGE_FOOTER_PATTERN eUI Skill for Simple or Advanced variants)   │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1–3 | Page Header (Breadcrumb + Title + Actions) | See **PAGE_HEADER_PATTERN** eUI Skill | Yes | The page header area (breadcrumb, title/subtitle, action items, optional collapsible body). Follows the **PAGE_HEADER_PATTERN** (Simple or Advanced variant). Retrieve the full pattern from the PAGE_HEADER_PATTERN eUI Skill for complete header implementation rules, component hierarchy, and generation instructions. |
| 4 | Left Column | `eui-page-column` [label, subLabel, euiSize2XL, isCollapsible, isAutocloseOnMobile] | Yes | Collapsible sidebar. Contains header body (sticky, optional), scrollable body, and footer. **Pluggable content**: filters, navigation, summary, category tree, etc. |
| 5 | Right Column | `eui-page-column` [label, subLabel (static or dynamic)] | Yes | **Pluggable** main content area. Contains header body (sticky, optional), header-right actions (optional), scrollable body, and footer. Content: data table, cards list, forms, detail views, or any custom component. |
| 6 | Page Footer | `eui-page-footer` | No | Global page-level actions. Follows the **PAGE_FOOTER_PATTERN** (Simple or Advanced variant). Retrieve the full pattern from the PAGE_FOOTER_PATTERN eUI Skill for complete footer implementation rules. |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── PAGE HEADER                                          ← See PAGE_HEADER_PATTERN eUI Skill
│   (Breadcrumb, title, subtitle, action items, optional body)
│   (Simple or Advanced variant — refer to PAGE_HEADER_PATTERN eUI Skill)
├── eui-page-content
│   └── eui-page-columns [hasPreventMobileRendering]
│       ├── eui-page-column [label][subLabel][euiSize2XL][isCollapsible][isAutocloseOnMobile]  ← LEFT (PLUGGABLE)
│       │   ├── eui-page-column-header-body              ← Optional sticky header
│       │   ├── eui-page-column-body
│       │   │   └── ⟨⟨ PLUGGABLE SIDEBAR CONTENT ⟩⟩
│       │   │       Option A: Search Filters (input + selects + reset button)
│       │   │       Option B: Navigation Menu (collapsible sidebar menu)
│       │   │       Option C: Summary Panel (key metrics, counters)
│       │   │       Option D: Category Tree (hierarchical navigation)
│       │   │       Option E: Any custom sidebar content
│       │   └── eui-page-column-footer                   ← Optional footer
│       │       └── div.eui-u-flex.eui-u-flex-justify-content-between
│       └── eui-page-column [label][subLabel]            ← RIGHT (PLUGGABLE)
│           ├── eui-page-column-header-body              ← Optional sticky header
│           ├── eui-page-column-header-right-content     ← Optional column-level actions
│           │   └── button[euiButton][euiSizeS] (×N)
│           ├── eui-page-column-body
│           │   └── ⟨⟨ PLUGGABLE CONTENT ⟩⟩
│           │       Option A: Data Table (euiTable + paginator)
│           │       Option B: Cards List (@for + eui-card)
│           │       Option C: Forms, detail views, custom components
│           └── eui-page-column-footer                   ← Optional footer
│               └── div.eui-u-flex.eui-u-flex-justify-content-between
└── eui-page-footer                                      ← See PAGE_FOOTER_PATTERN eUI Skill
    └── (Simple or Advanced variant — refer to PAGE_FOOTER_PATTERN eUI Skill)
```

---

## MCP EUI Compodoc Tool — Component Documentation Retrieval

> **IMPORTANT**: This pattern does NOT include inline code samples. Before generating code for this pattern, the AI tool **must** retrieve up-to-date component documentation, inputs, outputs, and examples from the **MCP EUI Compodoc tool**.

### Required Tool Calls

When implementing this pattern, use the following MCP EUI Compodoc tool calls to retrieve component APIs and examples:

#### Page Layout Components

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiPageComponent` | Root page structure, inputs, usage examples |
| `get_component_docs` | `EuiPageContentComponent` | Page content container |
| `get_component_docs` | `EuiPageColumnsComponent` | Multi-column layout container (hasPreventMobileRendering) |
| `get_component_docs` | `EuiPageColumnComponent` | Individual column (euiSize, isCollapsible, isAutocloseOnMobile) |
| `get_component_docs` | `EuiPageHeaderComponent` | Page/column header (label, subLabel, isCollapsible) |
| `get_component_docs` | `EuiPageFooterComponent` | Page footer (euiHighlighted support) |
| `get_component_docs` | `EuiPageBreadcrumbComponent` | Breadcrumb container |

#### Breadcrumb Components

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiBreadcrumbComponent` | Breadcrumb navigation |
| `get_component_docs` | `EuiBreadcrumbItemComponent` | Individual breadcrumb item (link, label, iconSvgName, ariaLabel) |

#### Button and Action Components

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiButtonDirective` | Button styles (euiPrimary, euiSecondary, euiOutline, euiSizeS) |
| `get_component_docs` | `EuiDropdownComponent` | Action overflow menus |
| `get_component_docs` | `EuiIconSvgComponent` | SVG icon rendering |

---

#### Left Column Content — Filter Components

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiInputTextComponent` | Search text input (euiClearable) |
| `get_component_docs` | `EuiSelectComponent` | Filter dropdown selects |
| `get_component_docs` | `EuiInputGroupComponent` | Form input group wrapper |
| `get_component_docs` | `EuiLabelDirective` | Field labels |

#### Left Column Content — Navigation Components

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiSidebarMenuComponent` | Sidebar navigation menu |
| `get_component_docs` | `EuiSidebarMenuItemComponent` | Menu items with expand/collapse |

#### Right Column Content — Table Components (Option A)

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiTableComponent` | Data table with sort, filter, paginator bindings |
| `get_component_inputs` | `EuiTableComponent` | Table inputs (data, filter, paginator, isTableResponsive) |
| `get_component_outputs` | `EuiTableComponent` | Table outputs (sortChange, filterChange) |
| `get_component_docs` | `EuiPaginatorComponent` | Paginator (hasPageNumberNavigation, pageSizeOptions, pageSize) |
| `get_component_examples` | `EuiTableComponent` | Table usage examples |

#### Right Column Content — Card Components (Option B)

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiCardComponent` | Card container (isSelectable, isSelected) |
| `get_component_inputs` | `EuiCardComponent` | Card inputs for selection state |
| `get_component_examples` | `EuiCardComponent` | Card usage examples |

#### UI Components

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiBadgeComponent` | Status/risk level color-coded badges |
| `get_component_docs` | `EuiTooltipDirective` | Tooltips on icon-only buttons |

#### Services (from @eui/core)

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiGrowlService` | Growl notifications for action feedback |

### Retrieval Strategy

1. **Before writing any component code**, call `get_component_docs` for each EUI component used in the pattern.
2. **For inputs/outputs details**, call `get_component_inputs` and `get_component_outputs` on the primary interactive components (EuiPageColumnComponent, EuiTableComponent, EuiCardComponent, EuiPaginatorComponent).
3. **For usage examples**, call `get_component_examples` on the main content components (EuiTableComponent, EuiCardComponent, EuiPageComponent).
4. **Use `search_components`** if you need to find related components by keyword (e.g., search "sidebar" to find navigation components).
5. **For accessibility requirements**, call `get_component_accessibility` on interactive components (EuiTableComponent, EuiCardComponent, EuiDropdownComponent).

---

## Left Column Content Options

The left column body is **content-agnostic**. Choose the appropriate sidebar content type based on user requirements:

### Option A: Search Filters

Use when the right column displays a data collection (table or cards) that needs filtering.

- Each filter uses `div[euiInputGroup]` containing a `label[euiLabel]` and an input/select element.
- Text search uses `input[euiInputText][euiClearable]` with `[maxlength]` and placeholder.
- Dropdown filters use `select[euiSelect]` with an "All" option (`value=""`) plus dynamic options from `@for`.
- Use Angular signals (`signal()`) for filter state and `computed()` for derived/filtered data.
- Bind with `[ngModel]` and `(ngModelChange)` using signal getter/setter pattern.
- Import `FormsModule` for ngModel bindings.
- Derive filter options from data using a `getDistinctValues()` helper method.
- Optionally include a Reset button in the column footer to clear all filters.

### Option B: Navigation Menu

Use when the left column provides page/section navigation.

- Use `eui-sidebar-menu` with `eui-sidebar-menu-item` elements.
- Menu items can be expandable/collapsible for hierarchical navigation.
- Optionally bind the active item to highlight the current selection.
- Retrieve `EuiSidebarMenuComponent` and `EuiSidebarMenuItemComponent` docs via MCP `get_component_docs` for exact API.

### Option C: Summary Panel

Use when the left column provides an overview or key metrics.

- Display key-value pairs, counters, or status indicators.
- Use utility classes for layout (`eui-u-flex`, `eui-u-flex-column`, spacing utilities).
- Optionally include links or actions to drill into details.

### Option D: Category Tree

Use when the left column provides hierarchical taxonomy navigation.

- Use a tree structure with expandable nodes.
- Bind selection to filter the right column content.
- Retrieve relevant tree/list component docs via MCP `get_component_docs` and `search_components`.

---

## Right Column Content Options

The right column body is **content-agnostic**. Choose the appropriate content type based on user requirements:

### Option A: Data Table

Use when the data is best displayed in rows and columns with sort/filter/pagination.

- Wrap table in `div.eui-table__scrollable-wrapper` for responsive overflow.
- Bind table with `[data]` and `[paginator]` inputs; use `euiTemplate` directives for header, body, and noData.
- Add `isTableResponsive` for mobile support; each `<td>` must have `data-col-label`.
- Use conditional badge directives (`[euiSuccess]`, `[euiWarning]`, `[euiDanger]`) for semantic status colors.
- Row actions use `eui-dropdown` with `euiDropdownItem` buttons.
- Place `eui-paginator` below the table.

### Option B: Cards List

Use when content is better represented as visual cards (e.g., items with images, rich descriptions, or selectable entries).

- Use `@for` to iterate over filtered items; wrap cards in a flex container with gap utilities.
- Use `eui-card` with optional `[isSelectable]` and `[isSelected]` bindings.
- Include card header (title, subtitle, actions) and card body (description, badges).
- Include `@empty` block for the empty state.
- Place `eui-paginator` below the cards when pagination is needed.

### Option C: Forms / Detail Views / Custom Content

Use when the right column displays forms, detail information, or any other custom content.

- Structure content using EUI utility classes for layout and spacing.
- Use `eui-input-group` and form components for data entry scenarios.
- For detail views, organize data in sections with labels and values.

---

## Content Type Decision Guide

### Left Column Decision

| Criteria | Use Filters | Use Navigation | Use Summary |
|----------|-------------|----------------|-------------|
| Right column has filterable data | ✅ | ❌ | ❌ |
| Page has multiple sections/sub-pages | ❌ | ✅ | ❌ |
| Overview/metrics are the primary need | ❌ | ❌ | ✅ |
| User needs to narrow down results | ✅ | ❌ | ❌ |
| Hierarchical content structure | ❌ | ✅ | ❌ |

### Right Column Decision

| Criteria | Use Data Table | Use Cards List |
|----------|---------------|----------------|
| Data has many fields per item | ✅ | ❌ |
| Need sortable columns | ✅ | ❌ |
| Items have visual/image content | ❌ | ✅ |
| Need selectable items | Both work | ✅ Preferred |
| Dense data display needed | ✅ | ❌ |
| Items have rich descriptions | ❌ | ✅ |
| Need row-level actions | ✅ | ✅ |
| Mobile-friendly overview | ❌ | ✅ Preferred |
| Comparison across items | ✅ | ❌ |

---

## Page Header

The page header follows the **PAGE_HEADER_PATTERN** described in the dedicated PAGE_HEADER_PATTERN eUI Skill. Two variants are available:

### Simple Page Header

- A minimal header with breadcrumb, title, subtitle (via `subLabel` input), and up to two direct action buttons.
- No collapsible behavior, no metadata, no tags, no overflow dropdown.
- Use when the page context is straightforward (list pages, simple forms).

### Advanced Page Header

- A feature-rich, collapsible header with breadcrumb, title, sub-label area (category badge, status chip, description, tags), action items (buttons, overflow dropdown, favorite toggle), and a collapsible body section with summary content.
- Use when the page displays detailed entity information or needs more than two actions.

> **Reference**: Retrieve the PAGE_HEADER_PATTERN from the eUI Skills library for complete header implementation rules, component hierarchy, variant selection guide, MCP retrieval strategy, and detailed generation instructions for both variants.

---

## Page Footer

The page footer follows the **PAGE_FOOTER_PATTERN** described in the dedicated PAGE_FOOTER_PATTERN eUI Skill. Two variants are available:

### Simple Page Footer

- Always visible, provides standard page actions (Save, Cancel, Submit).
- Uses a two-zone flex layout: left zone for dismissive/tertiary actions, right zone for affirmative actions.
- Left-side actions use `euiBasicButton` style; right-side uses `euiSecondary` and `euiPrimary`.
- Do NOT conditionally show/hide — it must always be visible.
- Do NOT use `euiHighlighted` on simple footers.

### Advanced Page Footer (Bulk Actions)

- Conditionally rendered when items are selected (`@if (selectedCount() > 0)`).
- Uses `euiHighlighted` directive on `eui-page-footer` for visual distinction.
- Left content includes a Reset button and a selection counter (`span.eui-u-f-bold` for the count).
- Right content includes action buttons with icons and an optional overflow `eui-dropdown`.
- Uses Angular signals (`signal()`) for the selection count.

> **Reference**: Retrieve the PAGE_FOOTER_PATTERN from the eUI Skills library for complete footer implementation rules, flexbox layout structure, MCP retrieval strategy, accessibility guidelines, and detailed generation instructions for both variants.

---

## Filter Architecture (Left Column — Angular Signals)

When the left column hosts search filters, the component state is managed with Angular signals and computed values:

- **Filter state signals**: Use `signal('')` for each filter field (e.g., `searchText`, `selectedStatus`, `selectedCategory`).
- **Derived filter options**: Use `computed()` to extract distinct values from the data source.
- **Filtered data**: Use a `computed()` that recomputes when any filter signal changes, applying all active filters to the source data.
- **Template binding**: Use `[ngModel]` and `(ngModelChange)` with the signal getter/setter pattern. Requires `FormsModule` import.
- **Retrieve component docs and examples** via MCP EUI Compodoc tool (`get_component_docs`, `get_component_examples`) for `EuiInputTextComponent`, `EuiSelectComponent`, and `EuiInputGroupComponent` before writing filter code.

---

## Required Angular Imports

> **Do not hardcode import paths.** Always retrieve the correct module/token imports by calling `get_component_docs` from the MCP EUI Compodoc tool for each component. The response includes the `imports` field with the proper module tokens.

### Import Tokens to Retrieve via MCP

The following EUI tokens are needed for this pattern. Use `get_component_docs` to confirm exact import paths and available APIs:

#### Base Pattern (layout only)

| Token | Purpose |
|-------|---------|
| `EUI_PAGE` | Page layout structure (page, page-content, page-columns, page-column, page-header, page-footer) |
| `EUI_BREADCRUMB` | Navigation breadcrumb |
| `EUI_BUTTON` | Action buttons |
| `EUI_DROPDOWN` | Overflow action menus |
| `EUI_ICON` | SVG icons |

#### With Filters (left column)

| Token | Purpose |
|-------|---------|
| `EUI_INPUT_TEXT` | Search text input |
| `EUI_SELECT` | Filter dropdown selects |
| `EUI_INPUT_GROUP` | Form input group wrapper |
| `EUI_LABEL` | Field labels |
| `FormsModule` (`@angular/forms`) | ngModel bindings |

#### With Data Table (right column)

| Token | Purpose |
|-------|---------|
| `EUI_TABLE` | Table component + Sort type |
| `EUI_PAGINATOR` | Paginator component |
| `EUI_BADGE` | Status/risk badges |
| `EuiTemplateDirective` | Table templates |
| `DecimalPipe` (`@angular/common`) | Number formatting |

#### With Cards List (right column)

| Token | Purpose |
|-------|---------|
| `EUI_CARD` | Card containers |
| `EUI_BADGE` | Status badges |
| `EUI_PAGINATOR` | Paginator component |

#### Services

| Token | Purpose |
|-------|---------|
| `EuiGrowlService` (`@eui/core`) | Growl notifications |

### Angular Core Imports

- `ChangeDetectionStrategy`, `Component`, `computed`, `inject`, `signal` from `@angular/core`
- `FormsModule` from `@angular/forms`
- `DecimalPipe` from `@angular/common` (when using number formatting)

---

## Data Model

All data models, mock data, and filter utilities are defined **inline** in the component file — no external shared folder dependencies. The component must be fully self-contained.

### Interface

Define a TypeScript interface that describes the shape of a single data item. Fields and types depend on the business domain (e.g., contracts, users, products, tasks, etc.).

### Mock Data

Define a typed constant array at the top of the component file, before the `@Component` decorator, with representative sample records. No external file imports needed.

### Filter Utilities

Define a `getDistinctValues(field)` helper method that extracts unique string values from a given field of the data array, sorted alphabetically. This is used to dynamically populate filter dropdown options.

---

## File Structure

```
<feature-folder>/
└── columns-layout/
    ├── component.ts              ← Component with inline interface, data, and signal-based logic
    ├── component.html            ← Template with two-column layout
    └── COLUMNS_LAYOUT_PATTERN.md ← This canonical pattern reference (used by AI for generation)
```

> **Self-contained principle:** The component has no external imports beyond Angular framework (`@angular/*`) and EUI library (`@eui/*`) packages. The data interface and mock data array are defined inline in the component file.

---

## Route Registration

Register the component as a lazy-loaded standalone component in the feature's routing module or standalone routes file. The route `path` and `loadComponent` import path are project-specific — choose meaningful values for your application.

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### Pre-Generation Step (MCP Tool Retrieval)

0. **Before writing any code**, call the MCP EUI Compodoc tool to retrieve documentation for all EUI components used in the pattern. Use the retrieved inputs, outputs, and examples as the authoritative source for component APIs. Refer to the "MCP EUI Compodoc Tool — Component Documentation Retrieval" section for the full list of required tool calls.

### Layout Rules

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: breadcrumb → header (with actions + optional body) → page-content (columns) → page-footer.
3. **Use `eui-page-columns` with `hasPreventMobileRendering`** inside `eui-page-content`.
4. **Left column is always the first `eui-page-column`** with `label`, `subLabel`, `euiSize2XL`, `isCollapsible`, and `isAutocloseOnMobile`.
5. **Right column is always the second `eui-page-column`** with `label` and optionally dynamic `[subLabel]` (e.g., showing result count).
6. **Page header follows the PAGE_HEADER_PATTERN eUI Skill** — use the Simple variant (title + subtitle + up to 2 buttons) or Advanced variant (collapsible, metadata, overflow menu, tags) depending on requirements.
7. **Page footer follows the PAGE_FOOTER_PATTERN eUI Skill** — use the Simple variant (always visible) or Advanced variant (conditional bulk actions) depending on requirements.
8. **Use `ChangeDetectionStrategy.OnPush`** on the component.
9. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_TABLE`).

### Left Column Rules (Pluggable Sidebar)

10. **The left column is content-agnostic.** Choose the sidebar content type (filters, navigation, summary, etc.) based on user requirements.
11. **For search filters**: Each filter uses `div[euiInputGroup]` containing a `label[euiLabel]` and an input/select element.
12. **For text search**: Use `input[euiInputText][euiClearable]` with `[maxlength]` and placeholder.
13. **For dropdown filters**: Use `select[euiSelect]` with an "All" option (`value=""`) plus dynamic options from `@for`.
14. **Use Angular signals** (`signal()`) for filter state and `computed()` for derived/filtered data.
15. **Bind with `[ngModel]` and `(ngModelChange)`** using signal getter/setter pattern.
16. **Import `FormsModule`** for ngModel bindings (when using filters).
17. **Derive filter options from data** using a `getDistinctValues()` helper method (when using filters).
18. **For navigation**: Use `eui-sidebar-menu` with collapsible menu items.
19. **For summary/custom content**: Use EUI utility classes for layout and spacing.

### Right Column Content Rules (Pluggable)

20. **The right column body is content-agnostic.** Choose the content type based on user requirements.
21. **For data tables**: wrap in `div.eui-table__scrollable-wrapper`, bind with `[data]` and `[paginator]`, use `euiTemplate` directives, add `isTableResponsive`, and ensure each `<td>` has `data-col-label`.
22. **For cards lists**: use `@for` to iterate over filtered items, wrap cards in a flex container (`eui-u-flex eui-u-flex-wrap eui-u-flex-gap-m`), use `eui-card` with optional `[isSelectable]`.
23. **For any content type**: connect it to the filter signals from the left column via a `computed()` signal that reacts to filter changes.
24. **Always include an empty state** (no-data template for tables, `@empty` block for cards/lists).
25. **Place `eui-paginator`** below the content when pagination is needed.

### Badge and Action Rules

26. **Use conditional badge directives** for semantic colors: `[euiSuccess]`, `[euiWarning]`, `[euiDanger]`, `[euiInfo]`.
27. **Row/card actions use `eui-dropdown`** with `euiButton euiPrimary euiOutline euiSizeS` as the trigger and `eui-dropdown-content` containing `button[euiDropdownItem]` items.

### Header Rules

28. **Follow the PAGE_HEADER_PATTERN eUI Skill** for all header implementation details (breadcrumb, title, actions, sub-label, collapsible body).
29. **Simple header**: Non-collapsible, uses `label` and `subLabel` inputs, up to two direct action buttons.
30. **Advanced header**: Collapsible, uses `eui-page-header-sub-label` for category/status/tags, overflow dropdown, favorite toggle, and header body.

### Footer Rules

31. **Follow the PAGE_FOOTER_PATTERN eUI Skill** for all footer implementation details.
32. **Simple footer**: Always visible, uses two-zone flex layout with dismissive actions on the left and affirmative actions on the right.
33. **Advanced footer**: Conditionally rendered when items are selected, uses `euiHighlighted`, includes selection counter and bulk action buttons.
34. **Use `inject(EuiGrowlService)`** for action feedback notifications.

### Accessibility

35. All icon-only buttons must have `aria-label`.
36. Breadcrumb home item must have `ariaLabel="Home"`.
37. Dropdown triggers must have `aria-label` or `euiTooltip`.
38. Use `<span euiLabel>` for button text that accompanies icons.
39. Each dropdown action item must have `aria-label`.
40. **Retrieve accessibility docs** via MCP `get_component_accessibility` for each interactive component to ensure compliance.

---

## Implementation Reference

A complete implementation of this pattern produces a **fully self-contained component** with two files:

- **`component.ts`** — Contains the data interface, mock data constant, and the component class with signal-based filtering and `ChangeDetectionStrategy.OnPush`
- **`component.html`** — Contains the complete two-column layout template

### Typical implementation features:

- **Page header**: Simple or Advanced variant (following PAGE_HEADER_PATTERN eUI Skill)
- **Left column**: Pluggable sidebar content (filters, navigation, summary) connected via Angular signals
- **Right column**: Pluggable main content (data table, cards list, forms) driven by computed signals
- **Page footer**: Simple or Advanced variant (following PAGE_FOOTER_PATTERN eUI Skill)
- **No external dependencies**: Data interface and mock data are defined inline in the component file
- **Service injection**: Use `inject(EuiGrowlService)` for action feedback notifications
- **Exported component class** for lazy loading via `loadComponent`

---

## Comparison with Other Layout Patterns

| Feature | Simple Layout | **Columns Layout** | Fluid Layout |
|---------|--------------|-------------------|--------------|
| Columns | 1 | 2 (flat) | 2+ (nested + panel) |
| Left sidebar | No | Yes (collapsible, pluggable) | Yes (nested sub-column) |
| Right content | Single free-form area | Pluggable (table, cards, etc.) | Pluggable (cards or table) |
| Detail panel | No | No | Yes (resizable) |
| Nested sub-columns | No | No | Yes |
| Multi-select + dimmer | No | Optional | Yes |
| Sidebar content options | N/A | Filters, navigation, summary, etc. | Filters only |
| Page footer | Simple three-zone | Simple or Advanced (PAGE_FOOTER_PATTERN) | Advanced (bulk actions) |
| Complexity | Low | Medium | High |
