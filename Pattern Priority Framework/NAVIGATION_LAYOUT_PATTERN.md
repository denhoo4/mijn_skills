---
name: Navigation Layout Pattern — Canonical Structure Reference
description: Canonical reference for the EUI Navigation Layout design pattern — a two-column page layout with a collapsible sidebar navigation menu (eui-sidebar-menu) and a pluggable main right content area (detail cards, forms, tables, dashboards). Includes breadcrumb, expandable page header with metadata, page-level actions, and page footer with full generation rules.
label: navigation-layout-pattern
category: pattern
applies-to: two-column page layout with sidebar navigation menu and pluggable right column content (detail cards, forms, tables, dashboards, settings)
triggered-when: generating a navigation layout page, a page with sidebar menu navigation between sections, or a detail page with inner navigation
requires: eUI page components (base), eui-sidebar-menu, plus content-specific components depending on right column content type
outputs: a two-column page following the Navigation Layout pattern with sidebar menu, expandable page header, pluggable main content, and page footer
related-skills: NAVIGATION_MENU_PATTERN, COLUMNS_LAYOUT_PATTERN, PAGE_DETAILS_ADVANCED_PATTERN, SIMPLE_LAYOUT_PATTERN
---

# EUI Navigation Layout Pattern — Canonical Structure Reference

## Purpose

This document describes the **Navigation Layout** design pattern — a two-column page layout with a sidebar navigation menu used across EUI-based applications. It serves as the canonical reference for AI code generation.

### What is this pattern?

The Navigation Layout pattern represents a **sidebar navigation + content page** wrapped inside the standard EUI page scaffolding (breadcrumb, expandable page header with actions, footer). The left column contains a collapsible `eui-sidebar-menu` for navigating between sub-sections; the right column is the main **pluggable content area** that can host any type of content:

- **Detail cards** — stacked cards with field/value pairs for entity detail views
- **Forms** — data entry with validation and multi-step workflows
- **Data table** — sortable, filterable, paginated tabular data
- **Dashboard** — charts, KPIs, and summary widgets
- **Settings** — configuration panels with toggles, inputs, and sections
- **Any custom content** — lists, timelines, documents, etc.

---

## Recommended Usage

Use this pattern when:

- A page needs sidebar navigation between multiple sub-sections within a single context
- The main content area should be pluggable (detail view, form, table, dashboard, settings)
- Inner navigation drives what content is displayed in the main area
- The page header should display key metadata with expand/collapse capability
- Page-level actions are needed in both the header and footer
- A breadcrumb trail provides navigation context

**Do not use** when:
- A simple single-column layout suffices (use Simple Layout instead)
- The left column is for filters rather than navigation (use Columns Layout instead)
- No inner navigation between sub-sections is needed

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 1. PAGE BREADCRUMB                                                │  │
│  │    Home > Section > Current page                                  │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────┬────────────────────────────────────┐  │
│  │ 2. PAGE HEADER (expandable)  │ 3. PAGE HEADER ACTIONS             │  │
│  │    Title / Sub-label         │    [Secondary] [Primary] [▼ More]  │  │
│  ├──────────────────────────────┴────────────────────────────────────┤  │
│  │    PAGE HEADER BODY (collapsible metadata card, optional)         │  │
│  │    Field 1 | Field 2 | Field 3 | Field 4 | ...                    │  │
│  │    [+ Show more / - Show less]                                    │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ eui-page-content > eui-page-columns                               │  │
│  │  ┌──────────────────────┐  ┌──────────────────────────────────┐   │  │
│  │  │ 4. NAVIGATION COLUMN │  │ 5. MAIN COLUMN (PLUGGABLE)       │   │  │
│  │  │    (collapsible)     │  │                                  │   │  │
│  │  │                      │  │    << PLUGGABLE CONTENT >>       │   │  │
│  │  │  ┌────────────────┐  │  │                                  │   │  │
│  │  │  │ SIDEBAR MENU   │  │  │  Any content: detail cards,      │   │  │
│  │  │  │                │  │  │  forms, tables, dashboards,      │   │  │
│  │  │  │ ● Section 1    │  │  │  settings, timelines,            │   │  │
│  │  │  │ ● Section 2    │  │  │  custom components, etc.         │   │  │
│  │  │  │ ● Section 3    │  │  │                                  │   │  │
│  │  │  │ ● Section N    │  │  │                                  │   │  │
│  │  │  └────────────────┘  │  │                                  │   │  │
│  │  │                      │  │                                  │   │  │
│  │  └──────────────────────┘  └──────────────────────────────────┘   │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 6. PAGE FOOTER                                                    │  │
│  │    [Tertiary]                        [Secondary] [Primary]        │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item` | No | Navigation trail. First item uses `iconSvgName="eui-home"` with `ariaLabel="Home"`. Last item has no `link` (current page). |
| 2 | Page Header | `eui-page-header` [label, isCollapsible, isCollapsed] | Yes | Page title (static or dynamic). May include `eui-page-header-sub-label` for inline metadata and `eui-page-header-body` for expandable content. For full details, refer to the **Page Header Pattern** in the eUI Skills (see [Cross-References](#cross-references)). |
| 3 | Page Header Actions | `eui-page-header-action-items` | No | Top-level page actions: primary/secondary buttons and overflow dropdown for extra actions. |
| 4 | Navigation Column | `eui-page-column` [label="Navigation", euiSize2XL, isCollapsible, hasSidebarMenu] | Yes | Collapsible sidebar with `eui-sidebar-menu` for navigating between sub-sections. Uses icons and collapsed initials. |
| 5 | Main Column | `eui-page-column` [label] | Yes | **Pluggable** main content area. Content varies based on requirements: detail cards, forms, tables, dashboards, settings panels, or any custom component. |
| 6 | Page Footer | `eui-page-footer` | No | Page-level actions. Supports tertiary (left), secondary, and primary (right) button zones. For full details, refer to the **Page Footer Pattern** in the eUI Skills (see [Cross-References](#cross-references)). |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── eui-page-breadcrumb
│   └── eui-breadcrumb
│       └── eui-breadcrumb-item (×N)
├── eui-page-header [label][isCollapsible][isCollapsed]
│   ├── eui-page-header-sub-label                        ← Optional inline metadata
│   │   └── div (badges, chips, text)
│   ├── eui-page-header-action-items
│   │   ├── button[euiButton][euiSecondary]
│   │   ├── button[euiButton][euiPrimary]
│   │   └── eui-dropdown
│   │       ├── button[euiButton][euiPrimary][euiOutline] + eui-icon-svg
│   │       └── eui-dropdown-content
│   │           └── button[euiDropdownItem] (×N)
│   └── eui-page-header-body                             ← Optional expandable content
│       └── eui-card (metadata grid with show more/less toggle)
├── eui-page-content
│   └── eui-page-columns
│       ├── eui-page-column [label="Navigation"][euiSize2XL][isCollapsible][hasSidebarMenu]  ← NAVIGATION
│       │   └── eui-page-column-body
│       │       └── eui-sidebar-menu [items][hasIcons][hasCollapsedInitials]
│       └── eui-page-column [label]                      ← MAIN (PLUGGABLE)
│           └── eui-page-column-body
│               └── << PLUGGABLE CONTENT >>
│                   Option A: Detail Cards (eui-card stacked)
│                   Option B: Forms (form controls + validation)
│                   Option C: Data Table (euiTable + paginator)
│                   Option D: Dashboard (charts, KPIs, widgets)
│                   Option E: Settings (toggles, inputs, sections)
│                   Option F: Any custom content
└── eui-page-footer
    └── div.eui-u-flex.eui-u-flex-justify-content-end.eui-u-flex-align-items-center
        ├── div (left: tertiary actions)
        └── div (right: secondary + primary actions)
```

---

## Component Documentation Sources

All component APIs (inputs, outputs, selectors, usage examples) must be retrieved from the **EUI MCP Compodoc tool** at generation time. Do not rely on hardcoded import paths or API signatures in this document. Query the following components:

| Component | MCP Compodoc Query |
|-----------|-------------------|
| Page root | `EuiPageComponent` |
| Page header | `EuiPageHeaderComponent` |
| Page header sub-label | `EuiPageHeaderSubLabelComponent` |
| Page header action items | `EuiPageHeaderActionItemsComponent` |
| Page header body | `EuiPageHeaderBodyComponent` |
| Page breadcrumb | `EuiPageBreadcrumbComponent` |
| Page content | `EuiPageContentComponent` |
| Page columns | `EuiPageColumnsComponent` |
| Page column | `EuiPageColumnComponent` |
| Sidebar menu | `EuiSidebarMenuComponent` |
| Page footer | `EuiPageFooterComponent` |
| Card | `EuiCardComponent` |
| Button | `EuiButtonDirective` |
| Chip | `EuiChipComponent` |
| Dropdown | `EuiDropdownComponent` |
| Icon | `EuiIconSvgComponent` |
| Breadcrumb | `EuiBreadcrumbComponent` |

For content-specific components (tables, forms, paginators, etc.), query the EUI MCP Compodoc tool for the relevant component documentation.

---

## Main Column Content Options

The main column body is **content-agnostic**. Choose the content type based on requirements.

### Option A: Detail Cards

Use when the page displays structured entity data in multiple categorized sections. Use stacked `eui-card` components separated by spacing utilities, with responsive grid (`col-md-6`) for field/value pairs inside `eui-card-content`.

### Option B: Forms

Use when the page sections contain editable form fields (settings, profile, multi-step wizards). Wrap form controls in `eui-card` sections, use `euiInputGroup` + `euiLabel` + `euiInputText`/`euiSelect`, bind with `[ngModel]` and signal setters.

### Option C: Data Table

Use when a navigation section displays tabular data with sort/filter/pagination. Wrap in `div.eui-table__scrollable-wrapper`, bind with `[data]` and `[paginator]`, use `euiTemplate` directives, add `isTableResponsive`.

### Option D: Dashboard / KPIs

Use when a section displays summary metrics, charts, or progress indicators. Use responsive grid (`row` + `col-md-4`) with KPI cards.

---

## Content Type Decision Guide

| Criteria | Detail Cards | Forms | Data Table | Dashboard |
|----------|-------------|-------|------------|-----------|
| Read-only entity data | ✅ | ❌ | ❌ | ❌ |
| Editable fields | ❌ | ✅ | ❌ | ❌ |
| Tabular data with sort/filter | ❌ | ❌ | ✅ | ❌ |
| Summary metrics / KPIs | ❌ | ❌ | ❌ | ✅ |
| Multiple categorized sections | ✅ | ✅ | ❌ | ✅ |
| Status indicators | ✅ (chips) | ❌ | ✅ (badges) | ✅ |
| Rich field/value pairs | ✅ | ❌ | ❌ | ❌ |
| Validation feedback | ❌ | ✅ | ❌ | ❌ |
| Pagination needed | ❌ | ❌ | ✅ | ❌ |
| Multi-step workflow | ❌ | ✅ | ❌ | ❌ |

---

## Cross-References

The Page Header and Page Footer zones in this pattern follow their own canonical pattern references. Retrieve their full structure and generation rules from the **eUI Skills**:

- **Page Header Pattern** → available from eUI Skills. Query the EUI MCP Compodoc tool for `EuiPageHeaderComponent` to retrieve the full component API.
- **Page Footer Pattern** → available from eUI Skills. Query the EUI MCP Compodoc tool for `EuiPageFooterComponent` to retrieve the full component API.

When generating pages using this layout, apply the Page Header and Page Footer rules from the eUI Skills for those zones respectively.

---

## Expandable Page Header Pattern

The expandable header uses `[isCollapsible]="true"` on `eui-page-header` combined with a `eui-page-header-body` containing a metadata card with a show more/less toggle.

### Sub-Label Zone

The `eui-page-header-sub-label` displays inline metadata alongside the title. Typical content includes:
- A category/department badge (dark background utility class)
- A status chip with conditional color directives (`[euiSuccess]`, `[euiWarning]`, `[euiDanger]`, `[euiInfo]`)
- Additional text (e.g., supplier, owner)

### Metadata Grid (Header Body)

Use a responsive grid (`row` + `col-xxxl-3 col-xxl-4 col-xl-6`) inside a card for structured metadata. Display initial fields visibly and hide additional fields behind a show more/less toggle using a signal-driven boolean.

### Show More/Less Toggle

Use a signal-driven toggle button with `eui-add`/`eui-remove` icons and `@if` block for additional fields.

For full Page Header implementation details (inputs, accessibility, collapsible behavior), retrieve documentation from the EUI MCP Compodoc tool by querying `EuiPageHeaderComponent`.

---

## Sidebar Menu Configuration

The sidebar menu items are defined as an `EuiMenuItem[]` array with icons.

Key rules:
- Always use `hasIcons` and `hasCollapsedInitials` on `eui-sidebar-menu`
- Use relative URLs (`./`, `./2`, etc.) for inner navigation
- Each item must have `label`, `url`, and `iconSvgName`
- Use Phosphor icon format: `icon-name:regular`

For the full API of `eui-sidebar-menu` (inputs, outputs, events), retrieve documentation from the EUI MCP Compodoc tool by querying `EuiSidebarMenuComponent`.

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### Layout Rules

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: breadcrumb → header (with sub-label, actions, body) → page-content (columns) → page-footer.
3. **Use `eui-page-columns`** inside `eui-page-content` (no `hasPreventMobileRendering` needed).
4. **Navigation column is always the first `eui-page-column`** with `label="Navigation"`, `euiSize2XL`, `isCollapsible`, and `hasSidebarMenu`.
5. **Main column is always the second `eui-page-column`** with a descriptive `label` (e.g., "Contract details", "Settings", "Main").
6. **Use `ChangeDetectionStrategy.OnPush`** on the component.
7. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_SIDEBAR_MENU`).
8. **Retrieve all component APIs** (imports, inputs, outputs) from the EUI MCP Compodoc tool at generation time.

### Page Header Rules

9. **Bind the page header `label`** dynamically to the data signal when applicable, or use a static string.
10. **Use `[isCollapsible]="true"`** on the page header to allow collapsing the header body.
11. **Use `eui-page-header-sub-label`** for inline metadata (category badge, status chip, owner/supplier text).
12. **Use conditional chip directives** (`[euiSuccess]`, `[euiWarning]`, `[euiDanger]`, `[euiInfo]`) for status indicators.
13. **Place the expandable metadata card** inside `eui-page-header-body` using `eui-card` with a `eui-card-header-subtitle`.
14. **Use a responsive grid** (`row` + `col-xxxl-3 col-xxl-4 col-xl-6`) for metadata fields in the header body.
15. **Implement show more/less** with a `signal(false)` toggle and `@if` block for additional fields.
16. **Apply the full Page Header Pattern rules** from the eUI Skills (see [Cross-References](#cross-references)).

### Sidebar Navigation Rules

17. **Use `eui-sidebar-menu`** with `[items]` bound to an `EuiMenuItem[]` array.
18. **Always include `hasIcons` and `hasCollapsedInitials`** on the sidebar menu.
19. **Define menu items** with `label`, `url` (relative), and `iconSvgName` (Phosphor format).
20. **Use relative URLs** (`./`, `./2`, etc.) for navigation items.

### Main Column Content Rules (Pluggable)

21. **The main column body is content-agnostic.** Choose the content type based on user requirements.
22. **For detail cards**: use stacked `eui-card` components separated by `eui-u-mt-l`, with `col-md-6` grid for field/value pairs.
23. **For forms**: wrap form controls in `eui-card` sections, use `euiInputGroup` + `euiLabel` + `euiInputText`/`euiSelect`, bind with `[ngModel]` and signal setters.
24. **For data tables**: wrap in `div.eui-table__scrollable-wrapper`, bind with `[data]` and `[paginator]`, use `euiTemplate` directives, add `isTableResponsive`.
25. **For dashboards**: use responsive grid (`row` + `col-md-4`) with KPI cards.
26. **Always include an empty state** (no-data template for tables, text paragraphs for empty card sections).

### Footer Rules

27. **Apply the full Page Footer Pattern rules** from the eUI Skills (see [Cross-References](#cross-references)).
28. **Use `eui-page-footer`** with a flex container for multi-zone layout.
29. **Left zone** contains tertiary actions (`euiBasicButton`).
30. **Right zone** contains secondary and primary actions.
31. **Use `eui-u-flex-justify-content-end`** for right-aligning the footer container.

### Accessibility

32. All icon-only buttons must have `aria-label`.
33. Breadcrumb home item must have `ariaLabel="Home"`.
34. Dropdown triggers must have `[attr.aria-label]`.
35. Each dropdown action item must have `aria-label`.
36. Action buttons with icons should include visible text labels alongside icons.

### Component API Retrieval

37. **All EUI component APIs** (selectors, inputs, outputs, import paths) must be retrieved at generation time from the **EUI MCP Compodoc tool** — not from hardcoded values in this document.
38. **Query the EUI MCP Compodoc tool** using the component names listed in the [Component Documentation Sources](#component-documentation-sources) table above.
