# EUI Page Header Simple Pattern — Canonical Structure Reference

## Purpose

This document describes the **Simple Page Header** design pattern — the minimal page header layout used across all EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

### What is this pattern?

The Simple Page Header pattern represents the **lightest page header variant**: a breadcrumb navigation trail followed by a title, a subtitle, and one or two action buttons. It contains no collapsible behavior, no metadata, no tags, no overflow dropdown, and no expandable body. It is the go-to layout whenever a page needs **only a title, a subtitle, and a small number of direct action buttons** without additional contextual information.

---

## Visual Anatomy (decoded from page-header-simple.png)

The anatomy image shows a simple page header with 4 numbered reference markers:

- 1 — **Page breadcrumb**: horizontal navigation trail at the top (Home > Section > Current page)
- 2 — **Page header title**: large title text spanning the left portion of the header row
- 3 — **Page header actions**: secondary and primary action buttons aligned to the right of the title row
- 4 — **Page header subtitle**: descriptive text line below the title

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
│  │ 2. PAGE HEADER TITLE         │ 3. PAGE HEADER ACTIONS             │  │
│  │    Page Title - Lorem ipsum  │    [Secondary action] [Primary]    │  │
│  │                              │                                    │  │
│  │ 4. PAGE HEADER SUBTITLE      │                                    │  │
│  │    Page Sub-title - Lorem... │                                    │  │
│  └──────────────────────────────┴────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

|  #  | Zone Name | EUI Component(s) | Mandatory | Description |
|-----|-----------|-------------------|-----------|-------------|
|  1  | Page Breadcrumb | `eui-page-breadcrumb` > `eui-breadcrumb` > `eui-breadcrumb-item` | No | Navigation trail. First item uses `iconSvgName="eui-home"` with `ariaLabel="Home"`. Last item has no `link` (current page). |
|  2  | Page Header Title | `eui-page-header` with `label` | Yes | Main page title via the `label` input. No `isCollapsible` — the title is always visible. |
|  3  | Page Header Actions | `eui-page-header-action-items` | No | Right-aligned action area. Contains only direct buttons (secondary and/or primary). No overflow dropdown, no icon toggle. |
|  4  | Page Header Subtitle | `eui-page-header` with `subLabel` | No | Subtitle text via the `subLabel` input. Plain text only — no category badge, no status chip, no tags. |

---

## Icons Reference

| Icon Value | Component | Usage |
|------------|-----------|-------|
| `eui-home` | `eui-breadcrumb-item` | Breadcrumb home item (`iconSvgName`) |

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
│       └── button[euiButton][euiPrimary]
```

---

## Required Angular Imports

```typescript
import { EUI_PAGE } from '@eui/components/eui-page';
import { EUI_BREADCRUMB } from '@eui/components/eui-breadcrumb';
import { EUI_BUTTON } from '@eui/components/eui-button';
import { EUI_ICON } from '@eui/components/eui-icon';
```

Component `imports` array (spread each token):

```typescript
imports: [
    ...EUI_PAGE,
    ...EUI_BREADCRUMB,
    ...EUI_BUTTON,
    ...EUI_ICON,
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
        label="Page Title - Lorem ipsum dolor sit amet, consectetur adipiscing elit."
        subLabel="Page Sub-title : Lorem ipsum dolor sit amet, consectetur adipiscing elit.">

        <eui-page-header-action-items>
            <button euiButton euiSecondary>
                Secondary action
            </button>
            <button euiButton euiPrimary>
                Primary action
            </button>
        </eui-page-header-action-items>

    </eui-page-header>
</eui-page>
```

---

## Reference Component (TypeScript)

```typescript
import { Component, ChangeDetectionStrategy } from '@angular/core';

@Component({
    selector: 'app-my-simple-page-header',
    templateUrl: './my-simple-page-header.component.html',
    imports: [
        ...EUI_PAGE,
        ...EUI_BREADCRUMB,
        ...EUI_BUTTON,
        ...EUI_ICON,
    ],
    changeDetection: ChangeDetectionStrategy.OnPush,
})
export class MySimplePageHeaderComponent {
}
```

---

## Generation Rules

When generating a page header following this pattern, an AI tool **must**:

1. **Always wrap everything** inside a single `<eui-page>` root element.
2. **Respect the zone ordering**: breadcrumb → header (title + subtitle + action items).
3. **Use `eui-page-header` with `label` and `subLabel` inputs** — do NOT use `isCollapsible`, `expandedLabel`, or `collapsedLabel` in this simple variant.
4. **Do NOT use `eui-page-header-sub-label`** — the subtitle is provided via the `subLabel` input directly on `eui-page-header`.
5. **Action items contain only direct buttons** inside `eui-page-header-action-items`. No `eui-dropdown` overflow menu, no `eui-icon-toggle` favorite star. If more than two actions are needed, switch to the **Page Header Anatomy (full)** pattern instead.
6. **Button hierarchy**: primary actions use `euiPrimary`, secondary use `euiSecondary`. No size directive needed (default size).
7. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_PAGE`, `...EUI_BUTTON`).
8. **Use `ChangeDetectionStrategy.OnPush`** on the component.
9. **Omit optional zones** only if explicitly not needed by the user's requirements. When in doubt, include all zones.
10. **Accessibility**: breadcrumb home item must have `ariaLabel="Home"`.
11. **When to use this pattern vs. the full anatomy pattern**: use this simple variant when the page needs only a title, subtitle, and up to two action buttons. If the page requires any of the following — collapsible title, category badge, status chip, tags, overflow dropdown, favorite toggle, or expandable body — use the **Page Header Anatomy** pattern instead.
