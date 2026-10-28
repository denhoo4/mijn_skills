---
name: App Shell Header Pattern — Canonical Structure Reference
description: Describes the App Shell Header design pattern — the top-level application header banner providing branding, user identity, and language switching. Optionally combined with a toolbar row for action items.
---

# EUI App Shell Header Pattern — Canonical Structure Reference

## Pattern Metadata

| Property | Value |
|----------|-------|
| **Applies to** | Top-level application header with EC logo, app name, user profile, and language selector |
| **Triggered when** | Generating an application shell that requires a top-level header banner with EC branding, user identity, and language switching |
| **Requires** | EUI layout components, eui-icon, eui-user-profile, eui-language-selector, optionally eui-icon-button and eui-badge for the toolbar variant |
| **Outputs** | An application header following the App Shell Header pattern |

## Purpose

This document describes the **App Shell Header** design pattern — the top-level application header banner used across all EUI-based applications (MyWorkplace, F&T Portal, DSA, and all corporate portals sharing this architecture).

### What is this pattern?

The App Shell Header pattern represents the **horizontal branding banner at the very top of the application**. It contains the European Commission logo (ECL), the application name, a user profile dropdown with menu, and a language selector. Unlike the toolbar pattern which provides action items (search, bookmarks, notifications), the header is focused on **branding, user identity, and language switching** in a taller, more prominent banner. It can optionally be combined with a toolbar row below it for additional action items.

---

## Variants

This pattern has two variants:

1. **Variant A — Standalone Header** — The app shell header pattern represents the horizontal branding banner at the very top of the application. It contains the European Commission ECL logo (theme and language-aware), the application name, a user profile dropdown with sub-info and menu items (profile and sign out), and a language selector. Use whenever an application needs a prominent top-level header focused on EC branding, user identity, and language switching — without inline action items such as search or notifications.
2. **Variant B — Header with Toolbar** — The app shell header with toolbar pattern combines the header banner (EC logo, application name, user profile, and language selector) with an additional toolbar row below it. The toolbar row provides action items: a search icon button, a bookmark icon button, and a notifications panel with badge counter. Use whenever an application needs both the prominent EC branding header and a secondary row of global action items such as search, bookmarks, and notifications.

---

## Visual Anatomy

The anatomy reference image shows two rows: a header banner on top and an optional toolbar below. The header row has 4 numbered markers and the toolbar row adds a 5th marker:

| Marker | Position | Element | Mandatory |
|--------|----------|---------|-----------|
| **1** | Far left | **Logo** — European Commission ECL logo, clickable, navigates to home route. Automatically adapts to active theme (light/dark) and active language. The optional environment banner can also be displayed on top of the logo for non-production environments. | Yes |
| **2** | Left, after logo | **App or Site name** — Application name text, with optional short name for responsive layouts and optional subtitle for context. Use appropriate app name, meaningful for your target users. | Yes |
| **3** | Right area | **User profile** — Represents currently logged-in user with optional dropdown menu containing user profile related actions and sign-out action. Displays additional user details (e.g., role) via sub-info. | Yes |
| **4** | Far right | **Language selector** — Application language switcher (dropdown for 2–3 languages, modal for 4+). | Yes |
| **5** | Below header, full width | **Toolbar row** (optional) — Secondary toolbar row below the header containing (standardized) action items: search icon button, bookmark icon button, and notifications bell panel with badge counter. Only present in the header with toolbar variant. | No |

---

## Visual Layout

### Variant A — Standalone Header

A single horizontal banner spanning the full width. From left to right: the EC logo occupies the far left, followed by the application name. On the right side, the user profile (showing a welcome message and sub-info) is followed by the language selector at the far right. All elements are vertically centered within the header bar.

### Variant B — Header with Toolbar

The same header banner as Variant A on top, with an additional toolbar row stacked directly below it. The toolbar row contains icon-only action buttons (search, bookmarks) and a notifications component, all wrapped within toolbar item containers inside a toolbar items group. The two rows together form the complete application shell header area.

---

## Zone Descriptions

| # | Zone Name | EUI Component(s) | Mandatory | EUI Icon Value | Description |
|---|-----------|-------------------|-----------|----------------|-------------|
| 1 | Logo | eui-header-logo | Yes | — (ECL logo SVG asset, theme/language-aware) | European Commission ECL logo, clickable, navigates to home route. Automatically adapts to active theme (light/dark) and active language. The optional environment banner can also be displayed on top of the logo for non-production environments. Self-closing component. |
| 2 | App or Site Name | eui-header-app | Yes | — | Application name text, with optional short name for responsive layouts and optional subtitle for context. Use appropriate app name, meaningful for your target users. |
| 3 | User Profile | eui-header-user-profile | Yes | user:regular (profile menu item), eui-sign-out (sign out menu item) | Represents currently logged-in user with optional dropdown menu containing user profile related actions and sign-out action. Displays additional user details (e.g., role) via sub-info. |
| 4 | Language Selector | eui-language-selector | Yes | — (built-in globe icon) | Application language switcher (dropdown for 2–3 languages, modal for 4+). Placed as a direct child of the header, after the user profile. |
| 5 | Toolbar Row (optional) | eui-toolbar containing eui-toolbar-items with eui-toolbar-item wrappers | No | eui-search, bookmark:regular, — (built-in bell for notifications) | Secondary toolbar row below the header containing (standardized) action items: search icon button, bookmark icon button, and notifications bell panel with badge counter. Only present in the header with toolbar variant. |

---

## Detailed Layout Description

### Root Element

**Variant A**: The entire header is wrapped in a single eui-header element. This is the sole root — no eui-page, eui-page-header, or eui-page-content is used.

**Variant B**: A flex-column wrapper div contains the eui-header element followed by the eui-toolbar element as siblings. The wrapper div uses flex display, column direction, and full width utility classes. This wrapper exists only for standalone rendering; in a real eui-app shell, the header goes inside eui-app-header and the toolbar inside eui-app-toolbar.

### Zone 1 — Logo

The first child of eui-header is eui-header-logo. It is a self-closing component that renders the European Commission ECL logo, clickable, navigates to home route. It automatically adapts to the active theme (light/dark) and active language. The optional environment banner can also be displayed on top of the logo for non-production environments.

### Zone 2 — App or Site Name

Immediately after the logo, eui-header-app displays the application name text, with optional short name for responsive layouts and optional subtitle for context. Use appropriate app name, meaningful for your target users.

### Zone 3 — User Profile

The eui-header-user-profile component represents the currently logged-in user with an optional dropdown menu containing user profile related actions and sign-out action. Displays additional user details (e.g., role) via the subInfos input. Inside it, a eui-user-profile-menu contains individual eui-user-profile-menu-item entries:

- The first menu item contains an eui-icon-svg with icon set to "user:regular" followed by the text "View profile information".
- The second menu item contains an eui-icon-svg with icon set to "eui-sign-out" followed by the text "Sign out".

### Zone 4 — Language Selector

The last direct child of eui-header is eui-language-selector. It is placed after eui-header-user-profile. It serves as the application language switcher (dropdown for 2–3 languages, modal for 4+). Self-closing component.

### Zone 5 — Toolbar Row (Variant B only)

A eui-toolbar element is placed as a sibling after eui-header (both children of the wrapper div). Inside it, a eui-toolbar-items container holds individual eui-toolbar-item wrappers for each action. The toolbar row contains (standardized) action items, in order:

1. **Search** — A eui-toolbar-item containing a eui-icon-button with its icon input set to "eui-search".
2. **Bookmarks** — A eui-toolbar-item containing a eui-icon-button with its icon input set to "bookmark:regular".
3. **Notifications** — A eui-toolbar-item containing a eui-notifications component (bell panel with badge counter) with its items input bound to a notification metadata array and its count input bound to the array length.

---

## Component Hierarchy (DOM nesting order)

### Variant A — Standalone Header

The eui-header element contains four direct children in sequence: eui-header-logo (self-closing), eui-header-app (with appName input), eui-header-user-profile (with subInfos input, containing a eui-user-profile-menu with two eui-user-profile-menu-item entries each having an eui-icon-svg followed by text), and eui-language-selector (self-closing).

### Variant B — Header with Toolbar

A wrapper div (with flex display, column direction, and full width utility classes) contains two children:

1. **eui-header** — Identical structure to Variant A: eui-header-logo, eui-header-app, eui-header-user-profile (with profile menu containing two items), and eui-language-selector.

2. **eui-toolbar** — Contains a single eui-toolbar-items container, which in turn holds three eui-toolbar-item wrappers:
   - First item: eui-icon-button with icon "eui-search"
   - Second item: eui-icon-button with icon "bookmark:regular"
   - Third item: eui-notifications with items and count inputs bound to notification data

---

## Icons Reference

All EUI icon values used in this pattern:

| Context | EUI Icon Value | Component | Usage |
|---------|---------------|-----------|-------|
| User profile menu item | user:regular | eui-icon-svg | "View profile information" entry |
| Sign out menu item | eui-sign-out | eui-icon-svg | "Sign out" entry |
| Search action (toolbar variant) | eui-search | eui-icon-button | Set via icon input |
| Bookmark action (toolbar variant) | bookmark:regular | eui-icon-button | Set via icon input |

---

## Notification Items Data Model

Each notification item (used in Variant B) follows this structure:

- **label** — string — Notification title
- **subLabel** — string — Notification description (can be long text)
- **metadata.date** — Date — Timestamp of the notification
- **metadata.read** — boolean — Read/unread status
- **metadata.important** — boolean (optional) — Importance flag

The items input on eui-notifications expects an array of these objects. The count input expects the total number of notifications (typically the array length).

---

## Key Differences from the Toolbar Pattern

| Aspect | Header Pattern | Toolbar Pattern |
|--------|---------------|-----------------|
| Logo | eui-header-logo (ECL logo SVG, theme/language-aware) | eui-toolbar-logo (Europa flag PNG) |
| User profile | eui-header-user-profile (with subInfos, full user info display) | eui-user-profile (compact avatar-only with isShowUserInfos=false) |
| Purpose | Branding and user identity | Navigation and global actions |
| Visual weight | Taller, more prominent banner | Compact single-row bar |
| Action items | Not included (unless combined with toolbar row in Variant B) | Integrated search, bookmarks, notifications |
| Root element | eui-header | eui-toolbar |

---

## Generation Rules

When generating a header following this pattern, an AI tool **must**:

1. **Always use eui-header as the root element** of the header. This is not an eui-page — it is a standalone header component.
2. **Respect the slot ordering**: logo → app name → user profile → language selector.
3. **Use eui-header-logo** as the first child for EC branding. It is self-closing, navigates to home by default, and automatically adapts to active theme (light/dark) and language.
4. **Use eui-header-app** with appName input for the application name. Optional appShortName for responsive layouts, optional appSubTitle for context.
5. **Use eui-header-user-profile** (not eui-user-profile directly) for the user profile in the header. Set subInfos for additional user details (e.g., role). Include eui-user-profile-menu with eui-user-profile-menu-item entries, each prefixed with an eui-icon-svg using the exact icon values: "user:regular" for profile, "eui-sign-out" for sign out.
6. **Place eui-language-selector** as the last direct child of eui-header, after eui-header-user-profile.
7. **For the header+toolbar variant**, place eui-toolbar as a sibling after eui-header, both wrapped in a flex-column div. The toolbar contains eui-toolbar-items with eui-toolbar-item wrappers for action items. Use eui-icon-button with exact icon values: "eui-search" for search, "bookmark:regular" for bookmarks. Use eui-notifications for the notification center with items and count inputs.
8. **Key difference from the toolbar pattern**: the header uses eui-header-logo (ECL logo, theme/language-aware, SVG) instead of eui-toolbar-logo (Europa flag, PNG). The header uses eui-header-user-profile (with subInfos, full user info display) instead of eui-user-profile (compact avatar-only).
9. **Spread EUI token arrays** in the component imports (e.g., ...EUI_LAYOUT, ...EUI_USER_PROFILE). Note that EUI_LAYOUT provides all header and toolbar structural components.
10. **Use ChangeDetectionStrategy.OnPush** on the component.
11. **Omit optional zones** only if explicitly not needed by the user's requirements. When in doubt, include all zones.
12. **Do not use eui-page, eui-page-header, or eui-page-content** — this pattern is exclusively for the application header, not for page content. In a real app, it is placed inside eui-app-header (and optionally eui-app-toolbar for the toolbar row) within the eui-app shell.
13. **Do not add environment indicator, center selector, or mega menu** to the header unless the user explicitly requests them — the header pattern is for branding and user identity. Action items belong in the toolbar row (Variant B) or in the standalone toolbar pattern.
14. **Retrieve component documentation** from MCP tools before generating code to ensure correct API usage.
