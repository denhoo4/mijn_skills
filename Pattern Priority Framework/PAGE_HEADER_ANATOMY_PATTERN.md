# EUI Page Header Anatomy Pattern — Canonical Structure Reference

## Purpose

This document describes the **Page Header Anatomy** design pattern — the full-featured page header layout used across all EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

### What is this pattern?

The Page Header Anatomy pattern represents the **complete page header with all available options**: breadcrumb navigation, collapsible title, sub-label area with category/status/tags metadata, action items (buttons, overflow dropdown, favorite toggle), and a collapsible body section. It is the go-to layout whenever a page needs to **display rich contextual information, metadata, and global actions** at the top of the page.

---

## Visual Anatomy (decoded from page-header-anatomy.png)

The anatomy image shows a page header with 6 numbered reference markers:

- 1 — **Page breadcrumb**: horizontal navigation trail at the top (Home > Section > Current page)
- 2 — **Page header title** (mandatory): large collapsible title text spanning the left portion of the header
- 3 — **Page header actions**: action buttons and controls aligned to the right of the title row (secondary button, primary button, rounded overflow dropdown, favorite toggle)
- 4 — **Page header subtitle**: row below the title containing a category badge, a status chip, and descriptive text
- 5 — **Page header metadata**: tag icon followed by a chip list of tags with expand/collapse control and a "Manage" action button
- 6 — **Page header body**: collapsible content area below the metadata, containing a card with summary information

---

## ASCII Structure Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│ eui-page                                                                │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 1. PAGE BREADCRUMB  (eui-page-breadcrumb)                         │  │
│  │    [eui-home] Home > Section > Current page                       │  │
│  └───────────────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │ 2. PAGE HEADER TITLE  (eui-page-header [isCollapsible])           │  │
│  │    Page Title - Lorem ipsum dolor sit amet...                     │  │
│  │                                                                   │  │
│  │  ┌─────────────────────────────────────────────────────────────┐  │  │
│  │  │ 4. PAGE HEADER SUBTITLE  (eui-page-header-sub-label)        │  │  │
│  │  │                                                             │  │  │
│  │  │  ┌──────────┐  ┌────────┐                                   │  │  │
│  │  │  │ CATEGORY │  │ STATUS │  Page Sub-title text...           │  │  │
│  │  │  └──────────┘  └────────┘                                   │  │  │
│  │  │                                                             │  │  │
│  │  │  5. PAGE HEADER METADATA (tags)                             │  │  │
│  │  │  [tag:regular] [Tag 01] [Tag 02] [Tag 03] [>]  [Manage]     │  │  │
│  │  └─────────────────────────────────────────────────────────────┘  │  │
│  │                                                                   │  │
│  │  3. PAGE HEADER ACTIONS  (eui-page-header-action-items)     ──┐   │  │
│  │     [Secondary action] [Primary action]                       │   │  │
│  │     [eui-ellipsis-vertical] (rounded overflow dropdown)       │   │  │
│  │     [eui-star] (favorite toggle)                            ──┘   │  │
│  │                                                                   │  │
│  │  ┌─────────────────────────────────────────────────────────────┐  │  │
│  │  │ 6. PAGE HEADER BODY  (eui-page-header-body)                 │  │  │
│  │  │  ┌───────────────────────────────────────────────────────┐  │  │  │
│  │  │  │ eui-card                                              │  │  │  │
│  │  │  │  Expandable custom body content (summary info)        │  │  │  │
│  │  │  └───────────────────────────────────────────────────────┘  │  │  │
│  │  └─────────────────────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

|  #  | Zone Name | EUI Component(s) | Mandatory | Description |
|-----|-----------|-------------------|-----------|-------------|
|  1  | Page Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item` | No | Navigation trail. First item uses `iconSvgName="eui-home"` with `ariaLabel="Home"`. Last item has no `link` (current page). |
|  2  | Page Header Title | `eui-page-header` with `label`, `isCollapsible`, `expandedLabel`, `collapsedLabel` | Yes | Main page title. Supports collapsing via `isCollapsible` with `[isCollapsed]="false"` default. `expandedLabel` and `collapsedLabel` provide toggle button labels. |
|  3  | Page Header Actions | `eui-page-header-action-items` | No | Right-aligned action area. Contains secondary/primary buttons, a rounded overflow `eui-dropdown` (icon `eui-ellipsis-vertical`), and an `eui-icon-toggle` favorite star (`eui-star`). |
|  4  | Page Header Subtitle | `eui-page-header-sub-label` (first row) | No | Sub-label area containing: a category badge (styled `div` with `eui-u-c-bg-secondary-surface`), a status `eui-chip` (`euiInfo`), and free-text description. |
|  5  | Page Header Metadata | `eui-page-header-sub-label` (second row) | No | Tag row with `eui-icon-svg` (`tag:regular`), `eui-chip-list` with `maxVisibleChipsCount` logic, expand/collapse button in `eui-chip-list-additional-content`, and optional "Manage" action button. |
|  6  | Page Header Body | `eui-page-header-body` | No | Collapsible content area below the header metadata. Contains an `eui-card` with `eui-card-content` for summary or contextual information. Visibility controlled by the header collapse state. |

---

## Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-home` | `eui-breadcrumb-item` | Breadcrumb home item (`iconSvgName`) |
| `tag:regular` | `eui-icon-svg` | Tag icon preceding the chip list in metadata row |
| `eui-ellipsis-vertical` | `eui-icon-svg` | Rounded overflow dropdown trigger button |
| `eui-chevron-right` | `eui-icon-svg` | Prefix icon for dropdown menu items + expand tags button |
| `eui-chevron-left` | `eui-icon-svg` | Collapse tags button (when tags are expanded) |
| `eui-star` | `eui-icon-toggle` | Favorite toggle (`iconSvgNameOn` and `iconSvgNameOff`) |

---

## Component Hierarchy (DOM nesting order)

```
eui-page
├── eui-page-breadcrumb
│   └── eui-breadcrumb
│       └── eui-breadcrumb-item (×N)
├── eui-page-header [label, isCollapsible, [isCollapsed], expandedLabel, collapsedLabel]
│   ├── eui-page-header-sub-label.eui-u-flex-gap-2xs
│   │   ├── div.eui-u-flex.eui-u-flex-gap-m  ← subtitle row
│   │   │   ├── div.eui-u-c-bg-secondary-surface.eui-u-ph-s.eui-u-pv-4xs  ← category badge
│   │   │   ├── eui-chip[euiSizeS][euiInfo]  ← status chip
│   │   │   └── (free text)  ← description
│   │   └── div.eui-u-flex.eui-u-flex-align-items-start.eui-u-flex-gap-xs  ← metadata/tags row
│   │       ├── eui-icon-svg [icon="tag:regular"]
│   │       ├── eui-chip-list
│   │       │   ├── @for → eui-chip[euiSizeS] (×N, conditional on maxVisibleChipsCount)
│   │       │   └── eui-chip-list-additional-content
│   │       │       └── button[euiButton][euiBasicButton][euiSecondary][euiSizeS]
│   │       │           └── eui-icon-svg [icon="eui-chevron-right" | "eui-chevron-left"]
│   │       └── button[euiButton][euiBasicButton][euiPrimary][euiSizeS]  ← "Manage"
│   ├── eui-page-header-action-items
│   │   ├── button[euiButton][euiSecondary]
│   │   ├── button[euiButton][euiPrimary]
│   │   ├── eui-dropdown
│   │   │   ├── button[euiButton][euiPrimary][euiBasicButton][euiRounded][euiIconButton]
│   │   │   │   └── eui-icon-svg [icon="eui-ellipsis-vertical"]
│   │   │   └── eui-dropdown-content
│   │   │       └── button[euiDropdownItem] (×N)
│   │   │           └── eui-icon-svg [icon="eui-chevron-right", size="s"]
│   │   └── eui-icon-toggle [iconSvgNameOn="eui-star", iconSvgNameOff="eui-star"]
│   └── eui-page-header-body
│       └── eui-card
│           └── eui-card-content
│               └── p.eui-u-text-paragraph
```

---

## Required Angular Imports

```typescript
import { EUI_PAGE } from '@eui/components/eui-page';
import { EUI_BREADCRUMB } from '@eui/components/eui-breadcrumb';
import { EUI_BUTTON } from '@eui/components/eui-button';
import { EUI_ICON } from '@eui/components/eui-icon';
import { EUI_DROPDOWN } from '@eui/components/eui-dropdown';
import { EUI_CARD } from '@eui/components/eui-card';
import { EUI_CHIP } from '@eui/components/eui-chip';
import { EUI_CHIP_LIST } from '@eui/components/eui-chip-list';
import { EUI_ICON_TOGGLE } from '@eui/components/eui-icon-toggle';
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
            <eui-breadcrumb-item link="/" iconSvgName="eui-home" ariaLabel="Home" />
            <eui-breadcrumb-item id="1" label="Section" link="/"/>
            <eui-breadcrumb-item id="2" label="Current page"/>
        </eui-breadcrumb>
    </eui-page-breadcrumb>

    <eui-page-header
        label="Page Title - Lorem ipsum dolor sit amet, consectetur adipiscing elit."
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

                Page Sub-title - Lorem ipsum dolor sit amet, consectetur adipiscing elit.
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
                                euiButton
                                euiBasicButton
                                euiSecondary
                                euiSizeS
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
                    <button euiDropdownItem aria-label="Action item 3">
                        <eui-icon-svg icon="eui-chevron-right" size="s" class="eui-u-mr-xs" />
                        Extra page action item 3
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
                        Its usage is to display page information that should always be visible on top of the page like a
                        "summary" for example.
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
    selector: 'app-my-page-header',
    templateUrl: './my-page-header.component.html',
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
export class MyPageHeaderComponent {
    chips = [
        { label: 'Tagname 01' },
        { label: 'Tagname 02' },
        { label: 'Tagname 03 with very long label' },
        { label: 'Tagname 04' },
        { label: 'Tagname 05' },
        { label: 'Tagname 06' },
        { label: 'Tagname 07' },
    ];

    maxVisibleChipsCount = 2;
    isMaxVisibleChipsOpened = false;

    toggleTags(): void {
        this.isMaxVisibleChipsOpened = !this.isMaxVisibleChipsOpened;
    }
}
```

---

## Generation Rules

When generating a page header following this pattern, an AI tool **must**:

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: breadcrumb → header (with sub-label → action items → body).
3. **Use `eui-page-header` with `isCollapsible`** and provide `expandedLabel` / `collapsedLabel` for the toggle button labels. Default state is `[isCollapsed]="false"`.
4. **Sub-label uses `eui-page-header-sub-label`** with `class="eui-u-flex-gap-2xs"` containing two rows: the subtitle row (category + status + text) and the metadata/tags row.
5. **Category badge is a styled `div`** with `eui-u-c-bg-secondary-surface eui-u-ph-s eui-u-pv-4xs` — it is NOT an `eui-chip`.
6. **Status uses `eui-chip`** with `euiSizeS` and a semantic directive (`euiInfo`, `euiSuccess`, `euiWarning`, `euiDanger`) depending on the status meaning.
7. **Tags use `eui-chip-list`** with `@for` control flow (Angular 17+), conditional rendering based on `maxVisibleChipsCount`, and an expand/collapse button inside `eui-chip-list-additional-content`. The tag icon is `eui-icon-svg` with `icon="tag:regular"`.
8. **Overflow dropdown uses a rounded icon button**: `euiButton euiPrimary euiBasicButton euiRounded euiIconButton` with `eui-ellipsis-vertical` icon. Dropdown items are prefixed with `eui-icon-svg icon="eui-chevron-right" size="s"`.
9. **Favorite toggle uses `eui-icon-toggle`** with `iconSvgNameOn="eui-star"` and `iconSvgNameOff="eui-star"`.
10. **Header body uses `eui-page-header-body`** containing an `eui-card` > `eui-card-content` for expandable summary content.
11. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_CARD`).
12. **Use `ChangeDetectionStrategy.OnPush`** on the component.
13. **Omit optional zones** only if explicitly not needed by the user's requirements. When in doubt, include all zones.
14. **Accessibility**: the overflow dropdown button must have `euiTooltip="More actions"` and `[attr.aria-label]="'More actions menu'"`. Breadcrumb home item must have `ariaLabel="Home"`. Expand/collapse icons must have `aria-label`.
