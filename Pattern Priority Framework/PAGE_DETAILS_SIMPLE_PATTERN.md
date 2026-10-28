---
name: Page Details Simple Pattern — Canonical Structure Reference
description: Describes the Page Details Simple design pattern — a single-column detail page with reactive form, edit/read-only toggle, validation, and conditional footer actions. All component APIs must be retrieved from the eUI MCP Compodoc tool.
label: page-details-simple-ai
category: pattern
applies-to: page-details simple layout with reactive forms
triggered-when: generating a simple detail/edit page with an inline reactive form
requires: eUI page components, reactive forms, EuiGrowlService, EuiMessageBoxComponent
outputs: a self-contained single-column page with inline reactive form following the Page Details Simple layout pattern
related-skills: PAGE_HEADER_PATTERN, PAGE_FOOTER_PATTERN, SIMPLE_LAYOUT_PATTERN
---

# EUI Page Details Simple Pattern — Canonical Structure Reference

## Purpose

A single-column detail page with a responsive reactive form. All form logic, validators, and template markup are inline within a single component. The page supports edit/read-only mode toggle, validation with visual feedback, and conditional footer actions.

---

## Recommended Usage

Use this pattern when:

- A reactive form detail/edit page is needed
- The form includes diverse field types (text, number, select, autocomplete, datepicker, radio, checkbox, textarea)
- Edit/read-only mode toggle is required
- Form validation with visual feedback is needed
- The page follows a simple single-column layout (no columns, no breadcrumb)

---

## Page Header

This pattern uses the **Simple Page Header** variant from the `PAGE_HEADER_PATTERN`.

Refer to **PAGE_HEADER_PATTERN** for full structure, rules, and MCP retrieval strategy.

### Header Configuration for this Pattern

| Zone | Content |
|------|---------|
| Title (`label`) | Page title (e.g., "Page details") |
| Subtitle (`subLabel`) | Descriptive subtitle text |
| Action Items | Secondary button (toggle edit/read-only) + Primary button (page-level action) |

### MCP Retrieval Strategy (Header)

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageHeaderComponent` | Page header inputs: `label`, `subLabel` |
| `get_component_docs` | `EuiPageHeaderActionItemsComponent` | Action items container |

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌──────────────────────────────┬────────────────────────────────────┐  │
│  │ 1. PAGE HEADER               │ 2. PAGE HEADER ACTIONS             │  │
│  │    Page title                │    [Toggle edit/read-only]         │  │
│  │    Page subtitle             │    [Primary action]               │  │
│  └──────────────────────────────┴────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 3. PAGE CONTENT (inline form)                                     │  │
│  │                                                                   │  │
│  │  form[formGroup]                                                  │  │
│  │  ├── eui-fieldset (expanded) — Personal informations              │  │
│  │  │   └── Bootstrap row/col grid layout with form fields           │  │
│  │  ├── eui-fieldset (expanded) — Financial informations             │  │
│  │  │   └── Bootstrap row/col grid layout with form fields           │  │
│  │  ├── eui-fieldset (collapsed) — Placeholder                       │  │
│  │  ├── eui-fieldset (collapsed) — Placeholder                       │  │
│  │  └── eui-fieldset (collapsed) — Placeholder                       │  │
│  │                                                                   │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 4. PAGE FOOTER (conditional — edit mode only)                     │  │
│  │  [Reset]                          [Delete]  [Cancel]  [Submit]    │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | Description |
|---|-----------|-------------------|-----------|-------------|
| 1 | Page Header | `eui-page-header` [label, subLabel] | Yes | Page title and subtitle. See PAGE_HEADER_PATTERN (Simple variant). |
| 2 | Page Header Actions | `eui-page-header-action-items` | No | Secondary button (toggle edit/read-only) + Primary button (growl action). |
| 3 | Page Content | `eui-page-content` > `form[formGroup]` | Yes | Inline reactive form with multiple fieldsets using Bootstrap grid for responsive layout. |
| 4 | Page Footer | `eui-page-footer` | No | Conditional (`@if (isEditActive())`). See PAGE_FOOTER_PATTERN (Simple variant). |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── eui-page-header [label][subLabel]
│   └── eui-page-header-action-items
│       ├── button[euiButton][euiSecondary]  ← Toggle edit/read-only
│       └── button[euiButton][euiPrimary]    ← Primary action (growl)
├── eui-page-content
│   └── form[formGroup]
│       ├── eui-fieldset [label][iconSvgName][isExpandable][isExpanded=true]
│       │   ├── euiFieldsetLabelExtraContent (optional badge/tooltip)
│       │   └── div.row > div.col-md-N > div[euiInputGroup]
│       │       ├── label[euiLabel][euiRequired]
│       │       ├── div[euiInputGroupAddOn]
│       │       │   ├── @if (isEditActive()) → div[euiInputGroupAddOnItem] > eui-icon-svg
│       │       │   └── input[euiInputText] | input[euiInputNumber] | select[euiSelect] | eui-autocomplete
│       │       └── @if (hasValidationError) → eui-feedback-message[euiDanger]
│       │   ├── div.row > div.col-md-6 > div[euiInputGroup] (radio group)
│       │   ├── div.row > div.col-md-6 > div[euiInputGroup][formGroupName] (checkbox group)
│       │   └── div[euiInputGroup] > textarea[euiTextArea][euiMaxlength]
│       ├── eui-fieldset [label][iconSvgName][isExpandable][isExpanded=true]
│       │   ├── euiFieldsetLabelExtraContent (optional badge/tooltip)
│       │   └── div.row > div.col-md-4 > div[euiInputGroup]
│       │       ├── input[euiInputText] | select[euiSelect]
│       │       ├── eui-datepicker[isDatepickerBlock][isClearable]
│       │       ├── eui-autocomplete
│       │       └── input[euiInputNumber] with euiInputGroupAddOnItem suffix
│       ├── eui-fieldset [isExpanded=false]
│       ├── eui-fieldset [isExpanded=false]
│       └── eui-fieldset [isExpanded=false]
├── @if (isEditActive())
│   └── eui-page-footer
│       └── div.eui-u-flex.eui-u-flex-justify-content-between
│           ├── div (left) > button[euiButton] ← Reset
│           └── div.eui-u-flex (right)
│               ├── button[euiButton][euiDanger]    ← Delete
│               ├── button[euiButton][euiSecondary] ← Cancel
│               └── button[euiButton][euiPrimary]   ← Submit
└── eui-message-box #messageBox  ← Delete confirmation dialog
```

---

## Page Footer

This pattern uses the **Simple Page Footer** variant from the `PAGE_FOOTER_PATTERN`, with a conditional rendering twist.

Refer to **PAGE_FOOTER_PATTERN** for full structure, rules, and MCP retrieval strategy.

### Footer Configuration for this Pattern

| Aspect | Rule |
|--------|------|
| Visibility | Conditional — rendered only in edit mode (`@if (isEditActive())`) |
| Left content | Reset button (`euiButton` — plain/basic) |
| Right content | Delete (`euiDanger`) + Cancel (`euiSecondary`) + Submit (`euiPrimary`) |
| Layout | `eui-u-flex eui-u-flex-justify-content-between` outer div; left side with `eui-u-flex-justify-content-start`, right side with `eui-u-flex eui-u-flex-justify-content-end` |
| Button labels | Wrapped in `<span euiLabel>` |
| Button spacing | Use `eui-u-ml-m` utility class on right-side buttons |

### MCP Retrieval Strategy (Footer)

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageFooterComponent` | Footer container |
| `get_component_docs` | `EuiMessageBoxComponent` | Confirmation dialog for destructive actions |
| `get_component_docs` | `EuiGrowlService` | Toast notifications for action feedback |

---

## Form Structure

### Fieldset Organization

Form fields must be grouped into `eui-fieldset` sections with `isExpandable`. Primary sections are expanded by default, secondary sections are collapsed. Each fieldset may optionally include `euiFieldsetLabelExtraContent` with an `eui-badge` containing a tooltip for contextual help.

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiFieldsetComponent` | Fieldset inputs: `label`, `iconSvgName`, `isExpandable`, `isExpanded`, `isFirst` |

### Bootstrap Grid Layout — Responsive Columns

All form fields within fieldsets **must** use Bootstrap's Grid System (`row`, `col-md-*`) for responsive layout. This is mandatory per the Bootstrap Grid System Rule.

#### Personal Informations Fieldset Layout

| Row | Column Layout | Fields |
|-----|--------------|--------|
| 1 | `col-md-6` + `col-md-6` | First name, Last name |
| (full width, no row wrapper) | single `div[euiInputGroup]` | Address |
| 2 | `col-md-6` + `col-md-6` | Postal code, City (select) |
| 3 | `col-md-6` + `col-md-6` | Country (autocomplete), Email |
| 4 | `col-md-6` + `col-md-6` | Gender (radios), Spoken languages (checkboxes) |
| (full width, no row wrapper) | single `div[euiInputGroup]` | Remarks (textarea) |

#### Financial Informations Fieldset Layout

| Row | Column Layout | Fields |
|-----|--------------|--------|
| 1 | `col-md-4` + `col-md-4` + `col-md-4` | Invoice reference, Invoice type (select), Scan reference (select) |
| 2 | `col-md-4` + `col-md-4` + `col-md-4` | Invoice date (datepicker, required), Start date (datepicker), End date (datepicker) |
| 3 | `col-md-4` + `col-md-4` + `col-md-4` | Beneficiary (autocomplete), Total amount (number + currency suffix), Currency (select) |

#### Grid Rules

1. Wrap fields that share a row inside a `div.row`.
2. Each field cell uses `div.col-md-N` where N determines the responsive width (6 = half, 4 = third).
3. Full-width fields (address, textarea) do NOT need a `row` wrapper — they sit directly in the fieldset.
4. Add `eui-u-mt-m` class to the first `div.row` inside a fieldset for top spacing after the fieldset header.
5. The Bootstrap grid CSS must be imported in `angular.json` styles array: `node_modules/@eui/styles/dist/eui-bootstrap-grid.css`.

### Supported Field Types

The following field types are supported within fieldsets. Retrieve component documentation via MCP before generating code:

| Field Type | MCP Component Name | Directive/Selector |
|------------|-------------------|-------------------|
| Text input | `EuiInputTextDirective` | `euiInputText` |
| Number input | `EuiInputNumberDirective` | `euiInputNumber` |
| Select | `EuiSelectDirective` | `euiSelect` |
| Autocomplete | `EuiAutocompleteComponent` | `eui-autocomplete` |
| Datepicker | `EuiDatepickerComponent` | `eui-datepicker` |
| Radio button | `EuiInputRadioDirective` | `euiInputRadio` |
| Checkbox | `EuiInputCheckBoxDirective` | `euiInputCheckBox` |
| Textarea | `EuiTextAreaDirective` | `euiTextArea` |
| Label | `EuiLabelDirective` | `euiLabel` |
| Feedback message | `EuiFeedbackMessageComponent` | `eui-feedback-message` |
| Input group | `EuiInputGroupDirective` | `euiInputGroup` |
| Max length | `EuiMaxLengthDirective` | `euiMaxlength` |

---

## Field Layout Rules

### Input Group with Add-On Icon (Prefix)

Fields that display a leading icon in edit mode use the following structure:

```
div[euiInputGroup]
├── label[euiLabel][euiRequired]
├── div[euiInputGroupAddOn]
│   ├── @if (isEditActive()) → div[euiInputGroupAddOnItem] > eui-icon-svg
│   └── input[euiInputText][formControlName][placeholder][readonly=!isEditActive()]
└── @if (validationError) → eui-feedback-message[euiDanger]
```

### Input Group with Add-On Suffix (e.g. Currency)

Fields that display a trailing suffix (like currency) use:

```
div[euiInputGroup]
├── label[euiLabel][euiRequired]
├── div[euiInputGroupAddOn]
│   ├── input[euiInputNumber][formControlName][placeholder][readonly=!isEditActive()]
│   └── @if (isEditActive()) → div[euiInputGroupAddOnItem] > span (suffix text)
└── @if (validationError) → eui-feedback-message[euiDanger]
```

### Select Field

```
div[euiInputGroup]
├── label[for][euiLabel][euiRequired]
├── div[euiInputGroupAddOn]
│   ├── @if (isEditActive()) → div[euiInputGroupAddOnItem] > eui-icon-svg (optional)
│   └── select[id][euiSelect][formControlName][readonly=!isEditActive()]
│       └── @for (option) → option[value]
└── @if (validationError) → eui-feedback-message[euiDanger]
```

### Autocomplete Field

```
div[euiInputGroup]
├── label[euiLabel][euiRequired]
├── div[euiInputGroupAddOn]
│   ├── @if (isEditActive()) → div[euiInputGroupAddOnItem] > eui-icon-svg (optional)
│   └── eui-autocomplete[formControlName][autocompleteData][isFreeValueAllowed][placeholder][isReadonly=!isEditActive()][aria-label]
└── @if (validationError) → eui-feedback-message[euiDanger]
```

### Datepicker Field

```
div[euiInputGroup]
├── label[euiLabel][euiRequired]
├── eui-datepicker[isDatepickerBlock][isClearable][formControlName][isReadOnly=!isEditActive()]
└── @if (validationError) → eui-feedback-message[euiDanger]
```

### Radio Group

```
div[euiInputGroup]
├── label[euiLabel][euiRequired]
├── div.eui-u-flex.eui-u-flex-wrap
│   └── @for (radio of options) → div.eui-u-inline-flex.eui-u-mb-s
│       ├── input[euiInputRadio][id][name][formControlName][value][readonly=!isEditActive()]
│       └── label[euiLabel][for]
└── @if (validationError) → eui-feedback-message[euiDanger]
```

### Checkbox Group (with at-least-one validator)

```
div[euiInputGroup][formGroupName]
├── label[euiLabel][euiRequired]
├── div.eui-u-flex.eui-u-flex-wrap
│   └── @for (checkbox of options) → div.eui-u-inline-flex.eui-u-mb-s
│       ├── input[euiInputCheckBox][id][name][formControlName][readonly=!isEditActive()]
│       └── label[euiLabel][for]
└── @if (group.errors && group.touched) → eui-feedback-message[euiDanger]
```

### Textarea Field

```
div[euiInputGroup]
├── label[euiLabel]
└── textarea[euiTextArea][formControlName][euiMaxlength][placeholder][readonly=!isEditActive()]
```

---

## State Management

- Use Angular `signal()` for edit/read-only mode control.
- `isEditActive()` is used in the template for conditional rendering of input icons, readonly state, and footer visibility.
- Toggled via a method bound to the secondary action button in the header.
- Read-only state is applied per field via `[readonly]="!isEditActive()"` on inputs/selects/textareas, and `[isReadonly]="!isEditActive()"` on autocomplete, and `[isReadOnly]="!isEditActive()"` on datepicker.

---

## Page Actions

| Action | Behavior |
|--------|----------|
| Toggle edit/read-only | Flips edit mode signal, shows growl notification |
| Primary action | Shows info growl |
| Submit | Marks all fields touched, validates, shows success/danger growl |
| Cancel | Resets form, shows info growl |
| Reset | Resets form, shows info growl |
| Delete | Opens `eui-message-box` confirmation dialog |
| Delete accept | Shows danger growl |
| Delete dismiss | Shows info growl |

---

## Validation Rules

### Required Field Indicator

- Labels use `[euiRequired]="isEditActive()"` to conditionally display the required asterisk only in edit mode.
- Validation error messages are shown conditionally using `@if` based on the control being invalid and touched while in edit mode.

### Custom Checkbox Group Validator

- Checkbox groups use a `FormGroup` with `formGroupName` directive.
- A custom `ValidatorFn` is applied at the group level to check that at least N checkboxes are checked.
- The validator sets/clears individual control errors to propagate the visual state.
- Error message references `group.errors?.requireCheckboxesToBeChecked && group.touched`.

### Email Validator

- Email fields use `Validators.compose([Validators.email, Validators.required])`.
- Two separate validation messages: one for required, one for invalid email format.
- Use separate helper methods to distinguish between `hasError('required')` and `hasError('email')`.

---

## MCP Retrieval Strategy (Full)

All component APIs **must** be retrieved from the eUI MCP Compodoc tool before generating code. Do NOT rely on inline code samples.

| MCP Tool | Component Name | Purpose |
|----------|----------------|---------|
| `get_component_docs` | `EuiPageHeaderComponent` | Page header: `label`, `subLabel` |
| `get_component_docs` | `EuiPageHeaderActionItemsComponent` | Action items container |
| `get_component_docs` | `EuiPageContentComponent` | Main content area |
| `get_component_docs` | `EuiPageFooterComponent` | Footer container |
| `get_component_docs` | `EuiFieldsetComponent` | Fieldset: `label`, `iconSvgName`, `isExpandable`, `isExpanded` |
| `get_component_docs` | `EuiInputTextDirective` | Text input fields |
| `get_component_docs` | `EuiInputNumberDirective` | Number input fields |
| `get_component_docs` | `EuiSelectDirective` | Select dropdowns |
| `get_component_docs` | `EuiAutocompleteComponent` | Autocomplete fields |
| `get_component_docs` | `EuiDatepickerComponent` | Date picker fields |
| `get_component_docs` | `EuiInputRadioDirective` | Radio buttons |
| `get_component_docs` | `EuiInputCheckBoxDirective` | Checkboxes |
| `get_component_docs` | `EuiTextAreaDirective` | Textarea fields |
| `get_component_docs` | `EuiLabelDirective` | Form labels |
| `get_component_docs` | `EuiFeedbackMessageComponent` | Validation error messages |
| `get_component_docs` | `EuiInputGroupDirective` | Input group wrapper |
| `get_component_docs` | `EuiInputGroupAddOnDirective` | Input add-on (icons, suffixes) |
| `get_component_docs` | `EuiMaxLengthDirective` | Character count for textareas |
| `get_component_docs` | `EuiMessageBoxComponent` | Confirmation dialog |
| `get_component_docs` | `EuiGrowlService` | Toast notifications |
| `get_component_docs` | `EuiTooltipDirective` | Tooltip on icons |

---

## Required Angular Imports

Retrieve the exact import paths via MCP `get_component_docs` for each component. The following EUI token arrays must be spread in the component `imports` array:

- `EUI_PAGE` from `@eui/components/eui-page`
- `EUI_BADGE` from `@eui/components/eui-badge`
- `EUI_BUTTON` from `@eui/components/eui-button`
- `EUI_DATEPICKER` from `@eui/components/eui-datepicker`
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
- `EUI_TEXTAREA` from `@eui/components/eui-textarea`
- `EUI_AUTOCOMPLETE` from `@eui/components/eui-autocomplete`
- `EuiMaxLengthDirective` from `@eui/components/directives`
- `EuiTooltipDirective` from `@eui/components/directives`
- `EuiMessageBoxComponent` from `@eui/components/eui-message-box`
- `ReactiveFormsModule` from `@angular/forms`

When using datepickers, provide `provideMomentDateAdapter(DEFAULT_FORMATS)` in the component `providers` array:
- `provideMomentDateAdapter` from `@angular/material-moment-adapter`
- `DEFAULT_FORMATS` from `@eui/components/eui-datepicker`

When using autocomplete, import the `EuiAutoCompleteItem` type:
- `EuiAutoCompleteItem` from `@eui/components/eui-autocomplete`

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

### General Rules

1. **Retrieve all component APIs** from the eUI MCP Compodoc tool (`get_component_docs`) before generating code.
2. **Use the PAGE_HEADER_PATTERN** (Simple variant) for the page header structure and rules.
3. **Use the PAGE_FOOTER_PATTERN** (Simple variant) for the page footer structure and rules.
4. **Keep everything self-contained** — all validators and logic are inline within the component.
5. **Use `signal()`** for edit/read-only mode control.
6. **Use `FormBuilder`** with `FormGroup` and define all controls in a `buildForm()` method called in `ngOnInit()`.
7. **Group form fields into `eui-fieldset` sections** with `isExpandable`. Primary sections expanded, secondary collapsed.
8. **Use `eui-feedback-message euiDanger`** for validation errors, rendered conditionally with `@if`.
9. **Use `euiInputGroupAddOn` with `euiInputGroupAddOnItem`** for field icons (prefix) or suffixes, conditionally shown only in edit mode.
10. **Use `ChangeDetectionStrategy.OnPush`** on the component.
11. **Provide `provideMomentDateAdapter(DEFAULT_FORMATS)`** in providers when using datepickers.
12. **Use the simple page layout** (`eui-page` > header > content > footer) with no columns/breadcrumb.
13. **Footer is conditional** (`@if (isEditActive())`) — hidden in read-only mode.
14. **Footer button hierarchy**: Reset (plain, left), Delete (`euiDanger`, right), Cancel (`euiSecondary`, right), Submit (`euiPrimary`, right). All use `<span euiLabel>`.
15. **Include `eui-message-box`** for destructive actions (delete) with accept/dismiss handlers. Place it **outside** `eui-page` at the end of the template.
16. **Use `EuiGrowlService`** for all user feedback notifications via `inject()`.
17. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_BUTTON`).
18. **Use `@for` control flow** (Angular 17+) for iterations, not `*ngFor`.
19. **Use `@if` control flow** (Angular 17+) for conditionals, not `*ngIf`.
20. **Data is agnostic** — form field options, labels, and values are set up by the user. This pattern does not prescribe specific data models or option lists.

### Bootstrap Grid Rules

21. **Use Bootstrap Grid System** (`row`, `col-md-*`) for responsive layout of form fields within fieldsets.
22. **Ensure `eui-bootstrap-grid.css`** is imported in `angular.json` styles array: `"node_modules/@eui/styles/dist/eui-bootstrap-grid.css"`.
23. **Personal informations fieldset** uses `col-md-6` (two-column) for paired fields and full-width for address/textarea.
24. **Financial informations fieldset** uses `col-md-4` (three-column) for all field rows.
25. **Add `eui-u-mt-m`** class to the first `div.row` in each fieldset for spacing after the fieldset header content.
26. **Full-width fields** (address, textarea) do not need a `div.row` wrapper — they are placed directly in the fieldset.
27. **Never use custom CSS or inline styles** for layout — only Bootstrap grid classes and eUI utility classes.

### Form Rules

28. **Implement radio buttons** with `euiInputRadio`, a single `formControlName`, `[value]` binding, `name` attribute, and `[readonly]="!isEditActive()"`.
29. **Implement checkbox groups** with a nested `FormGroup`, `formGroupName` directive, and individual `FormControl` per checkbox with a custom group validator (`requireCheckboxesToBeCheckedValidator`).
30. **Use `euiMaxlength`** on textarea fields for character count display.
31. **Use `isDatepickerBlock`** on datepickers to make them fill their container width.
32. **Use `isClearable`** on datepickers to allow clearing the value.
33. **Use `[isReadOnly]="!isEditActive()"`** on datepickers for read-only mode.
34. **Use `[isReadonly]="!isEditActive()"`** on autocomplete for read-only mode (note: lowercase 'o').
35. **Use `[readonly]="!isEditActive()"`** on input, select, and textarea for read-only mode.
36. **Currency suffix pattern**: The total amount field displays the selected currency as a trailing `euiInputGroupAddOnItem` suffix, shown only in edit mode. The suffix value is bound to a component property updated via subscription on the currency select control.

### Accessibility

37. All radio/checkbox inputs must have unique `id` attributes and matching `<label for="">`.
38. Autocomplete fields must have `aria-label`.
39. Informational icons should use `euiTooltip`.
40. Select elements should have unique `id` and matching `<label for="">`.
41. Labels with tooltip icons use an inline `eui-icon-svg` with `fillColor="info"`, `class="eui-u-cursor-help eui-u-ml-s"`, and `euiTooltip`.

### Fieldset Extra Content

42. Each fieldset may optionally include `<euiFieldsetLabelExtraContent>` with an `eui-badge[euiSecondary]` displaying a `?` character and a `euiTooltip` for contextual help information. Apply `class="eui-u-cursor-help eui-u-ml-m"` on the badge.
