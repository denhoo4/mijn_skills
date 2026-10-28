---
name: Simple Layout Pattern — Canonical Structure Reference
description: Canonical reference for the EUI Simple Layout design pattern — a single-column page layout with breadcrumb, page header with actions, a pluggable content area, and a page footer. Covers layout rules, component hierarchy, MCP retrieval strategy, and accessibility guidelines. No inline code samples — all component APIs must be retrieved from the MCP EUI Compodoc tool.
label: simple-layout-pattern
category: pattern
applies-to: simple single-column page layout with breadcrumb, page header, pluggable content, and page footer
triggered-when: generating a simple layout page that displays any single-column content (forms, tables, cards, text, dashboards, etc.)
requires: EUI page components, eui-button, eui-icon, eui-dropdown, EuiGrowlService, PAGE_HEADER_PATTERN (eUI Skill), PAGE_FOOTER_PATTERN (eUI Skill)
outputs: a single-column page following the Simple Layout pattern with pluggable content area
related-skills: COLUMNS_LAYOUT_PATTERN, FLUID_LAYOUT_PATTERN, NAVIGATION_LAYOUT_PATTERN, PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN
---

# EUI Simple Layout Pattern — Canonical Structure Reference

## Purpose

This document describes the **Simple Layout** design pattern — a single-column page layout used across EUI-based applications. It serves as the canonical reference for AI code generation.

### What is this pattern?

The Simple Layout pattern represents the **simplest page structure** in the EUI framework — a single column with:

- **Page breadcrumb** — navigation trail showing the user's location
- **Page header** — title, optional subtitle, and action buttons (follows the PAGE_HEADER_PATTERN eUI Skill)
- **Page content** — a **pluggable** area that can host any content: tables, forms, cards, lists, dashboards, charts, custom components, etc.
- **Page footer** — action bar with left/right zones (follows the PAGE_FOOTER_PATTERN eUI Skill)

### Key Differentiator from Other Layouts

Unlike the Columns, Navigation, or Fluid layouts, the Simple Layout uses **no multi-column structure** and no `eui-page-columns`. All content flows in a single vertical column within `eui-page-content`.

---

## Recommended Usage

Use this pattern when:

- A page needs a straightforward single-column layout
- No sidebar, navigation menu, filter panel, or detail panel is needed
- The content area hosts a single primary content block (form, table, dashboard, etc.)
- A Create/Edit form page with footer actions is needed
- A settings page with a single section is needed
- A detail/view page without sidebar navigation is needed
- A documentation page without navigation is needed
- A data table page without a filter sidebar is needed

**Do not use** when:
- A filter sidebar is needed alongside the content (use Columns Layout)
- A persistent navigation menu is needed (use Navigation Layout)
- A resizable detail/preview panel is needed (use Fluid Layout)
- Multi-column structure is required for any reason

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
│  │ 2. PAGE HEADER               │ 3. PAGE HEADER ACTIONS             │  │
│  │    Title / Sub-title         │    [Secondary] [Primary] [▼ More]  │  │
│  └──────────────────────────────┴────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 4. PAGE CONTENT                                                   │  │
│  │                                                                   │  │
│  │    ┌───────────────────────────────────────────────────────────┐  │  │
│  │    │                                                           │  │  │
│  │    │         << PLUGGABLE CONTENT >>                           │  │  │
│  │    │                                                           │  │  │
│  │    │  Any content: tables, forms, cards, lists, dashboards,    │  │  │
│  │    │  custom components, text, charts, etc.                    │  │  │
│  │    │                                                           │  │  │
│  │    └───────────────────────────────────────────────────────────┘  │  │
│  │                                                                   │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 5. PAGE FOOTER                                                    │  │
│  │    [Cancel]                          [Secondary] [Primary]        │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Breadcrumb | See **PAGE_HEADER_PATTERN** eUI Skill | No | Navigation trail. Part of the page header pattern — breadcrumb structure, rules, and accessibility are defined in the PAGE_HEADER_PATTERN eUI Skill. |
| 2 | Page Header | See **PAGE_HEADER_PATTERN** eUI Skill | Yes | Page title, optional subtitle, and action items. Follow the Simple or Advanced variant of the Page Header pattern as appropriate. Retrieve the full pattern from the PAGE_HEADER_PATTERN eUI Skill for structure, rules, and MCP retrieval strategy. |
| 3 | Page Header Actions | See **PAGE_HEADER_PATTERN** eUI Skill | No | Right-aligned action buttons and optional overflow dropdown. Defined as part of the Page Header pattern. |
| 4 | Page Content | `eui-page-content` | Yes | Single-column free-form content area. Accepts any pluggable content: tables, forms, cards, lists, dashboards, custom components, text, charts, etc. |
| 5 | Page Footer | See **PAGE_FOOTER_PATTERN** eUI Skill | No | Action bar with left and right zones. Follow the Simple variant of the Page Footer pattern. Retrieve the full pattern from the PAGE_FOOTER_PATTERN eUI Skill for structure, rules, and MCP retrieval strategy. |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── eui-page-breadcrumb
│   └── eui-breadcrumb
│       └── eui-breadcrumb-item (×N)
├── eui-page-header [label][subLabel]
│   └── eui-page-header-action-items
│       ├── button[euiButton][euiSecondary]
│       ├── button[euiButton][euiPrimary]
│       └── eui-dropdown (optional overflow)
│           ├── button[euiButton][euiPrimary][euiOutline] + eui-icon-svg
│           └── eui-dropdown-content
│               └── button[euiDropdownItem] (×N)
├── eui-page-content
│   └── ⟨⟨ PLUGGABLE CONTENT ⟩⟩
│       Any content: tables, forms, cards, lists, dashboards,
│       custom components, text, charts, etc.
└── eui-page-footer
    └── ⟨⟨ PAGE FOOTER — see PAGE_FOOTER_PATTERN eUI Skill (Simple variant) ⟩⟩
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

#### Page Header Components

> **Refer to the PAGE_HEADER_PATTERN eUI Skill** for the full component hierarchy, MCP retrieval strategy, and generation rules for the page header. Use the **Simple** variant for basic title/subtitle with up to two action buttons, or the **Advanced** variant for collapsible headers with metadata, tags, and overflow actions.

#### Page Footer Components

> **Refer to the PAGE_FOOTER_PATTERN eUI Skill** for the full component hierarchy, MCP retrieval strategy, and generation rules for the page footer. Use the **Simple** variant for always-visible footer actions.

#### Breadcrumb Components

> **Refer to the PAGE_HEADER_PATTERN eUI Skill** for breadcrumb usage, which is part of the Page Header pattern.

#### UI Components (for overflow dropdown in header actions)

| Tool Call | Component Name | Purpose |
|-----------|---------------|---------|
| `get_component_docs` | `EuiDropdownComponent` | Overflow actions menu in header |
| `get_component_docs` | `EuiGrowlService` | Growl notifications for action feedback |

### Retrieval Strategy

1. **Before writing any component code**, call `get_component_docs` for each EUI component used in the pattern.
2. **For inputs/outputs details**, call `get_component_inputs` and `get_component_outputs` on the primary components (EuiPageComponent, EuiPageContentComponent).
3. **For usage examples**, call `get_component_examples` on the main layout components (EuiPageComponent).
4. **Use `search_components`** if you need to find related components by keyword.
5. **For accessibility requirements**, call `get_component_accessibility` on interactive components.
6. **For the page header**, follow the MCP Retrieval Strategy in the **PAGE_HEADER_PATTERN eUI Skill** (Simple or Advanced variant).
7. **For the page footer**, follow the MCP Retrieval Strategy in the **PAGE_FOOTER_PATTERN eUI Skill** (Simple variant).

---

## Pluggable Content Area

The `eui-page-content` zone is **content-agnostic**. It accepts any content that fits within a single-column layout. Common content types include:

| Content Type | Key EUI Components | When to Use |
|-------------|-------------------|-------------|
| Data table | `eui-table`, `eui-paginator`, `eui-table-filter`, `eui-badge` | Displaying structured tabular data with sort, filter, pagination |
| Form | `eui-input-text`, `eui-select`, `eui-textarea`, `eui-input-checkbox` | Create/Edit entity pages |
| Cards list | `eui-card`, `eui-card-header`, `eui-card-content` | Displaying items as visual card blocks |
| Dashboard | Custom components, charts, summary cards | Overview/landing pages |
| Text/Documentation | HTML content, markdown rendering | Static content pages |

### Content-Specific MCP Retrieval

When the content area includes specific EUI components, retrieve their documentation before generating code:

| Content Type | Additional Tool Calls |
|-------------|----------------------|
| Data table | `get_component_docs("EuiTableComponent")`, `get_component_docs("EuiPaginatorComponent")`, `get_component_docs("EuiBadgeComponent")` |
| Form | `get_component_docs("EuiInputTextComponent")`, `get_component_docs("EuiSelectComponent")` |
| Cards list | `get_component_docs("EuiCardComponent")`, `get_component_docs("EuiCardHeaderComponent")` |

---

## Required Angular Imports

> **Do not hardcode import paths.** Retrieve the correct module/token imports by calling `get_component_docs` for each component. The response includes the `imports` field with the proper module tokens.

### Base Import Tokens (Simple Layout Structure)

The following EUI tokens form the minimum required imports for the Simple Layout structure. Use `get_component_docs` to confirm exact import paths:

| Token | Package | Usage |
|-------|---------|-------|
| `EUI_PAGE` | `@eui/components/eui-page` | Page layout structure (eui-page, eui-page-content, eui-page-footer) |
| `EUI_BREADCRUMB` | `@eui/components/eui-breadcrumb` | Breadcrumb navigation |
| `EUI_BUTTON` | `@eui/components/eui-button` | Action buttons (header + footer) |
| `EUI_ICON` | `@eui/components/eui-icon` | Icon SVGs |
| `EUI_DROPDOWN` | `@eui/components/eui-dropdown` | Overflow actions menu (optional) |

> **For Page Header imports**: see PAGE_HEADER_PATTERN eUI Skill — "Required Angular Imports" section (Simple or Advanced variant).
> **For Page Footer imports**: see PAGE_FOOTER_PATTERN eUI Skill — "Required Angular Imports" section.

### Additional Imports for Pluggable Content

Add these tokens based on what content is placed inside `eui-page-content`:

| Content Type | Additional Tokens |
|-------------|-------------------|
| Data table | `EUI_TABLE`, `EUI_PAGINATOR`, `EUI_BADGE`, `EUI_LABEL`, `EuiTemplateDirective`, `DecimalPipe` |
| Form | `EUI_INPUT_TEXT`, `EUI_SELECT`, `EUI_INPUT_GROUP`, `EUI_LABEL`, `FormsModule` or `ReactiveFormsModule` |
| Cards list | `EUI_CARD`, `EUI_CHIP` |

### Angular Core Imports

- `ChangeDetectionStrategy`, `Component`, `inject`, `signal`, `viewChild` from `@angular/core`
- `DecimalPipe` from `@angular/common` (if using number formatting)
- `EuiGrowlService` from `@eui/core` (for action notifications)

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### Pre-Generation Step (MCP Tool Retrieval)

0. **Before writing any code**, call the MCP EUI Compodoc tool to retrieve documentation for all components listed in the "Required Tool Calls" section above. Use the retrieved inputs, outputs, and examples as the authoritative source for component APIs.

### Layout Rules

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: breadcrumb → header → page-content → page-footer.
3. **Use `eui-page-content` directly** for the content area — do **not** use `eui-page-columns`.
4. **Page header** — follow the **PAGE_HEADER_PATTERN eUI Skill** (Simple or Advanced variant) for the header structure, rules, and required imports. Use the Simple variant for basic title/subtitle with up to two buttons; use the Advanced variant for collapsible headers with metadata, tags, and overflow actions.
5. **Page footer** — follow the **PAGE_FOOTER_PATTERN eUI Skill** (Simple variant) for the footer structure, rules, and required imports. Use the Simple variant for always-visible page actions.
6. **Use `ChangeDetectionStrategy.OnPush`** on the component.
7. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_BUTTON`).
8. **Use `inject()`** for service injection (e.g., `EuiGrowlService`).
9. **Use Angular signals** (`signal()`, `computed()`) for reactive state management.

### Content Area Rules

10. **The content area is pluggable** — place any appropriate content inside `eui-page-content` based on requirements.
11. **Retrieve component documentation** from MCP tools (`get_component_docs`) for any content-specific EUI components before generating their markup.
12. **Do not hardcode content type** — the Simple Layout is content-agnostic and works with any single-column content.

### Accessibility

13. All icon-only buttons must have `aria-label` or `euiTooltip`.
14. Breadcrumb home item must have `ariaLabel="Home"` (see PAGE_HEADER_PATTERN eUI Skill for full breadcrumb accessibility rules).
15. Dropdown triggers must have `[attr.aria-label]`.
16. Use `<span euiLabel>` for button text that accompanies icons.
17. Each dropdown action item must have `aria-label`.
18. **Retrieve accessibility docs** via `get_component_accessibility` for each interactive component to ensure compliance.
19. **For page header accessibility**, follow the accessibility rules in the PAGE_HEADER_PATTERN eUI Skill.
20. **For page footer accessibility**, follow the accessibility rules in the PAGE_FOOTER_PATTERN eUI Skill.

---

## Related Pattern Documentation (eUI Skills)

This pattern delegates the page header and page footer to their own canonical pattern files, maintained as part of the **eUI Skills** library. When implementing a Simple Layout, always consult these companion patterns:

| Pattern | eUI Skill Name | Usage in Simple Layout |
|---------|---------------|------------------------|
| **PAGE_HEADER_PATTERN** | `PAGE_HEADER_PATTERN` (eUI Skill) | Defines the page header structure (breadcrumb, title, subtitle, action items). Use the **Simple** variant for basic title/subtitle with up to two buttons, or the **Advanced** variant for collapsible headers with metadata, tags, and overflow dropdown. |
| **PAGE_FOOTER_PATTERN** | `PAGE_FOOTER_PATTERN` (eUI Skill) | Defines the page footer structure at the bottom of `eui-page`. Use the **Simple** variant with left-zone dismissive actions and right-zone affirmative actions. |

### How to Use the Companion Patterns

1. **Page Header**: Retrieve the PAGE_HEADER_PATTERN from the eUI Skills library. Place the header structure as a direct child of `eui-page`. The pattern includes its own MCP retrieval strategy, component hierarchy, generation rules, and accessibility requirements.
2. **Page Footer**: Retrieve the PAGE_FOOTER_PATTERN from the eUI Skills library. Place the footer structure as the last child of `eui-page`. The pattern includes its own MCP retrieval strategy, flexbox layout rules, generation rules, and accessibility requirements.

---

## Comparison with Other Layout Patterns

| Feature | **Simple Layout** | Columns Layout | Navigation Layout | Fluid Layout |
|---------|-------------------|----------------|-------------------|--------------|
| Columns | 1 | 2 (flat) | 2 (sidebar + main) | 2+ (nested + panel) |
| Filter sidebar | ❌ | ✅ | ❌ | ✅ |
| Sidebar navigation | ❌ | ❌ | ✅ | ❌ |
| Multi-select | ❌ | Optional | ❌ | ✅ |
| Dimmer effect | ❌ | ❌ | ❌ | ✅ |
| Bulk actions footer | ❌ | Optional | ❌ | ✅ |
| Resizable panel | ❌ | ❌ | ❌ | ✅ |
| Pluggable content | ✅ | ✅ | ✅ | ✅ |
| Display mode toggle | ❌ | ❌ | ❌ | ✅ |
| Detail preview panel | ❌ | ❌ | ❌ | ✅ |
| Complexity | Low | Medium | Medium | High |
| Use case | Forms, tables, settings, details | Search + filters + results | Multi-section settings, admin | Master-detail, entity browser |
