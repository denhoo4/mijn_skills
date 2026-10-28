# EUI Advanced Page Header Pattern — Canonical Structure Reference

## Purpose

This document describes the **Advanced Page Header** design pattern — a rich, collapsible page header with metadata, tags, actions, and an expandable body, used across EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

### What is this pattern?

The Advanced Page Header pattern represents a **feature-rich page header** that goes beyond a simple title and actions. It includes a breadcrumb, a collapsible title, a sub-label area with category badge, status chip, description text, and a tag list with expand/collapse control, page-level action buttons with an overflow dropdown and a favorite toggle, and a collapsible body area containing summary content inside a card. It is the go-to layout whenever a page needs to display **detailed entity information at the top** — such as a case detail page, a document overview, a profile page, or any page where the header carries structured metadata (category, status, tags) alongside a collapsible summary section.

---

## Visual Anatomy

The anatomy reference image (`page-header-advanced.png`) shows a page header with the following numbered zones from top to bottom:

| Marker | Position | Element | Mandatory |
|--------|----------|---------|-----------|
| **1** | Top | **Breadcrumb** — Navigation trail (`eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item`). Home icon uses `eui-home`. | No |
| **2** | Below breadcrumb, left | **Page title** — Collapsible title via `label` input on `eui-page-header`. Uses `isCollapsible`, `expandedLabel`, `collapsedLabel`. | Yes |
| **3** | Below title, left | **Sub-label area** — Contains category badge, status chip, description text, and tag list (`eui-page-header-sub-label`). | No |
| **3a** | Inside sub-label, first row | **Category** — Plain text inside a styled `div` with `eui-u-c-bg-secondary-surface`. | No |
| **3b** | Inside sub-label, first row | **Status chip** — `eui-chip` with `euiSizeS` and a status directive (e.g., `euiInfo`). | No |
| **3c** | Inside sub-label, first row | **Description text** — Free text after the category and status. | No |
| **3d** | Inside sub-label, second row | **Tags** — Tag icon (`tag:regular`) followed by `eui-chip-list` with `eui-chip` items, an expand/collapse button, and an optional "Manage" action button. | No |
| **4** | Right of title | **Action items** — Secondary button, primary button, overflow dropdown with ellipsis icon (`eui-ellipsis-vertical`), and a favorite toggle (`eui-icon-toggle` with `eui-star`). | No |
| **5** | Below header, collapsible | **Header body** — Expandable content area (`eui-page-header-body`) containing an `eui-card` with summary information. Controlled by the collapse/expand toggle on the title. | No |

---

## ASCII Structure Overview

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                           │
│  ┌───────────────────────────────────────────────────────────────────────────────┐ │
│  │ 1. BREADCRUMB                                                                 │ │
│  │    eui-home > patterns > Current page                                         │ │
│  └───────────────────────────────────────────────────────────────────────────────┘ │
│  ┌───────────────────────────────────────────────────┬───────────────────────────┐ │
│  │ 2. PAGE TITLE (isCollapsible)                     │ 4. ACTION ITEMS           │ │
│  │    "Page Title - Lorem ipsum..."                  │  [Secondary] [Primary]    │ │
│  │                                                   │  [eui-ellipsis-vertical]  │ │
│  │                                                   │  [eui-star toggle]        │ │
│  ├───────────────────────────────────────────────────┤                           │ │
│  │ 3. SUB-LABEL                                      │                           │ │
│  │  ┌──────────┐ ┌────────┐                          │                           │ │
│  │  │ CATEGORY │ │ STATUS │  Description text...     │                           │ │
│  │  └──────────┘ └────────┘                          │                           │ │
│  │                                                   │                           │ │
│  │  tag:regular [Tag01] [Tag02] [Tag03] [>] [Manage] |                           │ │
│  └───────────────────────────────────────────────────┴───────────────────────────┘ │
│  ┌───────────────────────────────────────────────────────────────────────────────┐ │
│  │ 5. HEADER BODY (collapsible)                                                  │ │
│  │  ┌─────────────────────────────────────────────────────────────────────────┐  │ │
│  │  │ eui-card                                                                │  │ │
│  │  │   Summary content...                                                    │  │ │
│  │  └─────────────────────────────────────────────────────────────────────────┘  │ │
│  └───────────────────────────────────────────────────────────────────────────────┘ │
└────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

|  #  | Zone Name | EUI Component(s) | Mandatory | EUI Icon Value | Description |
|-----|-----------|-------------------|-----------|----------------|-------------|
|  1  | Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item` | No | `eui-home` | Navigation trail. First item uses `iconSvgName="eui-home"` with `ariaLabel="Home"`. Last item has no `link` (current page). |
|  2  | Page Title | `eui-page-header` with `label`, `isCollapsible`, `expandedLabel`, `collapsedLabel` | Yes | — | Collapsible page title. `isCollapsible` enables the expand/collapse toggle. `[isCollapsed]="false"` sets the initial state to expanded. `expandedLabel` and `collapsedLabel` provide the toggle button labels. |
|  3  | Sub-Label | `eui-page-header-sub-label` | No | — | Container for metadata below the title. Uses `eui-u-flex-gap-2xs` for vertical spacing between rows. |
| 3a  | Category | `div` with `eui-u-c-bg-secondary-surface eui-u-ph-s eui-u-pv-4xs` | No | — | Category badge rendered as a styled `div` with background and padding utility classes. |
| 3b  | Status Chip | `eui-chip` with `euiSizeS` and status directive | No | — | Status indicator chip. Uses `euiInfo` (or `euiSuccess`, `euiWarning`, `euiDanger`) for color variant. |
| 3c  | Description | Free text inside the first row `div` | No | — | Description text after category and status. |
| 3d  | Tags | `eui-icon-svg` + `eui-chip-list` + `eui-chip-list-additional-content` | No | `tag:regular`, `eui-chevron-right`, `eui-chevron-left` | Tag icon followed by a chip list with expand/collapse button. Uses `@for` to iterate over chips with `maxVisibleChipsCount` logic. Expand button uses `eui-chevron-right`, collapse uses `eui-chevron-left`. Optional "Manage" action button at the end. |
|  4  | Action Items | `eui-page-header-action-items` | No | `eui-ellipsis-vertical`, `eui-chevron-right`, `eui-star` | Secondary button, primary button, overflow dropdown with rounded icon button (`euiRounded euiIconButton`) using `eui-ellipsis-vertical`, and a favorite toggle (`eui-icon-toggle`) using `eui-star` for both on/off states. Dropdown items are prefixed with `eui-chevron-right` icons. |
|  5  | Header Body | `eui-page-header-body` | No | — | Collapsible content area controlled by the `isCollapsible` toggle on the page header. Contains an `eui-card` > `eui-card-content` with summary information. |

---

## Icons Reference

All EUI icon values used in this pattern:

| Context | EUI Icon Value | Component | Usage |
|---------|---------------|-----------|-------|
| Breadcrumb home | `eui-home` | `eui-breadcrumb-item` | `iconSvgName="eui-home"` |
| Tag icon | `tag:regular` | `eui-icon-svg` | `icon="tag:regular"` — before the chip list |
| Tag expand | `eui-chevron-right` | `eui-icon-svg` | `icon="eui-chevron-right"` — expand tags button |
| Tag collapse | `eui-chevron-left` | `eui-icon-svg` | `icon="eui-chevron-left"` — collapse tags button |
| Overflow menu trigger | `eui-ellipsis-vertical` | `eui-icon-svg` | `icon="eui-ellipsis-vertical"` — more actions button |
| Dropdown item prefix | `eui-chevron-right` | `eui-icon-svg` | `icon="eui-chevron-right"` with `size="s"` — before each dropdown item label |
| Favorite toggle | `eui-star` | `eui-icon-toggle` | `iconSvgNameOn="eui-star"` and `iconSvgNameOff="eui-star"` |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── eui-page-breadcrumb                                                 ← 1
│   └── eui-breadcrumb
│       ├── eui-breadcrumb-item [link="/"][iconSvgName="eui-home"][ariaLabel="Home"]
│       ├── eui-breadcrumb-item [label][link]
│       └── eui-breadcrumb-item [label]  ← current page, no link
├── eui-page-header [label][isCollapsible][isCollapsed=false]           ← 2
│       [expandedLabel="Expand"][collapsedLabel="Collapse"]
│   ├── eui-page-header-sub-label .eui-u-flex-gap-2xs                  ← 3
│   │   ├── div.eui-u-flex.eui-u-flex-gap-m                            ← first row
│   │   │   ├── div.eui-u-c-bg-secondary-surface.eui-u-ph-s.eui-u-pv-4xs  ← 3a CATEGORY
│   │   │   ├── eui-chip [euiSizeS][euiInfo]                           ← 3b STATUS
│   │   │   └── (description text)                                     ← 3c
│   │   └── div.eui-u-flex.eui-u-flex-align-items-start.eui-u-flex-gap-xs  ← second row
│   │       ├── eui-icon-svg [icon="tag:regular"]                      ← 3d tag icon
│   │       ├── eui-chip-list
│   │       │   ├── @for → eui-chip [euiSizeS]  (×N, with maxVisibleChipsCount logic)
│   │       │   └── eui-chip-list-additional-content
│   │       │       └── button[euiButton][euiBasicButton][euiSecondary][euiSizeS]
│   │       │           └── eui-icon-svg [icon="eui-chevron-right" or "eui-chevron-left"]
│   │       └── button[euiButton][euiBasicButton][euiPrimary][euiSizeS]  ← "Manage"
│   ├── eui-page-header-action-items                                    ← 4
│   │   ├── button[euiButton][euiSecondary]
│   │   ├── button[euiButton][euiPrimary]
│   │   ├── eui-dropdown
│   │   │   ├── button[euiButton][euiPrimary][euiBasicButton][euiRounded][euiIconButton]
│   │   │   │   └── eui-icon-svg [icon="eui-ellipsis-vertical"]
│   │   │   └── eui-dropdown-content
│   │   │       └── button[euiDropdownItem] (×N)
│   │   │           └── eui-icon-svg [icon="eui-chevron-right"][size="s"] + label text
│   │   └── eui-icon-toggle [iconSvgNameOn="eui-star"][iconSvgNameOff="eui-star"]
│   └── eui-page-header-body                                           ← 5
│       └── eui-card
│           └── eui-card-content
│               └── (summary content)
```

---

## Required Angular Imports

```typescript
import { EUI_BREADCRUMB } from '@eui/components/eui-breadcrumb';
import { EUI_BUTTON } from '@eui/components/eui-button';
import { EUI_CARD } from '@eui/components/eui-card';
import { EUI_CHIP } from '@eui/components/eui-chip';
import { EUI_CHIP_LIST } from '@eui/components/eui-chip-list';
import { EUI_DROPDOWN } from '@eui/components/eui-dropdown';
import { EUI_ICON } from '@eui/components/eui-icon';
import { EUI_ICON_TOGGLE } from '@eui/components/eui-icon-toggle';
import { EUI_PAGE } from '@eui/components/eui-page';
```

Component `imports` array (spread each token):

```typescript
imports: [
    ...EUI_PAGE,
    ...EUI_BREADCRUMB,
    ...EUI_BUTTON,
    ...EUI_ICON,
    ...EUI_DROPDOWN,
    ...EUI_CARD,
    ...EUI_CHIP,
    ...EUI_CHIP_LIST,
    ...EUI_ICON_TOGGLE,
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

    <eui-page-header
        label="Page Title"
        isCollapsible [isCollapsed]="false"
        expandedLabel="Expand"
        collapsedLabel="Collapse">

        <eui-page-header-sub-label class="eui-u-flex-gap-2xs">

            <div class="eui-u-flex eui-u-flex-gap-m">
                <!-- CATEGORY -->
                <div class="eui-u-c-bg-secondary-surface eui-u-ph-s eui-u-pv-4xs">
                    CATEGORY
                </div>

                <!-- STATUS -->
                <eui-chip euiSizeS euiInfo>
                    STATUS
                </eui-chip>

                Page Sub-title description text.
            </div>

            <!-- OPTIONAL TAGS -->
            <div class="eui-u-flex eui-u-flex-align-items-start eui-u-flex-gap-xs">
                <eui-icon-svg icon="tag:regular" class="eui-u-mt-2xs" />
                <eui-chip-list>
                    @for (chip of chips; let i = $index; track $index) {
                        @if (isMaxVisibleChipsOpened || i <= maxVisibleChipsCount) {
                            <eui-chip euiSizeS>{{ chip.label }}</eui-chip>
                        }
                    }
                    <eui-chip-list-additional-content>
                        @if (maxVisibleChipsCount && chips && chips.length > maxVisibleChipsCount) {
                            <button
                                euiButton euiBasicButton euiSecondary euiSizeS
                                type="button"
                                class="eui-chip-list__expand-button"
                                (click)="toggleTags()">
                                @if (isMaxVisibleChipsOpened) {
                                    <eui-icon-svg icon="eui-chevron-left" aria-label="Collapse icon" />
                                } @else {
                                    <eui-icon-svg icon="eui-chevron-right" aria-label="Expand icon" />
                                }
                            </button>
                        }
                    </eui-chip-list-additional-content>
                </eui-chip-list>
                <!-- Optional Manage action -->
                <button euiButton euiBasicButton euiPrimary euiSizeS>Manage</button>
            </div>
        </eui-page-header-sub-label>

        <eui-page-header-action-items>
            <button euiButton euiSecondary>Secondary action</button>
            <button euiButton euiPrimary>Primary action</button>
            <eui-dropdown>
                <button euiButton euiPrimary euiBasicButton euiRounded euiIconButton euiTooltip="More actions" [attr.aria-label]="'More actions menu'">
                    <eui-icon-svg icon="eui-ellipsis-vertical" />
                </button>
                <eui-dropdown-content>
                    <button euiDropdownItem aria-label="Action item 1">
                        <eui-icon-svg icon="eui-chevron-right" size="s" class="eui-u-mr-xs" />
                        Extra page action item 1
                    </button>
                    <button euiDropdownItem aria-label="Action item 2">
                        <eui-icon-svg icon="eui-chevron-right" size="s" class="eui-u-mr-xs" />
                        Extra page action item 2
                    </button>
                </eui-dropdown-content>
            </eui-dropdown>
            <eui-icon-toggle iconSvgNameOn="eui-star" iconSvgNameOff="eui-star"/>
        </eui-page-header-action-items>

        <eui-page-header-body>
            <eui-card>
                <eui-card-content>
                    <p class="eui-u-text-paragraph">
                        <strong>This is the page header expandable custom body content.</strong>
                        <br>
                        Summary information displayed when the header is expanded.
                    </p>
                </eui-card-content>
            </eui-card>
        </eui-page-header-body>
    </eui-page-header>
</eui-page>
```

---

## Reference Component (TypeScript)

```typescript
import { Component, ChangeDetectionStrategy } from '@angular/core';

@Component({
    selector: 'app-my-advanced-header-page',
    templateUrl: './my-advanced-header-page.component.html',
    imports: [
        ...EUI_PAGE,
        ...EUI_BREADCRUMB,
        ...EUI_BUTTON,
        ...EUI_ICON,
        ...EUI_DROPDOWN,
        ...EUI_CARD,
        ...EUI_CHIP,
        ...EUI_CHIP_LIST,
        ...EUI_ICON_TOGGLE,
    ],
    changeDetection: ChangeDetectionStrategy.OnPush,
})
export class MyAdvancedHeaderPageComponent {
    public chips = [
        { label: 'Tagname 01' },
        { label: 'Tagname 02' },
        { label: 'Tagname 03' },
        { label: 'Tagname 04' },
        { label: 'Tagname 05' },
    ];

    public maxVisibleChipsCount = 2;
    public isMaxVisibleChipsOpened = false;

    public toggleTags(): void {
        this.isMaxVisibleChipsOpened = !this.isMaxVisibleChipsOpened;
    }
}
```

---

## Generation Rules

When generating a page following this pattern, an AI tool **must**:

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: breadcrumb → page-header (with sub-label, actions, body).
3. **Use `eui-page-header` with `isCollapsible`** to enable the expand/collapse toggle on the title. Set `[isCollapsed]="false"` for initially expanded, `expandedLabel` and `collapsedLabel` for the toggle button labels.
4. **Use `eui-page-header-sub-label`** with `class="eui-u-flex-gap-2xs"` for the metadata area below the title. Organize content in two rows: first row for category + status + description, second row for tags.
5. **Render the category** as a plain `div` with utility classes `eui-u-c-bg-secondary-surface eui-u-ph-s eui-u-pv-4xs`. Do not use a chip for the category.
6. **Render the status** as an `eui-chip` with `euiSizeS` and a status directive (`euiInfo`, `euiSuccess`, `euiWarning`, or `euiDanger`).
7. **Render tags** using `eui-icon-svg` with `icon="tag:regular"` followed by `eui-chip-list` with `eui-chip` items. Use `@for` control flow with `maxVisibleChipsCount` logic. Place the expand/collapse button inside `eui-chip-list-additional-content` using `eui-chevron-right` (expand) and `eui-chevron-left` (collapse) icons.
8. **Use `eui-page-header-action-items`** for page-level actions. The overflow dropdown uses a **rounded icon button** (`euiRounded euiIconButton`) with `eui-ellipsis-vertical` icon — this differs from other patterns that use a text button with chevron. Dropdown items are prefixed with `eui-icon-svg` using `icon="eui-chevron-right"` with `size="s"`.
9. **Use `eui-icon-toggle`** for the favorite/star toggle with `iconSvgNameOn="eui-star"` and `iconSvgNameOff="eui-star"`. Place it as the last child of `eui-page-header-action-items`.
10. **Use `eui-page-header-body`** for the collapsible summary content. Place an `eui-card` > `eui-card-content` inside it.
11. **Use `@for` control flow** (Angular 17+) for iterating over chips, not `*ngFor`.
12. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_CHIP`).
13. **Use `ChangeDetectionStrategy.OnPush`** on the component.
14. **Omit optional zones** only if explicitly not needed by the user's requirements. When in doubt, include all zones.
15. **Accessibility**: breadcrumb home item must have `ariaLabel="Home"`. The overflow dropdown trigger must have `[attr.aria-label]="'More actions menu'"` and `euiTooltip="More actions"`. The tag expand/collapse button icons must have `aria-label`.
