---
name: eui-coding-rules
description: Enforces EUI component library coding patterns, layout rules, and design conventions. Apply these rules whenever generating Angular templates or components using EUI (eui-page, eui-card, eui-dropdown, eui-dialog, eui-breadcrumb, eui-paginator, eui-page-footer, Bootstrap grid). Covers action menus, selectable cards with bulk actions, dialog structure, footer layouts, breadcrumb placement, and styling constraints.
---

You are an expert in the EUI Angular component library. When generating code that uses EUI components, you MUST follow all the rules below. These rules are non-negotiable and must always be applied.

---

# eui-page-footer Simple Rules

When generating a simple `eui-page-footer` (contextual page actions like Save/Cancel, without bulk selection or highlighted state), always follow this structure:

## Layout

Use a flex container with `eui-u-flex-justify-content-end` to separate left and right action groups:

```html
<eui-page-footer>
    <div class="eui-u-flex eui-u-flex-justify-content-end eui-u-flex-align-items-center">
        <div>
            <!-- Left actions (Tertiary actions) -->
            <button euiButton euiSecondary (click)="onTertiaryAction()">
                <eui-icon-svg icon="eui-close" size="s" />
                Cancel
            </button>
        </div>
        <div class="eui-u-flex eui-u-flex-gap-s">
            <!-- Right actions (Secondary action then Primary) -->
            <button euiButton euiSecondary (click)="onSecondaryAction()">
                <eui-icon-svg icon="icon-name" />
                Secondary
            </button>
            <!-- Primary action -->
            <button euiButton euiPrimary (click)="onPrimaryAction()">
                <eui-icon-svg icon="icon-name" />
                Primary
            </button>
        </div>
    </div>
</eui-page-footer>
```

## Rules Summary

1. Always use `eui-u-flex eui-u-flex-justify-content-end eui-u-flex-align-items-center` on the inner wrapper div.
2. Place dismissive actions (Cancel, Back) on the left side.
3. Place affirmative actions (Save, Submit, Export) on the right side.
4. Order right-side actions from least important (secondary) to most important (primary), left to right.
5. Use `eui-u-flex eui-u-flex-gap-s` on the right-side container for consistent spacing between buttons.
6. Do NOT use `euiHighlighted` on simple page footers — that is reserved for bulk action footers tied to selection state.
7. Do NOT conditionally show/hide simple page footers — they must always be visible.
8. You can include an icon inside each button for visual clarity.

---

# eui-page-breadcrumb Rules

When the user requests a breadcrumb on a page, always add `eui-page-breadcrumb` inside `eui-page` **before** the `eui-page-header`.

## Structure

```html
<eui-page>
    <eui-page-breadcrumb>
        <eui-breadcrumb>
            <eui-breadcrumb-item id="0" link="/" iconSvgName="eui-home" ariaLabel="Home" />
            <eui-breadcrumb-item id="1" label="Parent page" link="/screen/parent" />
            <eui-breadcrumb-item id="2" label="Current page" />
        </eui-breadcrumb>
    </eui-page-breadcrumb>

    <eui-page-header label="Page title">
        ...
    </eui-page-header>
    ...
</eui-page>
```

## Rules Summary

1. Place `eui-page-breadcrumb` as the first child of `eui-page`, before `eui-page-header`.
2. Always start with a Home item using `link="/"`, `iconSvgName="eui-home"`, and `ariaLabel="Home"`.
3. Intermediate items must have `label` and `link` attributes pointing to their route.
4. The last item (current page) must have only a `label` — no `link` attribute.
5. Each `eui-breadcrumb-item` must have a unique sequential `id` starting from `"0"`.
6. Import `EUI_BREADCRUMB` from `@eui/components/eui-breadcrumb` and spread it in the component imports array.
7. Do NOT add breadcrumbs unless the user explicitly requests them.

---

# eui-paginator Rules

When using the `eui-paginator` component, always enable the `[hasPageNumberNavigation]="true"` option. This displays page number buttons for direct navigation between pages, improving user experience.

---

# eui-dropdown Action Menu Rules

When using `eui-dropdown` to display row-level actions in a table or card, always follow this structure:

## Trigger Button

Default actions dropdown button should use a button label and the eui-ellipsis-vertical icon using the icon-only variant.
When having other actions next to the eui-dropdown button, the trigger must use the Label-icon variant.

### Icon-only variant

Use an icon-only action button with the vertical ellipsis icon:

```html
<button euiButton euiPrimary euiBasicButton euiRounded euiIconButton [attr.aria-label]="'Actions'">
    <eui-icon-svg icon="eui-ellipsis-vertical" size="s" />
</button>
```

Required directives on the trigger: `euiButton`, `euiPrimary`, `euiBasicButton`, `euiRounded`, `euiIconButton`.

Do not use text labels on action menu triggers in tables. The trigger must be icon-only.

### Label-icon variant

```html
<eui-dropdown>
    <button euiButton euiPrimary euiOutline euiSizeS [attr.aria-label]="'Actions'">
        <span euiLabel>Actions</span>
        <eui-icon-svg icon="eui-ellipsis-vertical" />
    </button>
    <eui-dropdown-content>
        <button euiDropdownItem (click)="onAction(row)" aria-label="Action name">Action name</button>
    </eui-dropdown-content>
</eui-dropdown>
```

Required directives on the trigger: `euiButton`, `euiPrimary`, `euiOutline`, `euiSizeS`.

Always use text labels on action menu triggers in tables or cards.

## Dropdown Content

Use `<eui-dropdown-content>` with `<button euiDropdownItem>` elements for each action:

```html
<eui-dropdown-content>
    <button euiDropdownItem (click)="onAction(row)" aria-label="Action name">Action name</button>
</eui-dropdown-content>
```

Do not use `<eui-dropdown-item>` as element — use `<button euiDropdownItem>` instead.

## Complete Pattern

```html
<eui-dropdown>
    <button euiButton euiPrimary euiBasicButton euiRounded euiIconButton [attr.aria-label]="'Actions'">
        <eui-icon-svg icon="eui-ellipsis-vertical" size="s" />
    </button>
    <eui-dropdown-content>
        <button euiDropdownItem (click)="onView(row)" aria-label="View">View</button>
        <button euiDropdownItem (click)="onEdit(row)" aria-label="Edit">Edit</button>
        <button euiDropdownItem (click)="onDelete(row)" aria-label="Delete">Delete</button>
    </eui-dropdown-content>
</eui-dropdown>
```

## Rules Summary

1. Trigger must use the Icon-only or Label-icon variant.
2. Use `eui-ellipsis-vertical` icon at size `"s"`.
3. Always provide `[attr.aria-label]` on the trigger button.
4. Always provide `aria-label` on each `euiDropdownItem`.
5. Use `<button euiDropdownItem>` — never `<eui-dropdown-item>`.

---

# No Extra Styles Rule

NEVER add or use custom styling CSS or SCSS when generating code.

---

# No Inline Styles Rule

NEVER use custom inline styling (`style="..."`) in templates. Always use eUI utility classes (`eui-u-*`) or Bootstrap grid classes whenever possible.

If no utility class exists for the desired styling, create a CSS class in the component's stylesheet rather than using inline styles.

---

# eui Selectable Cards List Rules

When generating a selectable cards list (multi-select cards with bulk actions), always follow this pattern:

## Page Column with euiHighlighted

The `eui-page-column` containing the cards list must use `[euiHighlighted]` bound to the `appShellService.state$` dimmer state:

```html
<eui-page-column [euiHighlighted]="(appShellService.state$ | async)?.isDimmerActive">
```

This requires:
- `EuiAppShellService` injected as a **public** property (accessible from template)
- `AsyncPipe` imported in the component

## Dimmer Activation

Use an Angular `effect()` to activate the app shell dimmer when items are selected:

```typescript
appShellService = inject(EuiAppShellService);

private dimmerEffect = effect(() => {
    this.appShellService.isDimmerActive = this.selectedCount() > 0;
});
```

## Select All with Indeterminate

The "Select all" checkbox must support three states using `[indeterminate]`:

```html
<input euiInputCheckBox id="select-all"
    [checked]="isAllSelected()"
    (change)="toggleSelectAll()"
    [indeterminate]="isIndeterminate()"
    aria-label="Select all" />
<label for="select-all" euiLabel>Select all</label>
```

Where `isIndeterminate` is true when some (but not all) visible items are selected.

## Card Selection

Each card must use `[euiSelected]` (not `euiHighlighted`) bound to the individual card's selected state, with a checkbox in `eui-card-header-left-content`:

```html
<eui-card [euiSelected]="isCardSelected(item.id)" euiCollapsible euiCollapsed>
    <eui-card-header hasBottomExpander>
        <eui-card-header-left-content>
            <input euiInputCheckBox
                [id]="'card-select-' + item.id"
                [checked]="isCardSelected(item.id)"
                (change)="toggleCardSelection(item.id)"
                [attr.aria-label]="'Select ' + item.title" />
        </eui-card-header-left-content>
        <eui-card-header-title>{{ item.title }}</eui-card-header-title>
    </eui-card-header>
</eui-card>
```

## Card Actions in Header

Row-level actions must be placed inside `eui-card-header-right-content` using the eui-dropdown pattern:

```html
<eui-card-header-right-content>
    <div class="eui-u-flex eui-u-flex-align-items-center eui-u-flex-gap-s" (click)="$event.stopPropagation()">
        <eui-dropdown>
            <button euiButton euiPrimary euiOutline [attr.aria-label]="'Actions'">
                <span euiLabel>Actions</span>
                <eui-icon-svg icon="eui-ellipsis-vertical" size="s" />
            </button>
            <eui-dropdown-content>
                <button euiDropdownItem (click)="onView(item)" aria-label="View">View</button>
                <button euiDropdownItem (click)="onEdit(item)" aria-label="Edit">Edit</button>
                <button euiDropdownItem (click)="onDelete(item)" aria-label="Delete">Delete</button>
            </eui-dropdown-content>
        </eui-dropdown>
    </div>
</eui-card-header-right-content>
```

When using the fluid pattern layout with panel for detail always add an action button next to the dropdown as the last action button in order to trigger the fluid panel display:

```html
<button euiButton euiSecondary euiIconButton euiOutline (click)="onView(item)" aria-label="View detail in panel" euiTooltip="View detail">
    <eui-icon-svg icon="arrow-line-right:regular" />
</button>
```

Do not use `eui-card-footer` for row-level actions in selectable cards lists.

## Page Footer with euiHighlighted for Bulk Actions

Bulk actions must appear in a `eui-page-footer` with `euiHighlighted`, shown only when items are selected:

```html
@if (selectedCount() > 0) {
    <eui-page-footer euiHighlighted>
        <div class="eui-u-flex eui-u-flex-justify-content-between eui-u-flex-align-items-center">
            <div class="eui-u-flex eui-u-flex-gap-m">
                <button euiButton euiBasicButton (click)="clearSelection()">Reset</button>
                <div class="eui-u-display-flex">
                    <span class="eui-u-f-bold">{{ selectedCount() }}</span>&nbsp;selected items
                </div>
            </div>
            <div class="eui-u-display-flex eui-u-flex-gap-s">
                <button euiButton euiSecondary (click)="clearSelection()">
                    <eui-icon-svg icon="eui-close" size="s" />
                    Cancel
                </button>
                <button euiButton euiPrimary (click)="onBulkAction()">
                    <eui-icon-svg icon="eui-download" size="s" />
                    Primary Action
                </button>
            </div>
        </div>
    </eui-page-footer>
}
```

## Rules Summary

1. Use `euiHighlighted` on the `eui-page-column` bound to `(appShellService.state$ | async)?.isDimmerActive`.
2. Use `euiSelected` on individual `eui-card` elements for per-card visual state.
3. Use `euiHighlighted` on the `eui-page-footer` for the bulk actions bar.
4. Activate the dimmer via `EuiAppShellService.isDimmerActive` using an `effect()`.
5. Place card-level actions in `eui-card-header-right-content`, not in `eui-card-footer`.
6. Always include `[indeterminate]` on the "Select all" checkbox.
7. Always provide `aria-label` on checkboxes and action buttons.
8. Use `(click)="$event.stopPropagation()"` on the right-content action container to prevent card collapse toggling.

---

# eui-dialog Rules

When generating the content of an `eui-dialog`, the dialog body must always be implemented in a separate dedicated component. The `eui-dialog` element itself can remain in the parent template, but its inner content (form, layout, logic) must be extracted into its own component that is rendered inside the dialog.

This ensures:
- Clear separation of concerns between the parent view and the dialog logic
- Easier testability of the dialog content in isolation
- Reusability of the dialog content component across different contexts
- Cleaner templates that remain readable as complexity grows

---

# Bootstrap Grid System Rule

When using responsive layout display, ALWAYS use Bootstrap's Grid System styles (`row`, `col-*`, `col-md-*`, `col-lg-*`, `col-xl-*`, etc.).

The Bootstrap grid must be imported by adding the `eui-bootstrap-grid.css` file to the project's root configuration (e.g., in `angular.json` styles array or equivalent):

```json
"styles": [
  "node_modules/@eui/styles/dist/eui-bootstrap-grid.css"
]
```

Do not use custom flex-based grid alternatives when Bootstrap grid classes are available.
