---
name: App Shell Toolbar Pattern — Canonical Structure Reference
description: Describes the App Shell Toolbar design pattern — the top-level application toolbar providing branding, global actions, notifications, user identity, and language switching in a single horizontal bar. Use when generating an application shell that requires a top-level toolbar with Europa flag logo, application name, optional environment indicator, optional center/workspace selector, global action items (search, bookmarks, notifications), user profile dropdown, and language switching. Requires EUI layout components, eui-icon-button, eui-badge, eui-user-profile, eui-icon, eui-language-selector. Applies to top-level toolbars in MyWorkplace, F&T Portal, DSA, BAEP, and all corporate portals. Related patterns SIMPLE_LAYOUT_PATTERN, FLUID_LAYOUT_PATTERN, NAVIGATION_LAYOUT_PATTERN.
---

# EUI App Shell Toolbar Pattern — Canonical Structure Reference

## Purpose

This document describes the **App Shell Toolbar** design pattern — the top-level application toolbar used across all EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

### What is this pattern?

The App Shell Toolbar pattern represents the **horizontal navigation and branding bar at the very top of the application**. It contains the organization logo, the application name, an optional environment indicator, an optional center selector, a set of action items (search, bookmarks, notifications), a user profile dropdown, and a language selector. It is the go-to structure whenever an application needs a **top-level toolbar providing branding, global actions, notifications, user identity, and language switching** in a single compact horizontal bar.

---

## Visual Anatomy

```
┌──────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ eui-toolbar                                                                                              │
│                                                                                                          │
│  1       2         3          4                        5a         5b        5c    5d           6         │
│  ┌────┐ ┌───────┐ ┌────┐ ┌────────────────┐ ┌─────────┐┌────────┐┌─────┐┌──────────┐ ┌──────────────┐    │
│  │LOGO│ │APP    │ │ENV │ │CENTER SELECTOR │ │ SEARCH  ││BOOKMARK││NOTIF││USER      │ │LANG SELECTOR │    │
│  │    │ │NAME   │ │    │ │                │ │         ││        ││     ││PROFILE   │ │              │    │
│  └────┘ └───────┘ └────┘ └────────────────┘ └─────────┘└────────┘└─────┘└──────────┘ └──────────────┘    │
│                                                                                                          │
└──────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | EUI Icon Value | Description |
|---|-----------|-------------------|-----------|----------------|-------------|
| 1 | Logo | `eui-toolbar-logo` | Yes | — (Europa flag PNG asset) | Europa flag logo, clickable, navigates to home route. Displayed when using the AppShell toolbar layout. The optional environment banner can also be displayed on top of the logo for non-production environments. Self-closing component. |
| 2 | App or Site Name | `eui-toolbar-app` | Yes | — | Application name text displayed via the `appName` input, with optional subtitle via `appSubTitle`. Use appropriate app name, meaningful for your target users. |
| 3 | Environment | `eui-toolbar-environment` | No | — | Environment indicator badge (e.g., "DEV", "TST", "ACC", "MOCK"). Content projected via ng-content. Should be hidden or empty in production. |
| 4 | Workspace Selector | `eui-toolbar-center` containing `eui-toolbar-selector` | No | `eui-stack` | Context or workspace selector button with icon, used for switching between workspaces. Uses `iconSvgName` set to "eui-stack" and a `label` input. Center-aligned within the toolbar. |
| 5a | Search Item | `eui-toolbar-item` containing `eui-icon-button` | No | `eui-search` | Standardized icon button for global search. The icon-button uses `icon` set to "eui-search". |
| 5b | Bookmark Item | `eui-toolbar-item` containing `eui-icon-button` | No | `bookmark:regular` | Standardized icon button for bookmarks/favorites. The icon-button uses `icon` set to "bookmark:regular". |
| 5c | Notifications Item | `eui-toolbar-item` containing `eui-notifications` | No | — (built-in bell icon) | Notification bell with badge counter and dropdown panel. Bound to a notification items array via the `items` input and a count via the `count` input. |
| 5d | User Profile | `eui-toolbar-item` containing `eui-user-profile` | Yes | `user:regular`, `eui-sign-out` | Represents the currently logged-in user with optional dropdown menu containing user profile related actions and sign out action. Uses `isShowAvatarInitials` to display initials and sets `isShowUserInfos` to false for compact toolbar display. |
| 6 | Language Selector | `eui-language-selector` | Yes | — (built-in globe icon) | Application language switcher (dropdown for 2–3 languages, modal for 4+). Placed as a direct child of the toolbar, after the toolbar items container. |

---

## Component Hierarchy (DOM nesting order)

```
eui-toolbar
├── eui-toolbar-logo                                                    ← Zone 1
├── eui-toolbar-app [appName]                                           ← Zone 2
├── eui-toolbar-environment                                             ← Zone 3
│   └── (text content, e.g. "MOCK")
├── eui-toolbar-center                                                  ← Zone 4
│   └── eui-toolbar-selector [label][iconSvgName="eui-stack"]
├── eui-toolbar-items                                                   ← Zones 5a–5d
│   ├── eui-toolbar-item                                                ← 5a search
│   │   └── eui-icon-button [icon="eui-search"]
│   ├── eui-toolbar-item                                                ← 5b bookmarks
│   │   └── eui-icon-button [icon="bookmark:regular"]
│   ├── eui-toolbar-item                                                ← 5c notifications
│   │   └── eui-notifications [items][count]
│   └── eui-toolbar-item                                                ← 5d user profile
│       └── eui-user-profile [isShowAvatarInitials][isShowUserInfos=false]
│           └── eui-user-profile-menu
│               ├── eui-user-profile-menu-item
│               │   ├── eui-icon-svg [icon="user:regular"]
│               │   └── "View profile information"
│               └── eui-user-profile-menu-item
│                   ├── eui-icon-svg [icon="eui-sign-out"]
│                   └── "Sign out"
└── eui-language-selector                                               ← Zone 6
```

---

## Detailed Layout Description

### Root Element

The entire toolbar is wrapped in a single `eui-toolbar` element. This is the sole root — no `eui-page`, `eui-page-header`, or `eui-page-content` is used. The toolbar is typically placed inside `eui-app-toolbar` in the application shell.

### Zone 1 — Logo

The first child of the toolbar is `eui-toolbar-logo`. It is a self-closing component that renders the Europa flag logo. It is clickable and navigates to the application's home route by default. Displayed when using the AppShell toolbar layout. The optional environment banner can also be displayed on top of the logo for non-production environments.

### Zone 2 — App or Site Name

Immediately after the logo, `eui-toolbar-app` displays the application or site name. The name is set via the `appName` input. An optional `appSubTitle` input can provide additional context beneath the name. Use an appropriate app name that is meaningful for your target users.

### Zone 3 — Environment Indicator

Between the app name and the center selector, `eui-toolbar-environment` shows an environment badge. Its content is projected via ng-content (e.g., the text "MOCK", "DEV", "TST", or "ACC"). This element should be omitted or left empty in production environments.

### Zone 4 — Workspace Selector

The `eui-toolbar-center` container holds a `eui-toolbar-selector` element. The selector displays a label (via the `label` input) and a leading icon (via `iconSvgName` set to "eui-stack"). It is a context or workspace selector button used for switching between workspaces, and is center-aligned within the toolbar.

### Zones 5a–5d — Toolbar Action Items and User Profile

A set of icon action buttons for any purpose are wrapped in a single `eui-toolbar-items` container. Each action is individually wrapped in its own `eui-toolbar-item` element. Standardized icon buttons are provided for search, bookmarks, and notifications bell with badge counter. The following order applies:

1. **Search** (5a) — A standardized `eui-icon-button` with its `icon` input set to "eui-search". Provides global search functionality.

2. **Bookmarks** (5b) — A standardized `eui-icon-button` with its `icon` input set to "bookmark:regular". Provides access to bookmarks or favorites.

3. **Notifications** (5c) — An `eui-notifications` component with its `items` input bound to an array of notification metadata objects and its `count` input bound to the total notification count. The component renders a bell icon with a badge counter and opens a dropdown panel listing notifications.

4. **User Profile** (5d) — Represents the currently logged-in user. An `eui-user-profile` component with `isShowAvatarInitials` enabled and `isShowUserInfos` set to false for compact display. It renders a circular avatar showing the user's initials. Inside it, a `eui-user-profile-menu` provides an optional dropdown menu containing user profile related actions and sign out action:
   - The first item contains an `eui-icon-svg` with `icon` set to "user:regular" followed by the text "View profile information".
   - The second item contains an `eui-icon-svg` with `icon` set to "eui-sign-out" followed by the text "Sign out".

### Zone 6 — Language Selector

The last direct child of `eui-toolbar` is `eui-language-selector`. It is placed after the `eui-toolbar-items` container. It serves as the application language switcher and automatically adapts its display mode: a dropdown for 2–3 languages, or a modal for 4 or more languages.

---

## Icons Reference

All EUI icon values used in this pattern:

| Context | EUI Icon Value | Component | Usage |
|---------|---------------|-----------|-------|
| Center selector | `eui-stack` | `eui-toolbar-selector` | Set via `iconSvgName` input |
| Search action | `eui-search` | `eui-icon-button` | Set via `icon` input |
| Bookmark action | `bookmark:regular` | `eui-icon-button` | Set via `icon` input |
| User profile menu item | `user:regular` | `eui-icon-svg` | "View profile information" entry |
| Sign out menu item | `eui-sign-out` | `eui-icon-svg` | "Sign out" entry |

---

## Notification Items Data Model

Each notification item follows this structure:

- **label** — string — Notification title
- **subLabel** — string — Notification description (can be long text)
- **metadata.date** — Date — Timestamp of the notification
- **metadata.read** — boolean — Read/unread status
- **metadata.important** — boolean (optional) — Importance flag

The `items` input on `eui-notifications` expects an array of these objects. The `count` input expects the total number of notifications (typically the array length).

---

## Generation Rules

When generating a toolbar following this pattern, an AI tool **must**:

1. **Always use `eui-toolbar` as the root element** of the toolbar. This is not an `eui-page` — it is a standalone toolbar component.
2. **Respect the slot ordering**: logo → app name → environment → center → toolbar-items → language-selector.
3. **Use `eui-toolbar-logo`** as the first child for organization branding. It is self-closing and navigates to home by default.
4. **Use `eui-toolbar-app`** with the `appName` input for the application name. Optional `appSubTitle` for additional context.
5. **Use `eui-toolbar-environment`** for environment indication. Content is projected via ng-content (e.g., "DEV", "TST"). Omit or leave empty in production.
6. **Use `eui-toolbar-center` containing `eui-toolbar-selector`** for center-aligned context switching. The selector takes `label` and `iconSvgName` inputs. Default icon value: "eui-stack".
7. **Wrap all right-side action items** inside a single `eui-toolbar-items` container. Each action is wrapped in its own `eui-toolbar-item`.
8. **Use `eui-icon-button`** for icon-only toolbar actions. Use the exact EUI icon values: "eui-search" for search, "bookmark:regular" for bookmarks.
9. **Use `eui-notifications`** for the notification center. Bind the `items` input to the notification data array and the `count` input to the total count.
10. **Use `eui-user-profile`** with `isShowAvatarInitials` enabled and `isShowUserInfos` set to false for a compact toolbar avatar. Include `eui-user-profile-menu` with `eui-user-profile-menu-item` entries, each prefixed with an `eui-icon-svg` using the exact icon values: "user:regular" for profile, "eui-sign-out" for sign out.
11. **Place `eui-language-selector`** as the last direct child of `eui-toolbar`, after `eui-toolbar-items`.
12. **Spread EUI token arrays** in the component imports (e.g., `...EUI_LAYOUT`, `...EUI_ICON_BUTTON`). Note that `EUI_LAYOUT` provides all toolbar structural components.
13. **Use `ChangeDetectionStrategy.OnPush`** on the component.
14. **Omit optional zones** only if explicitly not needed by the user's requirements. When in doubt, include all zones.
15. **Do not use `eui-page`, `eui-page-header`, or `eui-page-content`** — this pattern is exclusively for the application toolbar, not for page content. It is typically placed inside `eui-app-toolbar` in the app shell.
16. **Retrieve component documentation** from MCP tools before generating code to ensure correct API usage.

