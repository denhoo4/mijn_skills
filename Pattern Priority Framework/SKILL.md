---
name: Pattern Priority Framework
description: Deterministic pattern selection rules for evaluating and choosing the correct EUI design pattern based on functional requirements. Use when a new page must be generated and the correct pattern needs to be determined. Covers app shell patterns (APP_HEADER, APP_TOOLBAR), page header and footer patterns (PAGE_HEADER, PAGE_FOOTER), page layout patterns (FLUID_LAYOUT, NAVIGATION_LAYOUT, COLUMNS_LAYOUT, SIMPLE_LAYOUT), page list patterns (TABLE_LIST, PAGE_LIST_CARDS_FILTER, PAGE_LIST_CARDS_SELECTION, PAGE_LIST_CARDS_SIMPLE, PAGE_LIST_CARDS_VARIANTS), and page details patterns (PAGE_DETAILS_ADVANCED, PAGE_DETAILS_SIMPLE). Triggered when generating any EUI page, selecting between layout structures, choosing list display modes, or determining detail/form page structure.
---

# Pattern Priority Framework

Deterministic pattern selection rules that apply across all EUI design patterns. Evaluate this framework before reading individual pattern files. The same requirements must consistently produce the same pattern.

---

## Pattern Categories

| Category | Purpose | Patterns |
|----------|---------|----------|
| **App Shell** | Application-level shell structures (header bar, toolbar) | APP_HEADER, APP_TOOLBAR |
| **Page Header & Footer** | Reusable page header and footer structures | PAGE_HEADER, PAGE_FOOTER |
| **Page Layout** | Structural arrangement of columns and zones | SIMPLE_LAYOUT, COLUMNS_LAYOUT, NAVIGATION_LAYOUT, FLUID_LAYOUT |
| **Page List** | How a list of items is displayed and interacted with | PAGE_LIST_CARDS_SIMPLE, PAGE_LIST_CARDS_SELECTION, PAGE_LIST_CARDS_FILTER, PAGE_LIST_CARDS_VARIANTS, TABLE_LIST |
| **Page Details** | How a single entity's details/form is presented | PAGE_DETAILS_SIMPLE, PAGE_DETAILS_ADVANCED |
| **Coding Rules** | Mandatory coding conventions for all EUI patterns | EUI_CODING_RULES |

---

## Selection Algorithm

Before generating any page, follow this algorithm exactly:

### Step 1: Determine Page Purpose

- **List page** (displaying multiple items) → Step 2a
- **Detail/form page** (displaying/editing a single entity) → Step 2b
- **Other content** (dashboard, settings, documentation) → Step 2c

### Step 2a: List Page — Select List Pattern

1. Is the data inherently tabular (structured multi-column, needs sorting, per-row actions)? → **TABLE_LIST**
2. Are filter sidebar + selection + bulk actions needed with card-based display? → **PAGE_LIST_CARDS_FILTER**
3. Is multi-select with bulk actions needed but no filter sidebar? → **PAGE_LIST_CARDS_SELECTION**
4. Is neither filtering nor selection needed? → **PAGE_LIST_CARDS_SIMPLE**
5. Override: If a persistent inline detail panel is needed alongside the list → **FLUID_LAYOUT** (replaces list pattern)

### Step 2b: Detail/Form Page — Select Details Pattern

1. Is sidebar navigation between form sections needed, or multiple action zones (header + column + footer)? → **PAGE_DETAILS_ADVANCED**
2. Otherwise → **PAGE_DETAILS_SIMPLE**

### Step 2c: Other Content — Select Layout Pattern

1. Is a persistent detail/preview/inspector panel required? → **FLUID_LAYOUT**
2. Is a persistent navigation menu required? → **NAVIGATION_LAYOUT**
3. Is a sidebar with filter/search/contextual controls required? → **COLUMNS_LAYOUT**
4. Otherwise → **SIMPLE_LAYOUT**

### Disambiguation Rules

- Between NAVIGATION_LAYOUT and COLUMNS_LAYOUT: "Is the left column for navigating between pages, or for filtering content on the current page?" Navigation → NAVIGATION_LAYOUT. Filtering → COLUMNS_LAYOUT.
- Between TABLE_LIST and PAGE_LIST_CARDS_FILTER: "Is the data structured multi-column tabular data, or are items better represented as visual card blocks?" Tabular → TABLE_LIST. Cards → PAGE_LIST_CARDS_FILTER.
- Between PAGE_DETAILS_ADVANCED and NAVIGATION_LAYOUT: Does the page embed a reusable form component? → PAGE_DETAILS_ADVANCED. Does main content vary across navigation items? → NAVIGATION_LAYOUT.
- Between PAGE_LIST_CARDS_FILTER and COLUMNS_LAYOUT: Is the page's primary purpose a filterable list with selection? → PAGE_LIST_CARDS_FILTER. Is the right column not list-specific? → COLUMNS_LAYOUT.
- FLUID_LAYOUT always wins over other layouts when a persistent side panel is required.
- Never choose SIMPLE_LAYOUT if a dedicated sidebar, navigation, filter region, or detail panel is required.
- Never choose PAGE_LIST_CARDS_SIMPLE if selection checkboxes or filter sidebar are required.
- Select patterns solely from functional requirements, not visual preference.

### Cross-Category Implied Layouts

- TABLE_LIST → implies COLUMNS_LAYOUT structure
- PAGE_LIST_CARDS_FILTER → implies COLUMNS_LAYOUT structure
- PAGE_LIST_CARDS_SELECTION / PAGE_LIST_CARDS_SIMPLE → implies single-column within `eui-page-columns`
- PAGE_DETAILS_ADVANCED → implies NAVIGATION_LAYOUT structure
- PAGE_DETAILS_SIMPLE → implies SIMPLE_LAYOUT structure
- FLUID_LAYOUT can host a list with inline preview panel — prefer over PAGE_LIST patterns when persistent detail panel is needed

---

## Quick Decision Matrix

### Layout Selection

| Requirement | Pattern |
|------------|---------|
| Create/Edit Form (single section) | SIMPLE_LAYOUT |
| Settings Page (single section) | SIMPLE_LAYOUT |
| Detail/View Page (no navigation) | SIMPLE_LAYOUT |
| Documentation Page (no nav) | SIMPLE_LAYOUT |
| Data table page (no filters) | SIMPLE_LAYOUT |
| Search + Filters + Results | COLUMNS_LAYOUT |
| Category Filter + Content | COLUMNS_LAYOUT |
| Tree Filter + Content | COLUMNS_LAYOUT |
| Explorer Interface | COLUMNS_LAYOUT |
| Settings App (multi-section) | NAVIGATION_LAYOUT |
| Admin Console | NAVIGATION_LAYOUT |
| Documentation Portal (with nav) | NAVIGATION_LAYOUT |
| Help Center / Knowledge Base | NAVIGATION_LAYOUT |
| Detail page with section nav | NAVIGATION_LAYOUT |
| Record Management + Detail Panel | FLUID_LAYOUT |
| Entity Browser + Inspector | FLUID_LAYOUT |
| Case Management Workspace | FLUID_LAYOUT |
| Document Review + Properties | FLUID_LAYOUT |
| List + Persistent Side Detail | FLUID_LAYOUT |
| Master-Detail (side-by-side) | FLUID_LAYOUT |

### List Selection

| Requirement | Pattern |
|------------|---------|
| Simple paginated list (cards/table) | PAGE_LIST_CARDS_SIMPLE |
| List with per-item actions only | PAGE_LIST_CARDS_SIMPLE |
| List with multi-select + bulk actions | PAGE_LIST_CARDS_SELECTION |
| List with select-all/unselect-all toggle | PAGE_LIST_CARDS_SELECTION |
| List with dimmer highlight on selection | PAGE_LIST_CARDS_SELECTION |
| Filtered list + selection + bulk actions (cards) | PAGE_LIST_CARDS_FILTER |
| Advanced search + filter criteria chips (cards) | PAGE_LIST_CARDS_FILTER |
| Filter sidebar + selectable cards | PAGE_LIST_CARDS_FILTER |
| Sortable data table + filter sidebar | TABLE_LIST |
| Tabular data with row selection + bulk actions | TABLE_LIST |
| Multi-column structured data with per-row actions | TABLE_LIST |
| Large dataset with sorting, pagination, inline search | TABLE_LIST |
| Monitoring, inventories, financial/historical data | TABLE_LIST |
| Filter sidebar + selectable table rows | TABLE_LIST |

### Details Selection

| Requirement | Pattern |
|------------|---------|
| Single-column form/detail page | PAGE_DETAILS_SIMPLE |
| Reusable form in simple layout | PAGE_DETAILS_SIMPLE |
| Create/Edit page with footer actions | PAGE_DETAILS_SIMPLE |
| Detail page with sidebar section nav | PAGE_DETAILS_ADVANCED |
| Form with header summary card | PAGE_DETAILS_ADVANCED |
| Multi-section form with navigation | PAGE_DETAILS_ADVANCED |
| Detail page with back-to-list button | PAGE_DETAILS_ADVANCED |

---

## Feature Comparison

| Feature | SIMPLE | COLUMNS | NAVIGATION | FLUID | LIST SIMPLE | LIST SELECTION | LIST FILTER | TABLE LIST | DETAILS SIMPLE | DETAILS ADVANCED |
|---------|--------|---------|------------|-------|-------------|----------------|-------------|------------|----------------|-----------------|
| Columns | 1 | 2 | 2 | 2+ nested | 1 | 1 | 2 | 2 | 1 | 2 |
| Filter sidebar | ❌ | ✅ | ❌ | ✅ (nested) | ❌ | ❌ | ✅ | ✅ | ❌ | ❌ |
| Sidebar menu | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Data table | ❌ | Optional | ❌ | Optional | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ |
| Sortable columns | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ |
| Inline table search | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ |
| Multi-select | ❌ | Optional | ❌ | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ | ❌ |
| Dimmer effect | ❌ | ❌ | ❌ | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ | ✅ |
| Bulk action footer | ❌ | Optional | ❌ | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ | ❌ |
| Resizable panel | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Criteria chips | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ❌ | ❌ |
| Per-row actions | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ |
| Pluggable content | ✅ | ✅ | ✅ | ✅ | ✅ (cards/table) | ✅ (cards/table) | ✅ (cards/table) | Table | Form component | Form component |
| Reusable form | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ |
| Header summary card | ❌ | ❌ | Optional | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Expandable header | ❌ | Optional | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ | Optional | ✅ |

---

## Pattern Files Reference

When a pattern is selected, read the corresponding pattern document referenced below.

### App Shell

| Pattern ID | Pattern File |
|---|---|
| APP_HEADER | APP_HEADER_PATTERN.md |
| APP_TOOLBAR | APP_TOOLBAR_PATTERN.md |

### Page Header and Footer

| Pattern ID | Pattern File |
|---|---|
| PAGE_HEADER | PAGE_HEADER_PATTERN.md |
| PAGE_FOOTER | PAGE_FOOTER_PATTERN.md |

### Page Layout

| Pattern ID | Pattern File |
|---|---|
| SIMPLE_LAYOUT | SIMPLE_LAYOUT_PATTERN.md |
| NAVIGATION_LAYOUT | NAVIGATION_LAYOUT_PATTERN.md |
| COLUMNS_LAYOUT | COLUMNS_LAYOUT_PATTERN.md |
| FLUID_LAYOUT | FLUID_LAYOUT_PATTERN.md |

### Page List

| Pattern ID | Pattern File |
|---|---|
| PAGE_LIST_CARDS_VARIANTS | PAGE_LIST_CARDS_VARIANTS_PATTERN.md |
| PAGE_LIST_CARDS_SIMPLE | PAGE_LIST_CARDS_SIMPLE_PATTERN.md |
| PAGE_LIST_CARDS_SELECTION | PAGE_LIST_CARDS_SELECTION_PATTERN.md |
| PAGE_LIST_CARDS_FILTER | PAGE_LIST_CARDS_FILTER_PATTERN.md |
| TABLE_LIST | TABLE_LIST_PATTERN.md |

### Page Detail

| Pattern ID | Pattern File |
|---|---|
| PAGE_DETAILS_SIMPLE | PAGE_DETAILS_SIMPLE_PATTERN.md |
| PAGE_DETAILS_ADVANCED | PAGE_DETAILS_ADVANCED_PATTERN.md |

### Coding Rules

| Rule Set | File |
|---|---|
| EUI_CODING_RULES | SKILL.md |
