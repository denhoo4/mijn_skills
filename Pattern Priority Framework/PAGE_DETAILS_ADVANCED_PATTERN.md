---
name: Page Details Advanced Pattern — AI Sample
description: AI-generated self-contained advanced detail page with two-column layout, sidebar navigation menu, header summary card, dropdown actions, dimmer highlight, inline reactive form, edit/read-only toggle, and conditional footer actions. Use when generating an advanced detail/edit page with sidebar menu, columns layout, and inline reactive form. Requires eUI page components, eui-page-columns, eui-sidebar-menu, EuiAppShellService, AsyncPipe, reactive forms, EuiGrowlService, EuiMessageBoxComponent. Applies to page-details advanced layout with sidebar navigation and inline reactive forms. Related patterns PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN, PAGE_DETAILS_SIMPLE_PATTERN, NAVIGATION_LAYOUT, COLUMNS_LAYOUT.
---

# EUI Page Details Advanced Pattern — AI Sample (Self-Contained)

## Purpose

A two-column detail page with a **sidebar navigation menu** on the left and a **fully self-contained inline reactive form** on the right. The page includes a collapsible header with summary card, action buttons with overflow dropdown, and a conditional footer that appears in edit mode.

---

## Recommended Usage

Use this pattern when:

- The page requires a **sidebar navigation menu** to navigate between form sections or related sub-pages
- A **summary card** in the page header provides at-a-glance metadata about the record
- Multiple action buttons are needed in the header (toggle mode, save, more actions dropdown)
- The form content is extensive and benefits from a columns layout with navigation
- The `EuiAppShellService` dimmer state should highlight the main content column
- A self-contained component without external dependencies is preferred

---

## Page Header

This pattern uses the **Advanced Page Header** variant. Refer to the **PAGE_HEADER_PATTERN** skill for full canonical structure, rules, and MCP retrieval strategy.

Key header features in this pattern:

- Collapsible header with `[isCollapsible]="true"` and `[isCollapsed]="false"`
- `eui-page-header-body` containing a summary card with responsive key-value grid using Bootstrap Grid System
- `eui-page-header-action-items` with toggle edit button, save button, and "More" dropdown (Label-icon variant)
- Breadcrumb navigation via `eui-page-breadcrumb`

Retrieve header component documentation via MCP:

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageHeaderComponent` | Page header: `label`, `subLabel`, `isCollapsible`, `isCollapsed`, `expandedLabel`, `collapsedLabel`, `collapse` output |
| `get_component_docs` | `EuiPageBreadcrumbComponent` | Breadcrumb container |
| `get_component_docs` | `EuiBreadcrumbComponent` | Breadcrumb navigation |
| `get_component_docs` | `EuiBreadcrumbItemComponent` | Item inputs: `link`, `label`, `iconSvgName`, `ariaLabel` |
| `get_component_docs` | `EuiPageHeaderSubLabelComponent` | Sub-label container for metadata |
| `get_component_docs` | `EuiPageHeaderActionItemsComponent` | Action items container |
| `get_component_docs` | `EuiPageHeaderBodyComponent` | Collapsible body area |

---

## Page Footer

This pattern uses a **conditional footer** that appears only in edit mode. Refer to the **PAGE_FOOTER_PATTERN** skill for full canonical structure, rules, and MCP retrieval strategy.

Key footer features in this pattern:

- Conditionally rendered with `@if (isEditActive())`
- Uses `euiHighlighted="true"` for visual distinction
- Left side: Reset button (plain `euiButton`)
- Right side: Delete (`euiDanger`) + Cancel (`euiSecondary`) + Submit (`euiPrimary`)
- Flexbox layout with `eui-u-flex eui-u-flex-gap-m` outer wrapper and `eui-u-flex-justify-content-end eui-u-flex-gap-s` for right content

Retrieve footer component documentation via MCP:

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageFooterComponent` | Footer container with `euiHighlighted` support |
| `get_component_docs` | `EuiGrowlService` | Toast notifications for action feedback |

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                     │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ 1. PAGE BREADCRUMB                                                    │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ 2. PAGE HEADER  [label][subLabel][isCollapsible]                      │  │
│  │  ┌──────────────────────────────────────────────────────────────────┐ │  │
│  │  │ 3. PAGE HEADER ACTION ITEMS                                      │ │  │
│  │  │  [Toggle edit/read-only] [Save] [More ▾ (Export,Duplicate,       │ │  │
│  │  │                                         Archive,Delete)]         │ │  │
│  │  └──────────────────────────────────────────────────────────────────┘ │  │
│  │  ┌──────────────────────────────────────────────────────────────────┐ │  │
│  │  │ 4. PAGE HEADER BODY — Summary Card (Bootstrap Grid)              │ │  │
│  │  │  ┌──────────────────────────────────────────────────────────┐    │ │  │
│  │  │  │ row                                                      │    │ │  │
│  │  │  │  col-xl-3 col-lg-6 col-md-6 (×N key-value pairs)        │    │ │  │
│  │  │  │  ┌────────────┬────────────┬────────────┬────────────┐   │    │ │  │
│  │  │  │  │ Key/Value  │ Key/Value  │ Key/Value  │ Key/Value  │   │    │ │  │
│  │  │  │  │ (plain/    │ (plain/    │ (plain/    │ (plain/    │   │    │ │  │
│  │  │  │  │  badge)    │  badge)    │  badge)    │  badge)    │   │    │ │  │
│  │  │  │  └────────────┴────────────┴────────────┴────────────┘   │    │ │  │
│  │  │  └──────────────────────────────────────────────────────────┘    │ │  │
│  │  └──────────────────────────────────────────────────────────────────┘ │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ 5. PAGE CONTENT — eui-page-columns                                    │  │
│  │  ┌──────────────────┬────────────────────────────────────────────┐   │  │
│  │  │ 6. LEFT COLUMN   │ 7. RIGHT COLUMN (Main)                     │   │  │
│  │  │  (Navigation)    │  ┌──────────────────────────────────────┐   │   │  │
│  │  │                  │  │ Column Header: [Cancel] [Submit]     │   │   │  │
│  │  │ [← Back to list] │  └──────────────────────────────────────┘   │   │  │
│  │  │                  │  ┌──────────────────────────────────────┐   │   │  │
│  │  │ ▸ Section 1      │  │ INLINE FORM (self-contained)         │   │   │  │
│  │  │ ▸ Section 2      │  │                                      │   │   │  │
│  │  │ ▸ Section 3      │  │  form[formGroup]                     │   │   │  │
│  │  │ ▸ Section 4      │  │  ├── eui-fieldset "Personal info"    │   │   │  │
│  │  │ ▸ Section 5      │  │  │   (expanded, Bootstrap rows)      │   │   │  │
│  │  │                  │  │  └── eui-fieldset "Financial info"    │   │   │  │
│  │  │                  │  │      (collapsed, Bootstrap rows)      │   │   │  │
│  │  │                  │  └──────────────────────────────────────┘   │   │  │
│  │  └──────────────────┴────────────────────────────────────────────┘   │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ 8. PAGE FOOTER (conditional — edit mode only) [euiHighlighted]        │  │
│  │  [Reset]                              [Delete]  [Cancel]  [Submit]    │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────────┘
  ┌───────────────────────────────────────────────────────────────────────┐
  │ eui-message-box — Confirmation dialog for destructive actions          │
  └───────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` | No | Navigation breadcrumb trail. |
| 2 | Page Header | `eui-page-header` [label, subLabel, isCollapsible] | Yes | Collapsible page header with title and sub-title. Contains action items and a summary card body. |
| 3 | Header Action Items | `eui-page-header-action-items` | Yes | Toggle edit mode button (`euiSecondary`), Save button (`euiPrimary`), and "More" dropdown (`euiPrimary euiOutline`, Label-icon variant) with overflow actions. |
| 4 | Header Body Card | `eui-page-header-body` > `eui-card` > `eui-card-content` | No | Summary card with key-value pairs displayed in a responsive Bootstrap grid (`row` > `col-xl-3 col-lg-6 col-md-6`). Values may include `euiBadge` directives with status semantics. |
| 5 | Page Content | `eui-page-content` > `eui-page-columns` | Yes | Container for the two-column layout. |
| 6 | Left Column (Navigation) | `eui-page-column` [euiSize2XL, isCollapsible, hasSidebarMenu] | Yes | Collapsible sidebar with a "Back to list" button (`euiBlockButton euiOutline`) in the column header body and `eui-sidebar-menu` in the column body. |
| 7 | Right Column (Main) | `eui-page-column` [euiHighlighted] | Yes | Main content area. Header right content has Cancel/Submit buttons (`euiSizeS`). Body contains the inline reactive form with expandable fieldsets. Uses `(asService.state$ | async)?.isDimmerActive` for highlight state. |
| 8 | Page Footer | `eui-page-footer` [euiHighlighted="true"] | No | Conditionally shown in edit mode. Left: Reset. Right: Delete (`euiDanger`) + Cancel (`euiSecondary`) + Submit (`euiPrimary`). See **PAGE_FOOTER_PATTERN**. |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── eui-page-breadcrumb
│   └── eui-breadcrumb
│       ├── eui-breadcrumb-item [link="/"][iconSvgName="eui-home"][ariaLabel="Home"]
│       ├── eui-breadcrumb-item [label][link]
│       └── eui-breadcrumb-item [label]  ← current page (no link)
├── eui-page-header [label][subLabel][isCollapsible][isCollapsed=false][expandedLabel][collapsedLabel]
│   ├── eui-page-header-action-items
│   │   ├── button[euiButton][euiSecondary]  ← Toggle edit mode (dynamic label)
│   │   ├── button[euiButton][euiPrimary]    ← Save
│   │   └── eui-dropdown
│   │       ├── button[euiButton][euiPrimary][euiOutline][euiTooltip="More actions"]
│   │       │   ├── span[euiLabel]
│   │       │   └── eui-icon-svg[icon="eui-ellipsis-vertical"]
│   │       └── eui-dropdown-content
│   │           └── button[euiDropdownItem] (×N)  ← overflow actions
│   └── eui-page-header-body
│       └── eui-card
│           └── eui-card-content
│               └── div.row > div.col-xl-3.col-lg-6.col-md-6 (×N)
│                   ├── div.eui-u-pv-xs
│                   │   ├── div.eui-u-c-neutral-dark.eui-u-f-s  ← key label
│                   │   └── div.eui-u-f-bold  ← value (plain text or euiBadge)
├── eui-page-content
│   └── eui-page-columns
│       ├── eui-page-column [label="Navigation menu"][euiSize2XL][isCollapsible][hasSidebarMenu]
│       │   ├── eui-page-column-header-body
│       │   │   └── button[euiButton][euiPrimary][euiOutline][euiBlockButton]
│       │   │       ├── eui-icon-svg[icon="eui-chevron-left"]
│       │   │       └── span[euiLabel] "Back to list"
│       │   └── eui-page-column-body
│       │       └── eui-sidebar-menu [items] hasIcons hasCollapsedInitials
│       └── eui-page-column [label="Main"][euiHighlighted]="(asService.state$ | async)?.isDimmerActive"
│           ├── eui-page-column-header-right-content
│           │   └── div.eui-u-flex.eui-u-flex-gap-s
│           │       ├── button[euiButton][euiSecondary][euiSizeS] ← Cancel
│           │       └── button[euiButton][euiPrimary][euiSizeS]   ← Submit
│           └── eui-page-column-body
│               └── form[formGroup]
│                   ├── eui-fieldset [label][iconSvgName][isExpandable][isExpanded=true][isFirst]
│                   │   └── (form rows using Bootstrap Grid — see Form Layout section)
│                   └── eui-fieldset [label][iconSvgName][isExpandable][isExpanded=false]
│                       └── (form rows using Bootstrap Grid — see Form Layout section)
├── @if (isEditActive())
│   └── eui-page-footer [euiHighlighted="true"]
│       └── div.eui-u-flex.eui-u-flex-gap-m
│           ├── div.eui-u-flex.eui-u-flex-gap-s  ← Left: Reset
│           └── div.eui-u-flex.eui-u-flex-justify-content-end.eui-u-flex-gap-s  ← Right: Delete, Cancel, Submit
└── eui-message-box #messageBox [title="Confirm deletion"]
```

---

## Form Layout — Bootstrap Grid System

All form field rows inside fieldsets use the **Bootstrap Grid System** for responsive layout. This is mandatory per the eUI coding rules.

### Responsive Grid Rules for Form Fields

- Each row of form fields is wrapped in a `div.row`
- Each field occupies a column defined by `col-md-*` classes (12-column grid)
- Common responsive breakpoints used:
  - `col-md-12` — full-width single field (address, remarks)
  - `col-md-6` — half-width, two fields per row (first name + last name, city + country)
  - `col-md-4` — third-width, three fields per row (invoice ref + type + scan ref, date fields, beneficiary + amount + currency)
  - `col-md-3` — quarter-width (postal code when combined with other fields)
- Add vertical padding utility `eui-u-pv-s` on rows requiring extra vertical spacing

### Fieldset 1: Personal Information (expanded by default)

| Row | Fields | Grid Layout |
|-----|--------|-------------|
| 1 | Gender (radio group) | `col-md-6` — single field with inline radio buttons using `eui-u-flex eui-u-flex-wrap` |
| 2 | First name, Last name | `col-md-6` + `col-md-6` — two fields with `euiInputGroupAddOn` icon |
| 3 | Address | `col-md-12` — full-width single field with `euiInputGroupAddOn` icon |
| 4 | Postal code, City | `col-md-6` + `col-md-6` — number input + native select with `euiInputGroupAddOn` icons |
| 5 | Country, Email | `col-md-6` + `col-md-6` — autocomplete + text input with `euiInputGroupAddOn` icons and tooltip on label |
| 6 | Spoken languages (checkbox group) | `col-md-12` — inline checkboxes using `eui-u-flex eui-u-flex-wrap` with helper text |
| 7 | Remarks | Full-width textarea with `[euiMaxlength]` directive |

### Fieldset 2: Financial Information (collapsed by default)

| Row | Fields | Grid Layout |
|-----|--------|-------------|
| 1 | Invoice reference, Invoice type, Scan reference | `col-md-4` + `col-md-4` + `col-md-4` — text input + native select + native select |
| 2 | Invoice date, Start date, End date | `col-md-4` + `col-md-4` + `col-md-4` — three datepickers with `isDatepickerBlock isClearable` |
| 3 | Beneficiary, Total amount, Currency | `col-md-4` + `col-md-4` + `col-md-4` — autocomplete with add-on + number input with currency add-on suffix + native select |

### Form Field Composition Pattern

Each form field follows this structure:

1. Container: `div euiInputGroup`
2. Label: `label euiLabel` with optional `[euiRequired]="isEditActive()"` for required indicator
3. Input wrapper (when icons needed): `div euiInputGroupAddOn` containing:
   - Conditional icon add-on: `div euiInputGroupAddOnItem` > `eui-icon-svg` (shown only in edit mode via `@if`)
   - The actual input control (`euiInputText`, `euiInputNumber`, `euiSelect`, `eui-autocomplete`, `eui-datepicker`)
4. Validation feedback: `eui-feedback-message euiDanger` conditionally rendered with `@if` when field is invalid and touched
5. All inputs bind `[readonly]="!isEditActive()"` or `[isReadonly]="!isEditActive()"` (for autocomplete/datepicker)

### Input Types Used

| EUI Control | Usage | Key Attributes |
|-------------|-------|----------------|
| `input[euiInputText]` | Text fields (name, address, email, reference) | `formControlName`, `placeholder`, `[readonly]` |
| `input[euiInputNumber]` | Numeric fields (postal code, amount) | `formControlName`, `placeholder`, `[readonly]` |
| `select[euiSelect]` | Dropdown selections (city, type, currency) | `formControlName`, `placeholder`, `[readonly]`, native `option` elements with `@for` |
| `eui-autocomplete` | Searchable dropdowns (country, beneficiary) | `formControlName`, `[autocompleteData]`, `[isFreeValueAllowed]="true"`, `[isReadonly]`, `aria-label` |
| `eui-datepicker` | Date fields | `formControlName`, `isDatepickerBlock`, `isClearable`, `[isReadOnly]` |
| `input[euiInputRadio]` | Radio group (gender) | `formControlName`, `[value]`, `[readonly]`, unique `id` + matching `label[for]` |
| `input[euiInputCheckBox]` | Checkbox group (languages) | `formControlName` inside `formGroupName`, `[readonly]`, unique `id` + matching `label[for]` |
| `textarea[euiTextArea]` | Multi-line text (remarks) | `formControlName`, `[euiMaxlength]`, `placeholder`, `[readonly]` |

---

## Header Card — Bootstrap Grid for Metadata

The header body summary card uses the Bootstrap Grid System to display key-value metadata responsively:

- Container: `eui-card` > `eui-card-content` > `div.row`
- Each key-value pair occupies: `div.col-xl-3.col-lg-6.col-md-6`
- This creates a 4-column grid on XL screens, 2-column on LG/MD screens
- Each cell structure:
  - Outer: `div.eui-u-pv-xs` for vertical padding
  - Key: `div.eui-u-c-neutral-dark.eui-u-f-s` (small muted label)
  - Value: `div.eui-u-f-bold` (bold value, optionally containing `euiBadge` with semantic directives)

### Badge Semantics in Header Card

| Badge Directive | Usage |
|-----------------|-------|
| `euiBadge euiInfo` | Informational values (department, category) |
| `euiBadge euiSuccess` | Positive status (active, approved) |
| `euiBadge euiWarning` | Attention needed (grade, pending) |
| `euiBadge euiDanger` | Critical/negative values (expired, rejected) |

---

## MCP Retrieval Strategy

All component documentation, inputs, outputs, and usage examples must be retrieved from the EUI MCP Compodoc tool before generating code. The following table lists the key components used in this pattern:

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageHeaderComponent` | Page header with collapse support |
| `get_component_docs` | `EuiPageBreadcrumbComponent` | Breadcrumb container |
| `get_component_docs` | `EuiBreadcrumbComponent` | Breadcrumb navigation |
| `get_component_docs` | `EuiBreadcrumbItemComponent` | Individual breadcrumb items |
| `get_component_docs` | `EuiPageHeaderActionItemsComponent` | Header action buttons container |
| `get_component_docs` | `EuiPageHeaderBodyComponent` | Collapsible body area |
| `get_component_docs` | `EuiPageColumnsComponent` | Two-column layout container |
| `get_component_docs` | `EuiPageColumnComponent` | Individual column with collapse, sidebar, highlight |
| `get_component_docs` | `EuiSidebarMenuComponent` | Sidebar navigation menu |
| `get_component_docs` | `EuiFieldsetComponent` | Expandable form section grouping |
| `get_component_docs` | `EuiDropdownComponent` | Overflow actions menu |
| `get_component_docs` | `EuiPageFooterComponent` | Footer with `euiHighlighted` support |
| `get_component_docs` | `EuiMessageBoxComponent` | Confirmation dialog for destructive actions |
| `get_component_docs` | `EuiGrowlService` | Toast notifications for user feedback |

---

## Required Angular Imports

Retrieve via MCP `get_component_docs` for each component. The following tokens must be spread in the component `imports` array:

- `EUI_PAGE` from `@eui/components/eui-page`
- `EUI_AUTOCOMPLETE` from `@eui/components/eui-autocomplete`
- `EUI_BADGE` from `@eui/components/eui-badge`
- `EUI_BREADCRUMB` from `@eui/components/eui-breadcrumb`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EUI_CARD` from `@eui/components/eui-card`
- `EUI_DATEPICKER` from `@eui/components/eui-datepicker`
- `EUI_DROPDOWN` from `@eui/components/eui-dropdown`
- `EUI_FEEDBACK_MESSAGE` from `@eui/components/eui-feedback-message`
- `EUI_FIELDSET` from `@eui/components/eui-fieldset`
- `EUI_ICON` from `@eui/components/eui-icon`
- `EUI_INPUT_CHECKBOX` from `@eui/components/eui-input-checkbox`
- `EUI_INPUT_GROUP` from `@eui/components/eui-input-group`
- `EUI_INPUT_NUMBER` from `@eui/components/eui-input-number`
- `EUI_INPUT_RADIO` from `@eui/components/eui-input-radio`
- `EUI_INPUT_TEXT` from `@eui/components/eui-input-text`
- `EUI_LABEL` from `@eui/components/eui-label`
- `EUI_SELECT` from `@eui/components/eui-select`
- `EUI_SIDEBAR_MENU` from `@eui/components/eui-sidebar-menu`
- `EUI_TEXTAREA` from `@eui/components/eui-textarea`
- `EUI_HELPER_TEXT` from `@eui/components/eui-helper-text`
- `EuiMaxLengthDirective` from `@eui/components/directives`
- `EuiTooltipDirective` from `@eui/components/directives`
- `EuiMessageBoxComponent` from `@eui/components/eui-message-box`
- `AsyncPipe` from `@angular/common`
- `ReactiveFormsModule` from `@angular/forms`

---

## Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-home` | `eui-breadcrumb-item` | Breadcrumb home item |
| `eui-ellipsis-vertical` | `eui-icon-svg` | "More" dropdown trigger icon |
| `eui-chevron-left` | `eui-icon-svg` | Back to list button icon |
| `eui-state-info` | `eui-icon-svg` | Info tooltip icon on labels |
| `eui-email` | `eui-icon-svg` | Email input add-on |
| `eui-add` | `eui-icon-svg` | Add action input add-on (beneficiary) |
| `user:regular` | `eui-icon-svg` / `eui-fieldset` | Personal section icon, name field add-ons |
| `currency-eur:regular` | `eui-fieldset` | Financial section icon |
| `envelope:regular` | Sidebar menu item | Contact section icon |
| `gear:regular` | Sidebar menu item | Preferences section icon |
| `file-text:regular` | Sidebar menu item | Documents section icon |
| `globe:regular` | `eui-icon-svg` | Country field add-on |
| `circle-dashed:regular` | `eui-icon-svg` / `eui-fieldset` | Postal code / city / financial section icon |

---

## State Management

- Use `signal()` for edit/read-only mode control (`isEditActive = signal(true)`)
- The signal controls conditional rendering of input add-on icons, readonly state, required indicators, and footer visibility
- Toggle via a dedicated method that also triggers a growl notification
- `EuiAppShellService` is injected as a **public** property (`asService`) for template access to `state$`

---

## Page Actions

| Action | Behavior |
|--------|----------|
| Toggle edit/read-only | Flips `isEditActive` signal, shows info growl, button label changes dynamically |
| Back to list | Shows info growl notification |
| Save | Marks all touched, validates, shows success/danger growl |
| Submit (column header / footer) | Same as Save — validates and provides feedback |
| Cancel | Resets form, shows info growl |
| Reset (footer) | Resets form, shows info growl |
| Delete (dropdown / footer) | Opens `eui-message-box` confirmation dialog |
| Delete accept | Shows danger growl |
| Delete dismiss | Shows info growl |
| Export (dropdown) | Shows info growl |
| Duplicate (dropdown) | Shows info growl |
| Archive (dropdown) | Shows warning growl |

---

## Fieldset Configuration

| Fieldset | Label | Icon | Expandable | Initially Expanded | Position |
|----------|-------|------|------------|-------------------|----------|
| Personal information | "Personal information" | `user:regular` | Yes | Yes (`isExpanded="true"`) | First (`isFirst`) |
| Financial information | "Financial informations" | `circle-dashed:regular` | Yes | Yes (`isExpanded="true"`) | Subsequent (with `eui-u-mt-m` spacing) |

Each fieldset may include a `euiFieldsetLabelExtraContent` containing a secondary badge with tooltip for contextual help.

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### Self-Contained Rules

1. **Keep everything self-contained** — no external shared folder imports. All validators, options, and logic are inline.
2. **Use `signal()`** for edit/read-only mode control.
3. **Use `FormBuilder`** with `FormGroup` and define all controls in a single `buildForm()` method.
4. **Group form fields into `eui-fieldset` sections** with `isExpandable`. Primary sections expanded, secondary collapsed.
5. **Use `eui-feedback-message euiDanger`** for validation errors, rendered conditionally with `@if`.
6. **Use `euiInputGroupAddOn` with `euiInputGroupAddOnItem`** for field icons, conditionally shown only in edit mode via `@if (isEditActive())`.
7. **Use `ChangeDetectionStrategy.OnPush`**.
8. **Provide `provideMomentDateAdapter(DEFAULT_FORMATS)`** in providers when using datepickers.

### Bootstrap Grid System Rules (Mandatory)

9. **Always use Bootstrap Grid System** (`row`, `col-md-*`, `col-lg-*`, `col-xl-*`) for responsive form field layout inside fieldsets.
10. **Never use custom flex-based grid alternatives** when Bootstrap grid classes are available.
11. **Common column patterns**: `col-md-6` for two fields per row, `col-md-4` for three fields per row, `col-md-12` for full-width fields.
12. **Header card metadata** must use `row` > `col-xl-3 col-lg-6 col-md-6` for a 4/2/2-column responsive grid.
13. **Add `eui-u-pv-s` utility** on rows that require extra vertical spacing between field groups.
14. **Never add or use custom CSS/SCSS** — only eUI utility classes and Bootstrap grid.
15. **Never use inline styles** — use eUI utility classes (`eui-u-*`) or Bootstrap grid classes.

### Advanced Layout Rules

16. **Use `eui-page-columns`** inside `eui-page-content` to create a two-column layout.
17. **Left column** must use `euiSize2XL`, `isCollapsible`, and `hasSidebarMenu` attributes.
18. **Left column header body** should contain a "Back to list" button with `euiBlockButton`, `euiOutline`, a left chevron icon, and a growl notification action.
19. **Left column body** must contain `eui-sidebar-menu` with `[items]`, `hasIcons`, and `hasCollapsedInitials`.
20. **Sidebar menu items** must be an `EuiMenuItem[]` array with `label`, `url`, and `iconSvgName` for each entry.
21. **Right column** must bind `[euiHighlighted]` to `(asService.state$ | async)?.isDimmerActive`.
22. **Right column header** should use `eui-page-column-header-right-content` with small action buttons (`euiSizeS`) in a flex container (`eui-u-flex eui-u-flex-gap-s`).
23. **Inject `EuiAppShellService`** as a public property (`asService`) for template access to `state$`.
24. **Import `AsyncPipe`** in the component imports array for the `| async` pipe usage.

### Header Rules (see PAGE_HEADER_PATTERN for full details)

25. **Page header** must use `[isCollapsible]="true"` and include a `eui-page-header-body` with a summary card.
26. **Header card** must use `eui-card` > `eui-card-content` with a responsive Bootstrap grid (`row` > `col-xl-3 col-lg-6 col-md-6`) for key-value pairs.
27. **Key-value pair structure**: `div.eui-u-pv-xs` > key (`div.eui-u-c-neutral-dark.eui-u-f-s`) + value (`div.eui-u-f-bold`, optionally with `euiBadge`).
28. **Header action items** must include: toggle edit button (`euiSecondary`), primary save button (`euiPrimary`), and a "More" dropdown with overflow actions using the Label-icon variant.
29. **Dropdown trigger** must use `euiPrimary euiOutline euiTooltip="More actions"` with `[attr.aria-label]`, containing `span[euiLabel]` + `eui-icon-svg[icon="eui-ellipsis-vertical"]`.

### Footer Rules (see PAGE_FOOTER_PATTERN for full details)

30. **Footer** must use `euiHighlighted="true"` attribute when visible.
31. **Footer is conditional** (`@if (isEditActive())`) — hidden in read-only mode.
32. **Footer layout** uses `eui-u-flex eui-u-flex-gap-m` outer wrapper with left and right zones.
33. **Footer button hierarchy**: Reset (plain `euiButton`), Delete (`euiDanger`), Cancel (`euiSecondary`), Submit (`euiPrimary`).
34. **Include `eui-message-box`** for destructive actions (delete) with accept/dismiss handlers.
35. **Use `EuiGrowlService`** for all user feedback notifications.
36. **Include `eui-page-breadcrumb`** with breadcrumb items for navigation context.

### Form Field Rules

37. **Use native `select[euiSelect]`** with native `option` elements for dropdown fields (not `eui-select` > `eui-option`).
38. **Use `eui-autocomplete`** with `[autocompleteData]` (not `[options]`) and `[isFreeValueAllowed]="true"` for searchable fields.
39. **Use `[euiRequired]="isEditActive()"`** on labels to conditionally show the required indicator.
40. **Use `[readonly]="!isEditActive()"`** on native inputs and `[isReadonly]="!isEditActive()"` on autocomplete/datepicker.
41. **Radio inputs** must use `formControlName` on each input with unique `id` and matching `label[for]`, rendered inline with `eui-u-flex eui-u-flex-wrap`.
42. **Checkbox groups** must use a nested `FormGroup` with `formGroupName`, individual `formControlName` per checkbox, with a custom group validator.
43. **Use `eui-helper-text`** below labels for contextual guidance text (e.g., "Select at least one language").
44. **Use `euiTooltip`** on info icons next to labels for field-level help.
45. **Datepicker fields** must use `isDatepickerBlock` and `isClearable` attributes.
46. **Number input add-on suffix** (e.g., currency symbol) is placed after the input inside `euiInputGroupAddOn`, conditionally shown in edit mode.

### Accessibility

47. All interactive dropdown triggers must have `[attr.aria-label]`.
48. Autocomplete fields must have `aria-label`.
49. Informational icons should use `euiTooltip`.
50. Radio/checkbox inputs must have unique `id` attributes and matching `label[for]`.
51. Breadcrumb home item must have `ariaLabel="Home"`.
52. Each dropdown action item must have `aria-label`.
53. All interactive elements must be keyboard accessible.

---

## Key Differences from PAGE_DETAILS_SIMPLE_PATTERN (Simple AI)

| Aspect | Simple AI Pattern | Advanced AI Pattern (this) |
|--------|--------------------|-----------------------------|
| Page layout | Single column (`eui-page-content` only) | Two columns (`eui-page-columns`) |
| Sidebar menu | None | `eui-sidebar-menu` with `EuiMenuItem[]` |
| Breadcrumb | None | `eui-page-breadcrumb` with trail |
| Header body | None | Summary card with responsive Bootstrap grid + badges |
| Header collapsible | No | Yes (`[isCollapsible]="true"`) |
| Header actions | Toggle + Primary action | Toggle + Save + "More" dropdown (Label-icon variant) |
| Column actions | None | Right column header with Cancel/Submit buttons (`euiSizeS`) |
| EuiAppShellService | Not used | Used for dimmer highlight on main column |
| AsyncPipe | Not needed | Required for `(state$ | async)` |
| Footer style | Plain | `euiHighlighted="true"` |
| Back to list | Not applicable | Growl notification via back button in sidebar column header |
| Imports required | ~6 EUI modules | ~15 EUI modules + AsyncPipe |
| Navigation | None | Breadcrumb + sidebar menu + back button |
| Form grid | Bootstrap Grid (`col-md-*`) | Bootstrap Grid (`col-md-*`, `col-lg-*`, `col-xl-*`) |
| Helper text | None | `eui-helper-text` for field guidance |
| Fieldset extras | None | `euiFieldsetLabelExtraContent` with badge tooltip |
| Input add-on suffix | None | Currency symbol shown after amount input |
| Select implementation | Native `select[euiSelect]` + `option` | Native `select[euiSelect]` + `option` |
| Autocomplete binding | `[autocompleteData]` | `[autocompleteData]` with `[isFreeValueAllowed]` |
