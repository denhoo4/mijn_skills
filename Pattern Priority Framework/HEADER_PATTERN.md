# EUI App Shell Header Pattern — Canonical Structure Reference

## Purpose

This document describes the **App Shell Header** design pattern — the top-level application header banner used across all EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

### What is this pattern?

The App Shell Header pattern represents the **horizontal branding banner at the very top of the application**. It contains the European Commission logo (ECL), the application name, a user profile dropdown with menu, and a language selector. Unlike the toolbar pattern which provides action items (search, bookmarks, notifications), the header is focused on **branding, user identity, and language switching** in a taller, more prominent banner. It can optionally be combined with a toolbar row below it for additional action items.

---

## Visual Anatomy

The anatomy reference image (`app-shell-header-anatomy.png`) shows two rows: a header banner on top and an optional toolbar below. The header row has **4 numbered markers** and the toolbar row adds a **5th marker**:

| Marker | Position | Element | Mandatory |
|--------|----------|---------|-----------|
| **1** | Far left | **Logo** — European Commission ECL logo (`eui-header-logo`). Clickable, navigates to home. Adapts to active theme (light/dark) and language. | Yes |
| **2** | Left, after logo | **App name** — Application name text (`eui-header-app`). Displayed via `appName` input. | Yes |
| **3** | Right area | **User profile** — User avatar with name, sub-info, and dropdown menu (`eui-header-user-profile`). Contains `eui-user-profile-menu` with `eui-user-profile-menu-item` entries. | Yes |
| **4** | Far right | **Language selector** — Language switcher (`eui-language-selector`). Adapts display based on number of available languages. | Yes |
| **5** | Below header, full width | **Toolbar row** (optional) — A secondary `eui-toolbar` row containing action items such as search, bookmarks, and notifications. Only present in the header+toolbar variant. | No |

---

## ASCII Structure Overview

### Variant A — Standalone Header

```
┌──────────────────────────────────────────────────────────────────────────────────────┐
│ eui-header                                                                           │
│                                                                                      │
│  1                  2                                    3                  4        │
│  ┌────────────┐    ┌─────────┐                          ┌──────────────┐  ┌──┐       │
│  │EC LOGO     │    │APP NAME │                          │user:regular  │  │LN│       │
│  │(eui-header │    │         │                          │USER PROFILE  │  │  │       │
│  │ -logo)     │    │         │                          │+ subInfos    │  │  │       │
│  └────────────┘    └─────────┘                          └──────────────┘  └──┘       │
│                                                                                      │
└──────────────────────────────────────────────────────────────────────────────────────┘
```

### Variant B — Header with Toolbar

```
┌──────────────────────────────────────────────────────────────────────────────────────┐
│ eui-header                                                                           │
│                                                                                      │
│  1                  2                                    3                  4        │
│  ┌────────────┐    ┌─────────┐                          ┌──────────────┐  ┌──┐       │
│  │EC LOGO     │    │APP NAME │                          │user:regular  │  │LN│       │
│  │            │    │         │                          │USER PROFILE  │  │  │       │
│  └────────────┘    └─────────┘                          └──────────────┘  └──┘       │
├──────────────────────────────────────────────────────────────────────────────────────┤
│ eui-toolbar                                                                5         │
│                                                                                      │
│  ┌───────────┐ ┌──────────────┐ ┌────┐                                               │
│  │eui-search │ │bookmark:     │ │bell│                                               │
│  │           │ │regular       │ │    │                                               │
│  └───────────┘ └──────────────┘ └────┘                                               │
│                                                                                      │
└──────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

|  #  | Zone Name | EUI Component(s) | Mandatory | EUI Icon Value | Description |
|-----|-----------|-------------------|-----------|----------------|-------------|
|  1  | Logo | `eui-header-logo` | Yes | — (ECL logo SVG asset, theme/language-aware) | European Commission logo. Clickable, navigates to home route. Automatically switches between light/dark variants based on active theme and adapts to active language. |
|  2  | App Name | `eui-header-app` | Yes | — | Application name displayed via `appName` input. Optional `appShortName` for responsive layouts, optional `appSubTitle` for context. |
|  3  | User Profile | `eui-header-user-profile` | Yes | `user:regular` (profile menu item), `eui-sign-out` (sign out menu item) | User avatar with name, welcome message, and dropdown menu. Uses `subInfos` input for additional user details (e.g., role). Contains `eui-user-profile-menu` with `eui-user-profile-menu-item` entries, each prefixed with an `eui-icon-svg`. |
|  4  | Language Selector | `eui-language-selector` | Yes | — (built-in globe icon) | Language switcher. Adapts display: dropdown for 2–3 languages, modal for 4+. Placed as a direct child of `eui-header`, after `eui-header-user-profile`. |
|  5  | Toolbar Row (optional) | `eui-toolbar` > `eui-toolbar-items` > `eui-toolbar-item` | No | `eui-search`, `bookmark:regular`, — (built-in bell for notifications) | Secondary toolbar row below the header. Contains action items: search icon button, bookmark icon button, notifications panel. Only used in the header+toolbar variant. |

---

## Icons Reference

All EUI icon values used in this pattern:

| Context | EUI Icon Value | Component | Usage |
|---------|---------------|-----------|-------|
| User profile menu item | `user:regular` | `eui-icon-svg` | `icon="user:regular"` — "View profile information" |
| Sign out menu item | `eui-sign-out` | `eui-icon-svg` | `icon="eui-sign-out"` — "Sign out" |
| Search action (toolbar variant) | `eui-search` | `eui-icon-button` | `icon="eui-search"` |
| Bookmark action (toolbar variant) | `bookmark:regular` | `eui-icon-button` | `icon="bookmark:regular"` |

---

## Component Hierarchy (DOM nesting order)

### Variant A — Standalone Header

```
eui-header                                                              
├── eui-header-logo                                                     ← 1
├── eui-header-app [appName]                                            ← 2
├── eui-header-user-profile [subInfos]                                  ← 3
│   └── eui-user-profile-menu
│       ├── eui-user-profile-menu-item
│       │   ├── eui-icon-svg [icon="user:regular"]
│       │   └── "View profile information"
│       └── eui-user-profile-menu-item
│           ├── eui-icon-svg [icon="eui-sign-out"]
│           └── "Sign out"
└── eui-language-selector                                               ← 4
```

### Variant B — Header with Toolbar

```
div (wrapper)
├── eui-header                                                          
│   ├── eui-header-logo                                                 ← 1
│   ├── eui-header-app [appName]                                        ← 2
│   ├── eui-header-user-profile [subInfos]                              ← 3
│   │   └── eui-user-profile-menu
│   │       ├── eui-user-profile-menu-item
│   │       │   ├── eui-icon-svg [icon="user:regular"]
│   │       │   └── "View profile information"
│   │       └── eui-user-profile-menu-item
│   │           ├── eui-icon-svg [icon="eui-sign-out"]
│   │           └── "Sign out"
│   └── eui-language-selector                                           ← 4
└── eui-toolbar                                                         ← 5
    └── eui-toolbar-items
        ├── eui-toolbar-item
        │   └── eui-icon-button [icon="eui-search"]
        ├── eui-toolbar-item
        │   └── eui-icon-button [icon="bookmark:regular"]
        └── eui-toolbar-item
            └── eui-notifications [items][count]
```

---

## Required Angular Imports

### Variant A — Standalone Header

```typescript
import { EUI_ICON } from '@eui/components/eui-icon';
import { EUI_LANGUAGE_SELECTOR } from '@eui/components/eui-language-selector';
import { EUI_USER_PROFILE } from '@eui/components/eui-user-profile';
import { EUI_LAYOUT } from '@eui/components/layout';
```

Component `imports` array (spread each token):

```typescript
imports: [
    ...EUI_USER_PROFILE,
    ...EUI_LANGUAGE_SELECTOR,
    ...EUI_ICON,
    ...EUI_LAYOUT,
]
```

### Variant B — Header with Toolbar (additional imports)

```typescript
import { EUI_BADGE } from '@eui/components/eui-badge';
import { EUI_ICON } from '@eui/components/eui-icon';
import { EUI_ICON_BUTTON } from '@eui/components/eui-icon-button';
import { EUI_LANGUAGE_SELECTOR } from '@eui/components/eui-language-selector';
import { EUI_USER_PROFILE } from '@eui/components/eui-user-profile';
import { EUI_LAYOUT } from '@eui/components/layout';
```

Component `imports` array (spread each token):

```typescript
imports: [
    ...EUI_ICON_BUTTON,
    ...EUI_BADGE,
    ...EUI_USER_PROFILE,
    ...EUI_ICON,
    ...EUI_LANGUAGE_SELECTOR,
    ...EUI_LAYOUT,
]
```

> **Note**: `EUI_LAYOUT` provides all header and toolbar structural components (`eui-header`, `eui-header-logo`, `eui-header-app`, `eui-header-user-profile`, `eui-toolbar`, `eui-toolbar-items`, `eui-toolbar-item`, `eui-notifications`).

---

## Reference Template — Variant A (Standalone Header)

```html
<eui-header>
    <eui-header-logo />
    <eui-header-app appName="appName" />
    <eui-header-user-profile subInfos="eUI developer">
        <eui-user-profile-menu>
            <eui-user-profile-menu-item>
                <eui-icon-svg icon="user:regular" />
                View profile information
            </eui-user-profile-menu-item>
            <eui-user-profile-menu-item>
                <eui-icon-svg icon="eui-sign-out" />
                Sign out
            </eui-user-profile-menu-item>
        </eui-user-profile-menu>
    </eui-header-user-profile>
    <eui-language-selector />
</eui-header>
```

---

## Reference Template — Variant B (Header with Toolbar)

```html
<eui-header>
    <eui-header-logo />
    <eui-header-app appName="appName" />
    <eui-header-user-profile subInfos="eUI developer">
        <eui-user-profile-menu>
            <eui-user-profile-menu-item>
                <eui-icon-svg icon="user:regular" />
                View profile information
            </eui-user-profile-menu-item>
            <eui-user-profile-menu-item>
                <eui-icon-svg icon="eui-sign-out" />
                Sign out
            </eui-user-profile-menu-item>
        </eui-user-profile-menu>
    </eui-header-user-profile>
    <eui-language-selector />
</eui-header>
<eui-toolbar>
    <eui-toolbar-items>
        <eui-toolbar-item>
            <eui-icon-button icon="eui-search"/>
        </eui-toolbar-item>
        <eui-toolbar-item>
            <eui-icon-button icon="bookmark:regular"/>
        </eui-toolbar-item>
        <eui-toolbar-item>
            <eui-notifications [items]="notificationItemsMetadata" [count]="notificationItemsMetadata.length"/>
        </eui-toolbar-item>
    </eui-toolbar-items>
</eui-toolbar>
```

> **Note**: In a real `eui-app` shell, the header is placed inside `eui-app-header` and the toolbar inside `eui-app-toolbar`. The wrapper `div` in the sample is only for standalone rendering purposes.

---

## Reference Component — Variant A (Standalone Header)

```typescript
import { Component, ChangeDetectionStrategy } from '@angular/core';

@Component({
    selector: 'app-my-header',
    templateUrl: './my-header.component.html',
    imports: [
        ...EUI_USER_PROFILE,
        ...EUI_LANGUAGE_SELECTOR,
        ...EUI_ICON,
        ...EUI_LAYOUT,
    ],
    changeDetection: ChangeDetectionStrategy.OnPush,
})
export class MyHeaderComponent {
}
```

---

## Reference Component — Variant B (Header with Toolbar)

```typescript
import { Component, ChangeDetectionStrategy } from '@angular/core';

@Component({
    selector: 'app-my-header-toolbar',
    templateUrl: './my-header-toolbar.component.html',
    imports: [
        ...EUI_ICON_BUTTON,
        ...EUI_BADGE,
        ...EUI_USER_PROFILE,
        ...EUI_ICON,
        ...EUI_LANGUAGE_SELECTOR,
        ...EUI_LAYOUT,
    ],
    changeDetection: ChangeDetectionStrategy.OnPush,
})
export class MyHeaderToolbarComponent {
    notificationItemsMetadata = [
        {
            label: 'Notification label',
            subLabel: 'this is the description of the notification - subLabel - and this can be very huge too',
            metadata: {
                date: new Date(), read: false, important: true,
            },
        },
        {
            label: 'Notification label',
            subLabel: 'this is the description of the notification - subLabel - and this can be very huge too',
            metadata: {
                date: new Date(), read: true,
            },
        },
    ];
}
```

---

## Generation Rules

When generating a header following this pattern, an AI tool **must**:

1. **Always use `<eui-header>` as the root element** of the header. This is not an `eui-page` — it is a standalone header component.
2. **Respect the slot ordering**: logo → app name → user profile → language selector.
3. **Use `eui-header-logo`** as the first child for EC branding. It is self-closing, navigates to home by default, and automatically adapts to active theme (light/dark) and language.
4. **Use `eui-header-app`** with `appName` input for the application name. Optional `appShortName` for responsive layouts, optional `appSubTitle` for context.
5. **Use `eui-header-user-profile`** (not `eui-user-profile` directly) for the user profile in the header. Set `subInfos` for additional user details (e.g., role). Include `eui-user-profile-menu` with `eui-user-profile-menu-item` entries, each prefixed with an `eui-icon-svg` using the exact icon values: `user:regular` for profile, `eui-sign-out` for sign out.
6. **Place `eui-language-selector`** as the last direct child of `eui-header`, after `eui-header-user-profile`.
7. **For the header+toolbar variant**, place `eui-toolbar` as a sibling after `eui-header`. The toolbar contains `eui-toolbar-items` > `eui-toolbar-item` wrappers for action items. Use `eui-icon-button` with exact icon values: `eui-search` for search, `bookmark:regular` for bookmarks. Use `eui-notifications` for the notification center.
8. **Key difference from the toolbar pattern**: the header uses `eui-header-logo` (ECL logo, theme/language-aware, SVG) instead of `eui-toolbar-logo` (Europa flag, PNG). The header uses `eui-header-user-profile` (with `subInfos`, full user info display) instead of `eui-user-profile` (compact avatar-only).
9. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_LAYOUT`, `...EUI_USER_PROFILE`). Note that `EUI_LAYOUT` provides all header and toolbar structural components.
10. **Use `ChangeDetectionStrategy.OnPush`** on the component.
11. **Omit optional zones** only if explicitly not needed by the user's requirements. When in doubt, include all zones.
12. **Do not use `eui-page`, `eui-page-header`, or `eui-page-content`** — this pattern is exclusively for the application header, not for page content. In a real app, it is placed inside `eui-app-header` (and optionally `eui-app-toolbar` for the toolbar row) within the `eui-app` shell.
13. **Do not add environment indicator, center selector, or mega menu** to the header unless the user explicitly requests them — the header pattern is for branding and user identity. Action items belong in the toolbar row (variant B) or in the standalone toolbar pattern.
