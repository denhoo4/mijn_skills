---
name: Page List Anatomy Pattern
description: Full-featured two-column search & results page layout showing all available building blocks. Includes collapsible filter sidebar (text search, quick filters, advanced filters), result column with header, filter criteria chips, paginated card list with per-card actions, and page footer. Canonical reference for understanding all page list structural options.
label: page-list-anatomy
category: pattern
applies-to: page list anatomy reference, understanding all available page list zones and components
triggered-when: understanding the complete page list structure, referencing all available page list building blocks, or assembling a card-based list page with search and filter capabilities
requires: eUI page components, eui-card, eui-chip, eui-chip-list, eui-dropdown, eui-fieldset, eui-input-text, eui-input-checkbox, eui-select, eui-paginator, EuiTooltipDirective
outputs: a two-column page list with all optional and mandatory zones included as a structural reference
related-skills: PAGE_LIST_CARDS_FILTER_PATTERN, PAGE_LIST_CARDS_SIMPLE_PATTERN, PAGE_LIST_CARDS_SELECTION_PATTERN, TABLE_LIST_PATTERN, COLUMNS_LAYOUT_PATTERN
---

# EUI Page List Anatomy Pattern — Canonical Structure Reference

## Purpose

This document describes the **Page List Anatomy** design pattern — the full-featured two-column search & results page layout used across all EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

### What is this pattern?

The Page List Anatomy pattern represents the **complete page list with all available options**: a collapsible filter sidebar on the left (with text search, quick filters, and advanced filters) and a paginated card-based result list on the right (with column header, filter criteria chips, contextual actions, and per-card action dropdowns), wrapped inside the standard EUI page scaffolding (breadcrumb, header with actions, footer). It is the canonical reference layout whenever a user needs to **browse, search, filter, and act upon a collection of items**.

---

## Visual Anatomy (decoded from page-list-cards-list-anatomy.png)

The anatomy image shows a full page list layout with 11 numbered reference markers:

- 1 — **Page breadcrumb** (outside pattern): horizontal navigation trail at the top (Home > Section > Current page)
- 2 — **Page header** (outside pattern): page title and subtitle spanning the left portion
- 3 — **Page actions** (outside pattern): action buttons aligned to the right of the header (secondary, primary, overflow dropdown)
- 4 — **Filter column**: collapsible left sidebar with text search, quick filters (expandable), and advanced filters (collapsed by default)
- 5 — **Result column header** (mandatory): title ("Filter results") and result count
- 6 — **Contextual column actions**: action buttons scoped to the result column (secondary + primary, size S)
- 7 — **Filter criteria**: active filter criteria displayed as removable chips with a "Clear all" link
- 8 — **List content** (mandatory): iterable list of `eui-card` components
- 9 — **Card list action**: per-card action dropdown menu (Edit, Delete, etc.)
- 10 — **Paginator**: pagination control at the bottom of the result column
- 11 — **Page footer**: global page-level actions at the bottom (secondary + primary buttons)

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 1. PAGE BREADCRUMB  (eui-page-breadcrumb)                         │  │
│  │    [eui-home] Home > Section > Current page                       │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────┬────────────────────────────────────┐  │
│  │ 2. PAGE HEADER               │ 3. PAGE ACTIONS                    │  │
│  │    Title / Sub-title         │    [Secondary] [Primary]           │  │
│  │                              │    [Other actions eui-chevron-down]│  │
│  └──────────────────────────────┴────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ eui-page-content > eui-page-columns                               │  │
│  │  ┌──────────────────┐  ┌──────────────────────────────────────┐   │  │
│  │  │ 4. FILTER COLUMN │  │ 5. RESULT COLUMN HEADER              │   │  │
│  │  │  (collapsible)   │  │    Title + result count              │   │  │
│  │  │                  │  │                          6. ACTIONS  │   │  │
│  │  │  ┌────────────┐  │  ├──────────────────────────────────────┤   │  │
│  │  │  │[eui-search]│  │  │ 7. FILTER CRITERIA (chips)           │   │  │
│  │  │  │ Text search│  │  │    Selected: [chip1] [chip2] Clear   │   │  │
│  │  │  └────────────┘  │  ├──────────────────────────────────────┤   │  │
│  │  │                  │  │ 8. LIST CONTENT                      │   │  │
│  │  │  ┌────────────┐  │  │                                      │   │  │
│  │  │  │Quick filter│  │  │  ┌────────────────────────────────┐  │   │  │
│  │  │  │(expandable)│  │  │  │ eui-card                       │  │   │  │
│  │  │  │ [] Check 1 │  │  │  │  Title (link)    [Status] 9.   │  │   │  │
│  │  │  │ [] Check 2 │  │  │  │  Subtitle         [eui-edit]   │  │   │  │
│  │  │  │ [Select]   │  │  │  │                   [eui-trash]  │  │   │  │
│  │  │  └────────────┘  │  │  └────────────────────────────────┘  │   │  │
│  │  │                  │  │  ┌────────────────────────────────┐  │   │  │
│  │  │  ┌────────────┐  │  │  │ eui-card                       │  │   │  │
│  │  │  │ Advanced   │  │  │  │  Title (link)    [Status] 9.   │  │   │  │
│  │  │  │ (collapsed)│  │  │  │  Subtitle                      │  │   │  │
│  │  │  └────────────┘  │  │  └────────────────────────────────┘  │   │  │
│  │  │                  │  │                                      │   │  │
│  │  └──────────────────┘  ├──────────────────────────────────────┤   │  │
│  │                        │ 10. PAGINATOR                        │   │  │
│  │                        │    eui-paginator                     │   │  │
│  │                        └──────────────────────────────────────┘   │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 11. PAGE FOOTER                                                   │  │
│  │                              [Secondary action] [Primary action]  │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

|  #  | Zone Name | EUI Component(s) | Mandatory | Description |
|-----|-----------|-------------------|-----------|-------------|
|  1  | Page Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item` | No | Navigation trail. First item uses `iconSvgName="eui-home"` with `ariaLabel="Home"`. Last item has no `link` (current page). |
|  2  | Page Header | `eui-page-header` | Yes | Page title via `label` input, optional subtitle via `subLabel`. |
|  3  | Page Actions | `eui-page-header-action-items` | No | Top-level page actions. Contains primary/secondary buttons and an overflow `eui-dropdown` with `eui-chevron-down` icon. |
|  4  | Filter Column | `eui-page-column` (1st, with `isCollapsible`, sized `euiSize3XL`) | No | Left sidebar containing search and filter controls. Has its own header with optional action button via `eui-page-column-header-right-content`. Body contains form fields organized in `eui-fieldset` sections. |
|  5  | Result Column Header | `eui-page-column` (2nd) > `eui-page-column-header-left-content` | Yes | Displays a title ("Filter results") and the total result count. |
|  6  | Contextual Column Actions | `eui-page-column-header-right-content` (of 2nd column) | No | Action buttons scoped to the result list (secondary + primary, size S). |
|  7  | Filter Criteria | `eui-page-column-header-body` | No | Displays active filter criteria as removable `eui-chip` items inside an `eui-chip-list` with a "Clear all" link. |
|  8  | List Content | `eui-page-column-body` (of 2nd column) | Yes | Iterable list of `eui-card` components. Each card has a header with title (link), subtitle, status chip, and action dropdown. |
|  9  | Card List Action | `eui-dropdown` inside `eui-card-header-right-content` | No | Per-item action menu with icon-prefixed dropdown items (`eui-edit`, `eui-trash`). |
| 10  | Paginator | `eui-page-column-footer` > `eui-paginator` | No | Pagination control bound to the data source length via `[length]`. |
| 11  | Page Footer | `eui-page-footer` | No | Global page-level actions at the bottom (secondary + primary buttons, right-aligned with `eui-u-ml-auto`). |

---

## Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-home` | `eui-breadcrumb-item` | Breadcrumb home item (`iconSvgName`) |
| `eui-chevron-down` | `eui-icon-svg` / `span[euiIconSvg]` | Page-level overflow dropdown trigger + card action dropdown trigger |
| `eui-search` | `eui-icon-svg` | Text search button in filter column |
| `eui-edit` | `eui-icon-svg` | Edit action in card dropdown |
| `eui-trash` | `eui-icon-svg` | Delete action in card dropdown |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── eui-page-breadcrumb
│   └── eui-breadcrumb
│       └── eui-breadcrumb-item (×N)
├── eui-page-header [label, subLabel]
│   └── eui-page-header-action-items
│       ├── button[euiButton][euiSecondary]
│       ├── button[euiButton][euiPrimary]
│       └── eui-dropdown
│           ├── button[euiButton][euiPrimary][euiOutline] + eui-icon-svg[icon="eui-chevron-down"]
│           └── eui-dropdown-content
│               └── button[euiDropdownItem] (×N)
├── eui-page-content
│   └── eui-page-columns [hasPreventMobileRendering]
│       ├── eui-page-column [label="Search filter"][euiSize3XL][isCollapsible]  ← FILTER COLUMN
│       │   ├── eui-page-column-header-right-content
│       │   │   └── button[euiButton][euiBasicButton][euiPrimary][euiSizeS]
│       │   └── eui-page-column-body
│       │       └── div.eui-u-flex.eui-u-flex-column
│       │           ├── div[euiInputGroup]  ← text search
│       │           │   ├── label[euiLabel]
│       │           │   └── div[euiInputGroupAddOn]
│       │           │       ├── input[euiInputText]
│       │           │       └── button[euiButton][euiIconButton][euiPrimary][euiOutline] > eui-icon-svg[icon="eui-search"]
│       │           ├── eui-fieldset [label][isLarge][isExpandable]  ← quick filters
│       │           │   ├── div[euiInputGroup] (checkboxes)
│       │           │   └── div[euiInputGroup] (select)
│       │           └── eui-fieldset [label][isLarge][isExpandable][isExpanded=false]  ← advanced filters
│       │               └── div[euiInputGroup] (select)
│       └── eui-page-column  ← RESULT COLUMN
│           ├── eui-page-column-header-left-content
│           │   ├── div.eui-u-f-l  ← title
│           │   └── div  ← result count
│           ├── eui-page-column-header-body
│           │   ├── div  ← "Selected criteria" + "Clear all" link
│           │   └── eui-chip-list
│           │       └── eui-chip [isChipRemovable][euiSizeS] (×N)
│           ├── eui-page-column-header-right-content
│           │   ├── button[euiButton][euiSecondary][euiSizeS]
│           │   └── button[euiButton][euiPrimary][euiSizeS]
│           ├── eui-page-column-body
│           │   └── @for ← iteration over data source
│           │       └── eui-card.eui-u-mb-m
│           │           └── eui-card-header
│           │               ├── eui-card-header-title
│           │               │   └── a.eui-u-text-link
│           │               ├── eui-card-header-subtitle
│           │               └── eui-card-header-right-content
│           │                   ├── eui-chip[euiSuccess]  ← status
│           │                   └── eui-dropdown  ← per-card actions
│           │                       ├── button[euiButton][euiBasicButton][euiPrimary][euiOutline][euiSizeS]
│           │                       └── eui-dropdown-content
│           │                           └── button[euiDropdownItem] (×N) with eui-icon-svg prefix
│           └── eui-page-column-footer
│               └── eui-paginator [length]
└── eui-page-footer
    └── div.eui-u-ml-auto
        ├── button[euiButton][euiSecondary]
        └── button[euiButton][euiPrimary]
```

---

## Required Angular Imports

```typescript
import { EuiTooltipDirective } from '@eui/components/directives';
import { EUI_BREADCRUMB } from '@eui/components/eui-breadcrumb';
import { EUI_BUTTON } from '@eui/components/eui-button';
import { EUI_CARD } from '@eui/components/eui-card';
import { EUI_CHIP } from '@eui/components/eui-chip';
import { EUI_CHIP_LIST } from '@eui/components/eui-chip-list';
import { EUI_DROPDOWN } from '@eui/components/eui-dropdown';
import { EUI_FIELDSET } from '@eui/components/eui-fieldset';
import { EUI_ICON } from '@eui/components/eui-icon';
import { EUI_INPUT_CHECKBOX } from '@eui/components/eui-input-checkbox';
import { EUI_INPUT_GROUP } from '@eui/components/eui-input-group';
import { EUI_INPUT_TEXT } from '@eui/components/eui-input-text';
import { EUI_LABEL } from '@eui/components/eui-label';
import { EUI_PAGE } from '@eui/components/eui-page';
import { EUI_PAGINATOR } from '@eui/components/eui-paginator';
import { EUI_SELECT } from '@eui/components/eui-select';
```

Component `imports` array (spread each token):

```typescript
imports: [
    ...EUI_PAGE,
    ...EUI_DROPDOWN,
    ...EUI_ICON,
    ...EUI_BREADCRUMB,
    ...EUI_BUTTON,
    ...EUI_FIELDSET,
    ...EUI_LABEL,
    ...EUI_INPUT_GROUP,
    ...EUI_INPUT_TEXT,
    ...EUI_INPUT_CHECKBOX,
    ...EUI_SELECT,
    ...EUI_CARD,
    ...EUI_CHIP,
    ...EUI_CHIP_LIST,
    ...EUI_PAGINATOR,
    EuiTooltipDirective,
]
```

---

## Reference Template

```html
<eui-page>
    <eui-page-breadcrumb>
        <eui-breadcrumb>
            <eui-breadcrumb-item id="0" link="/" iconSvgName="eui-home" ariaLabel="Home" />
            <eui-breadcrumb-item id="1" label="Section" link="/"/>
            <eui-breadcrumb-item id="2" label="Current page"/>
        </eui-breadcrumb>
    </eui-page-breadcrumb>

    <eui-page-header label="Page title" subLabel="Page Sub-title (optional)">
        <eui-page-header-action-items>
            <button euiButton euiSecondary>Secondary action</button>
            <button euiButton euiPrimary>Primary action</button>
            <eui-dropdown>
                <button euiButton euiPrimary euiOutline euiTooltip="More actions" aria-label="More actions menu">
                    Other actions
                    <eui-icon-svg icon="eui-chevron-down"/>
                </button>
                <eui-dropdown-content>
                    <button euiDropdownItem aria-label="Action item 1">Extra page action item 1</button>
                    <button euiDropdownItem aria-label="Action item 2">Extra page action item 2</button>
                    <button euiDropdownItem aria-label="Action item 3">Extra page action item 3</button>
                </eui-dropdown-content>
            </eui-dropdown>
        </eui-page-header-action-items>
    </eui-page-header>

    <eui-page-content>
        <eui-page-columns hasPreventMobileRendering>

            <!-- FILTER COLUMN (left sidebar) -->
            <eui-page-column label="Search filter" euiSize3XL isCollapsible>
                <eui-page-column-header-right-content>
                    <button euiButton euiBasicButton euiPrimary euiSizeS>Action</button>
                </eui-page-column-header-right-content>
                <eui-page-column-body>
                    <div class="eui-u-flex eui-u-flex-column">

                        <!-- TEXT SEARCH -->
                        <div euiInputGroup>
                            <label for="text-search" euiLabel>Search</label>
                            <div class="eui-u-f-s eui-u-mb-2xs">Type at least 3 characters</div>
                            <div euiInputGroupAddOn>
                                <input euiInputText id="text-search" />
                                <button euiButton euiIconButton euiPrimary euiOutline>
                                    <eui-icon-svg icon="eui-search" />
                                </button>
                            </div>
                        </div>

                        <!-- QUICK FILTERS (expandable, expanded by default) -->
                        <eui-fieldset label="Quick filters" isLarge isExpandable>
                            <div euiInputGroup>
                                <label euiLabel>Criteria</label>
                                <div class="eui-u-flex eui-u-flex-wrap eui-u-flex-gap-s">
                                    <div class="eui-u-inline-flex">
                                        <input id="checkbox1" euiInputCheckBox/>
                                        <label euilabel for="checkbox1">Checkbox 1</label>
                                    </div>
                                    <div class="eui-u-inline-flex">
                                        <input id="checkbox2" euiInputCheckBox/>
                                        <label euilabel for="checkbox2">Checkbox 2</label>
                                    </div>
                                </div>
                            </div>
                            <div euiInputGroup>
                                <label euiLabel for="select">Another criteria</label>
                                <select euiSelect id="select" placeholder="Select something...">
                                    <option [ngValue]="1">option 1</option>
                                    <option [ngValue]="2">option 2</option>
                                </select>
                            </div>
                        </eui-fieldset>

                        <!-- ADVANCED FILTERS (expandable, collapsed by default) -->
                        <eui-fieldset label="Advanced filter" isLarge isExpandable [isExpanded]="false">
                            <div class="eui-u-flex eui-u-flex-column eui-u-mt-m">
                                <div euiInputGroup>
                                    <label euiLabel for="select2">Another criteria</label>
                                    <select euiSelect id="select2" placeholder="Select something...">
                                        <option [ngValue]="1">option 1</option>
                                        <option [ngValue]="2">option 2</option>
                                    </select>
                                </div>
                            </div>
                        </eui-fieldset>

                    </div>
                </eui-page-column-body>
            </eui-page-column>

            <!-- RESULT COLUMN (main content) -->
            <eui-page-column>
                <eui-page-column-header-left-content>
                    <div class="eui-u-f-l">Filter results</div>
                    <div><strong>{{dataSource.length}}</strong>&nbsp;results found</div>
                </eui-page-column-header-left-content>

                <eui-page-column-header-body>
                    <div class="eui-u-flex eui-u-flex-gap-m">
                        <div class="eui-u-f-s">
                            Selected criteria :
                            <br>
                            <a class="eui-u-text-link">Clear all</a>
                        </div>
                        <eui-chip-list>
                            <eui-chip isChipRemovable euiSizeS>criteria 1</eui-chip>
                            <eui-chip isChipRemovable euiSizeS>criteria 2</eui-chip>
                            <eui-chip isChipRemovable euiSizeS>criteria 3</eui-chip>
                        </eui-chip-list>
                    </div>
                </eui-page-column-header-body>

                <eui-page-column-header-right-content>
                    <div class="eui-u-flex">
                        <button euiButton euiSecondary euiSizeS>Secondary action</button>
                        <button euiButton euiPrimary euiSizeS class="eui-u-ml-s">Primary action</button>
                    </div>
                </eui-page-column-header-right-content>

                <eui-page-column-body>
                    @for (data of dataSource; track data; let i = $index) {
                    <eui-card class="eui-u-mb-m">
                        <eui-card-header>
                            <eui-card-header-title>
                                <a class="eui-u-text-link">{{ data.title }}</a>
                            </eui-card-header-title>
                            <eui-card-header-subtitle>{{ data.subtitle }}</eui-card-header-subtitle>
                            <eui-card-header-right-content>
                                <eui-chip euiSuccess>Status</eui-chip>
                                <eui-dropdown class="eui-u-ml-s">
                                    <button euiButton euiBasicButton euiPrimary euiOutline euiSizeS>
                                        Actions
                                        <span euiIconSvg icon="eui-chevron-down"></span>
                                    </button>
                                    <eui-dropdown-content>
                                        <button euiDropdownItem>
                                            <eui-icon-svg icon="eui-edit" class="eui-u-mr-s"/>
                                            Edit
                                        </button>
                                        <button euiDropdownItem>
                                            <eui-icon-svg icon="eui-trash" class="eui-u-mr-s"/>
                                            Delete
                                        </button>
                                    </eui-dropdown-content>
                                </eui-dropdown>
                            </eui-card-header-right-content>
                        </eui-card-header>
                    </eui-card>
                    }
                </eui-page-column-body>

                <eui-page-column-footer>
                    <eui-paginator [length]="dataSource.length"/>
                </eui-page-column-footer>
            </eui-page-column>

        </eui-page-columns>
    </eui-page-content>

    <eui-page-footer>
        <div class="eui-u-ml-auto">
            <button euiButton euiSecondary class="eui-u-mr-m">Secondary action</button>
            <button euiButton euiPrimary>Primary action</button>
        </div>
    </eui-page-footer>
</eui-page>
```

---

## Reference Component (TypeScript)

```typescript
import { Component, ChangeDetectionStrategy } from '@angular/core';

@Component({
    selector: 'app-my-list-page',
    templateUrl: './my-list-page.component.html',
    imports: [
        ...EUI_PAGE,
        ...EUI_DROPDOWN,
        ...EUI_ICON,
        ...EUI_BREADCRUMB,
        ...EUI_BUTTON,
        ...EUI_FIELDSET,
        ...EUI_LABEL,
        ...EUI_INPUT_GROUP,
        ...EUI_INPUT_TEXT,
        ...EUI_INPUT_CHECKBOX,
        ...EUI_SELECT,
        ...EUI_CARD,
        ...EUI_CHIP,
        ...EUI_CHIP_LIST,
        ...EUI_PAGINATOR,
        EuiTooltipDirective,
    ],
    changeDetection: ChangeDetectionStrategy.OnPush,
})
export class MyListPageComponent {
    dataSource: any[] = [];
}
```

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: breadcrumb → header → page-content (columns) → page-footer.
3. **Use `eui-page-columns` with `hasPreventMobileRendering`** inside `eui-page-content`.
4. **Filter column is always the first `eui-page-column`** with `isCollapsible` and a size directive (`euiSize3XL`). It contains the search/filter form.
5. **Result column is always the second `eui-page-column`** (no label attribute on the tag itself). It contains header-left (title + count), header-body (chips), header-right (actions), body (card list), and footer (paginator).
6. **Use `eui-fieldset` with `isExpandable`** to group filter sections. Quick filters are expanded by default; advanced filters are collapsed (`[isExpanded]="false"`).
7. **Use `eui-card`** for each list item. Card header contains: title as a link, subtitle, status chip, and action dropdown.
8. **Use `@for` control flow** (Angular 17+) for iterating over the data source, not `*ngFor`.
9. **Use `eui-paginator`** in the result column footer, bound to the data source length.
10. **Button hierarchy**: primary actions use `euiPrimary`, secondary use `euiSecondary`. Overflow actions go in `eui-dropdown`. Buttons inside columns use `euiSizeS`.
11. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_CARD`).
12. **Use `ChangeDetectionStrategy.OnPush`** on the component.
13. **Omit optional zones** only if explicitly not needed by the user's requirements. When in doubt, include all zones.
14. **Accessibility**: all icon-only buttons must have `aria-label`. Breadcrumb home item must have `ariaLabel="Home"`. Dropdown triggers must have `aria-label`.
