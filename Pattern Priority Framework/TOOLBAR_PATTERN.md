# EUI App Shell Toolbar Pattern — Canonical Structure Reference

## Purpose

This document describes the **App Shell Toolbar** design pattern — the top-level application toolbar used across all EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

### What is this pattern?

The App Shell Toolbar pattern represents the **horizontal navigation and branding bar at the very top of the application**. It contains the organization logo, the application name, an optional environment indicator, an optional center selector, a set of action items (search, bookmarks, notifications), a user profile dropdown, and a language selector. It is the go-to structure whenever an application needs a **top-level toolbar providing branding, global actions, notifications, user identity, and language switching** in a single compact horizontal bar.

---

## Visual Anatomy

| Marker | Position | Element | Mandatory |
|--------|----------|---------|-----------|
| **1** | Far left | **Logo** — Europa flag logo (`eui-toolbar-logo`) | Yes |
| **2** | Left, after logo | **App name** — Application name text (`eui-toolbar-app`) | Yes |
| **3** | Center | **Center selector** — Context/workspace selector button with icon (`eui-toolbar-center` > `eui-toolbar-selector`) | No |
| **4** | Right area, first group | **Toolbar action items** — Icon buttons for search, bookmarks, notifications (`eui-toolbar-items` > `eui-toolbar-item`) | No |
| **5** | Right area, after items | **User profile** — Avatar with initials and dropdown menu (`eui-user-profile`) | Yes |
| **6** | Far right | **Language selector** — Language switcher (`eui-language-selector`) | Yes |

The environment indicator (`eui-toolbar-environment`) is displayed as a small badge between the app name (2) and the center selector (3), visible only in non-production environments.

---

## ASCII Structure Overview

```
┌──────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ eui-toolbar                                                                                              │
│                                                                                                          │
│  1       2              3                   4                                    5              6        │
│  ┌────┐ ┌─────────┐ ┌──────┐ ┌─────────────────────┐ ┌───────────┐┌────────────┐┌────┐ ┌────────┐ ┌──┐   │
│  │LOGO│ │APP NAME │ │ ENV  │ │  eui-stack          │ │eui-search ││bookmark:   ││bell│ │user:   │ │LN│   │
│  │    │ │         │ │      │ │  CENTER SELECTOR    │ │           ││regular     ││    │ │regular │ │  │   │
│  └────┘ └─────────┘ └──────┘ └─────────────────────┘ └───────────┘└────────────┘└────┘ └────────┘ └──┘   │
│                                                                                                          │
└──────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

|  #  | Zone Name | EUI Component(s) | Mandatory | EUI Icon Value | Description |
|-----|-----------|-------------------|-----------|----------------|-------------|
|  1  | Logo | `eui-toolbar-logo` | Yes | — (Europa flag PNG asset) | Organization logo (Europa flag by default). Clickable, navigates to home route. Self-closing component. |
|  2  | App Name | `eui-toolbar-app` | Yes | — | Application name displayed via `appName` input. Optional subtitle via `appSubTitle`. |
|  3  | Environment | `eui-toolbar-environment` | No | — | Environment indicator badge (e.g., "DEV", "TST", "ACC", "MOCK"). Content projected via `ng-content`. Should be hidden or empty in production. |
|  4  | Center Selector | `eui-toolbar-center` > `eui-toolbar-selector` | No | `eui-stack` | Center-aligned selector button. Uses `iconSvgName="eui-stack"` and `label` inputs. Used for context/workspace switching. |
| 5a  | Search Item | `eui-toolbar-item` > `eui-icon-button` | No | `eui-search` | Icon button for global search. Uses `icon="eui-search"`. |
| 5b  | Bookmark Item | `eui-toolbar-item` > `eui-icon-button` | No | `bookmark:regular` | Icon button for bookmarks/favorites. Uses `icon="bookmark:regular"`. |
| 5c  | Notifications Item | `eui-toolbar-item` > `eui-notifications` | No | — (built-in bell icon) | Notification bell with badge counter and dropdown panel. Bound to a notification items array with `[items]` and `[count]`. |
| 5d  | User Profile Item | `eui-toolbar-item` > `eui-user-profile` | Yes | `user:regular` (profile menu), `eui-sign-out` (sign out menu) | User avatar with initials and dropdown menu. Uses `isShowAvatarInitials` and `[isShowUserInfos]="false"` for compact toolbar display. Contains `eui-user-profile-menu` with `eui-user-profile-menu-item` entries. |
|  6  | Language Selector | `eui-language-selector` | No | — (built-in globe icon) | Language switcher. Adapts display: dropdown for 2–3 languages, modal for 4+. Placed as a direct child of `eui-toolbar`, after `eui-toolbar-items`. |

---

## Icons Reference

All EUI icon values used in this pattern:

| Context | EUI Icon Value | Component | Usage |
|---------|---------------|-----------|-------|
| Center selector | `eui-stack` | `eui-toolbar-selector` | `iconSvgName="eui-stack"` |
| Search action | `eui-search` | `eui-icon-button` | `icon="eui-search"` |
| Bookmark action | `bookmark:regular` | `eui-icon-button` | `icon="bookmark:regular"` |
| User profile menu item | `user:regular` | `eui-icon-svg` | `icon="user:regular"` — "View profile information" |
| Sign out menu item | `eui-sign-out` | `eui-icon-svg` | `icon="eui-sign-out"` — "Sign out" |

---

## Component Hierarchy (DOM nesting order)

```
eui-toolbar
├── eui-toolbar-logo                                                    ← 1
├── eui-toolbar-app [appName]                                           ← 2
├── eui-toolbar-environment                                             ← (between 2 and 3)
│   └── (text content, e.g. "MOCK")
├── eui-toolbar-center                                                  ← 3
│   └── eui-toolbar-selector [label][iconSvgName="eui-stack"]
├── eui-toolbar-items                                                   ← 4
│   ├── eui-toolbar-item  ← search
│   │   └── eui-icon-button [icon="eui-search"]
│   ├── eui-toolbar-item  ← bookmarks
│   │   └── eui-icon-button [icon="bookmark:regular"]
│   ├── eui-toolbar-item  ← notifications
│   │   └── eui-notifications [items][count]
│   └── eui-toolbar-item  ← user profile                               ← 5
│       └── eui-user-profile [isShowAvatarInitials][isShowUserInfos=false]
│           └── eui-user-profile-menu
│               ├── eui-user-profile-menu-item
│               │   ├── eui-icon-svg [icon="user:regular"]
│               │   └── "View profile information"
│               └── eui-user-profile-menu-item
│                   ├── eui-icon-svg [icon="eui-sign-out"]
│                   └── "Sign out"
└── eui-language-selector                                               ← 6
```

---

## Required Angular Imports

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

> **Note**: `EUI_LAYOUT` provides all toolbar structural components (`eui-toolbar`, `eui-toolbar-logo`, `eui-toolbar-app`, `eui-toolbar-environment`, `eui-toolbar-center`, `eui-toolbar-selector`, `eui-toolbar-items`, `eui-toolbar-item`, `eui-notifications`).

---

## Notification Items Data Model

Each notification item follows this structure:

```typescript
{
    label: string;           // Notification title
    subLabel: string;        // Notification description
    metadata: {
        date: Date;          // Timestamp
        read: boolean;       // Read/unread status
        important?: boolean; // Optional importance flag
    };
}
```

---

## Reference Template

```html
<eui-toolbar>
    <eui-toolbar-logo/>
    <eui-toolbar-app appName="appName"/>
    <eui-toolbar-environment>MOCK</eui-toolbar-environment>
    <eui-toolbar-center>
        <eui-toolbar-selector label="Selector label" iconSvgName="eui-stack"/>
    </eui-toolbar-center>
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
        <eui-toolbar-item>
            <eui-user-profile isShowAvatarInitials [isShowUserInfos]="false">
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
            </eui-user-profile>
        </eui-toolbar-item>
    </eui-toolbar-items>
    <eui-language-selector/>
</eui-toolbar>
```

---

## Reference Component (TypeScript)

```typescript
import { Component, ChangeDetectionStrategy } from '@angular/core';

@Component({
    selector: 'app-my-toolbar',
    templateUrl: './my-toolbar.component.html',
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
export class MyToolbarComponent {
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
        {
            label: 'Notification label',
            subLabel: 'this is the description of the notification - subLabel - and this can be very huge too',
            metadata: {
                date: new Date(), read: true, important: true,
            },
        },
        {
            label: 'Notification label',
            subLabel: 'Long notification description text that can span multiple lines.',
            metadata: {
                date: new Date(),
            },
        },
    ];
}
```

---

## Generation Rules

When generating a toolbar following this pattern, an AI tool **must**:

1. **Always use `<eui-toolbar>` as the root element** of the toolbar. This is not an `eui-page` — it is a standalone toolbar component.
2. **Respect the slot ordering**: logo → app name → environment → center → toolbar-items → language-selector.
3. **Use `eui-toolbar-logo`** as the first child for organization branding. It is self-closing and navigates to home by default.
4. **Use `eui-toolbar-app`** with `appName` input for the application name. Optional `appSubTitle` for additional context.
5. **Use `eui-toolbar-environment`** for environment indication. Content is projected via `ng-content` (e.g., "DEV", "TST"). Omit or leave empty in production.
6. **Use `eui-toolbar-center` > `eui-toolbar-selector`** for center-aligned context switching. The selector takes `label` and `iconSvgName` inputs. Default icon: `eui-stack`.
7. **Wrap all right-side action items** inside a single `eui-toolbar-items` container. Each action is wrapped in its own `eui-toolbar-item`.
8. **Use `eui-icon-button`** for icon-only toolbar actions. Use the exact EUI icon values: `eui-search` for search, `bookmark:regular` for bookmarks.
9. **Use `eui-notifications`** for the notification center. Bind `[items]` to the notification data array and `[count]` to the total count.
10. **Use `eui-user-profile`** with `isShowAvatarInitials` and `[isShowUserInfos]="false"` for a compact toolbar avatar. Include `eui-user-profile-menu` with `eui-user-profile-menu-item` entries, each prefixed with an `eui-icon-svg` using the exact icon values: `user:regular` for profile, `eui-sign-out` for sign out.
11. **Place `eui-language-selector`** as the last direct child of `eui-toolbar`, after `eui-toolbar-items`.
12. **Spread EUI token arrays** in the component `imports` (e.g., `...EUI_LAYOUT`, `...EUI_ICON_BUTTON`). Note that `EUI_LAYOUT` provides all toolbar structural components.
13. **Use `ChangeDetectionStrategy.OnPush`** on the component.
14. **Omit optional zones** only if explicitly not needed by the user's requirements. When in doubt, include all zones.
15. **Do not use `eui-page`, `eui-page-header`, or `eui-page-content`** — this pattern is exclusively for the application toolbar, not for page content. It is typically placed inside `eui-app-toolbar` in the app shell.
