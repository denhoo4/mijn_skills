# ECL Components Reference

European Commission Library components for public-facing EC/EU websites.

## When to Use ECL

- Public-facing sites on ec.europa.eu or europa.eu
- Sites that must follow DG COMM guidelines
- Applications requiring ECL design compliance

For internal apps, use eUI components instead.

## Setup

```bash
# Install ECL package
npm install @eui/ecl
```

```typescript
// Import components
import { ECL_BUTTON } from '@eui/ecl/ecl-button';
import { ECL_CARD } from '@eui/ecl/ecl-card';

@Component({
  standalone: true,
  imports: [...ECL_BUTTON, ...ECL_CARD],
})
```

## Components By Category

### Form Components

| Component | Type | Purpose |
|-----------|------|---------|
| [ecl-checkbox](components/ecl-checkbox.md) | directive | Checkbox input |
| [ecl-radio](components/ecl-radio.md) | directive | Radio buttons |
| [ecl-text-input](components/ecl-text-input.md) | directive | Text input |
| [ecl-text-area](components/ecl-text-area.md) | directive | Textarea |
| [ecl-select](components/ecl-select.md) | directive | Dropdown select |
| [ecl-multiselect](components/ecl-multiselect.md) | component | Multi-select |
| [ecl-date-picker](components/ecl-date-picker.md) | component | Date picker |
| [ecl-range](components/ecl-range.md) | directive | Range slider |
| [ecl-file-upload](components/ecl-file-upload.md) | component | File upload |
| [ecl-search-form](components/ecl-search-form.md) | component | Search form |
| [ecl-form-group](components/ecl-form-group.md) | directive | Form group wrapper |
| [ecl-form-label](components/ecl-form-label.md) | directive | Form label |

### Navigation Components

| Component | Type | Purpose |
|-----------|------|---------|
| [ecl-breadcrumb](components/ecl-breadcrumb.md) | directive | Breadcrumb trail |
| [ecl-menu](components/ecl-menu.md) | component | Navigation menu |
| [ecl-mega-menu](components/ecl-mega-menu.md) | component | Mega menu |
| [ecl-pagination](components/ecl-pagination.md) | directive | Pagination |
| [ecl-tabs](components/ecl-tabs.md) | component | Tab navigation |
| [ecl-link](components/ecl-link.md) | directive | Styled links |
| [ecl-inpage-navigation](components/ecl-inpage-navigation.md) | component | In-page nav |
| [ecl-navigation-list](components/ecl-navigation-list.md) | component | Navigation list |
| [ecl-category-filter](components/ecl-category-filter.md) | component | Category filter |

### Content Components

| Component | Type | Purpose |
|-----------|------|---------|
| [ecl-card](components/ecl-card.md) | component | Content card |
| [ecl-accordion](components/ecl-accordion.md) | component | Accordion |
| [ecl-table](components/ecl-table.md) | directive | Data table |
| [ecl-blockquote](components/ecl-blockquote.md) | component | Blockquote |
| [ecl-content-block](components/ecl-content-block.md) | component | Content block |
| [ecl-content-item](components/ecl-content-item.md) | component | Content item |
| [ecl-featured](components/ecl-featured.md) | component | Featured content |
| [ecl-fact-figures](components/ecl-fact-figures.md) | component | Facts & figures |
| [ecl-file](components/ecl-file.md) | component | File download |
| [ecl-gallery](components/ecl-gallery.md) | component | Image gallery |
| [ecl-timeline](components/ecl-timeline.md) | component | Timeline |
| [ecl-carousel](components/ecl-carousel.md) | component | Carousel |
| [ecl-news-ticker](components/ecl-news-ticker.md) | component | News ticker |

### Layout Components

| Component | Type | Purpose |
|-----------|------|---------|
| [ecl-page-header](components/ecl-page-header.md) | component | Page header |
| [ecl-banner](components/ecl-banner.md) | component | Banner |
| [ecl-splash-page](components/ecl-splash-page.md) | component | Splash/landing page |
| [ecl-sticky-container](components/ecl-sticky-container.md) | component | Sticky container |
| [ecl-separator](components/ecl-separator.md) | directive | Separator/divider |

### Interactive Components

| Component | Type | Purpose |
|-----------|------|---------|
| [ecl-button](components/ecl-button.md) | directive | Button |
| [ecl-modal](components/ecl-modal.md) | component | Modal dialog |
| [ecl-expandable](components/ecl-expandable.md) | component | Expandable section |
| [ecl-popover](components/ecl-popover.md) | component | Popover |
| [ecl-notification](components/ecl-notification.md) | component | Notification |
| [ecl-loading-indicator](components/ecl-loading-indicator.md) | component | Loading spinner |

### Utility Components

| Component | Type | Purpose |
|-----------|------|---------|
| [ecl-icon](components/ecl-icon.md) | directive | ECL icons |
| [ecl-label](components/ecl-label.md) | directive | Label/badge |
| [ecl-tag](components/ecl-tag.md) | directive | Tag |
| [ecl-date-block](components/ecl-date-block.md) | component | Date display |

## Basic Example

```typescript
import { Component } from '@angular/core';
import { ECL_BUTTON } from '@eui/ecl/ecl-button';
import { ECL_CARD } from '@eui/ecl/ecl-card';

@Component({
  standalone: true,
  imports: [...ECL_BUTTON, ...ECL_CARD],
  template: `
    <ecl-card>
      <ecl-card-header>
        <ecl-card-header-title>Card Title</ecl-card-header-title>
      </ecl-card-header>
      <ecl-card-content>
        Content here
      </ecl-card-content>
      <ecl-card-footer>
        <button eclButton eclPrimary>Action</button>
      </ecl-card-footer>
    </ecl-card>
  `,
})
export class MyComponent {}
```

## ECL CSS Classes

ECL uses its own utility classes (prefix `ecl-u-`):

```html
<h2 class="ecl-u-type-heading-2 ecl-u-mt-xl">Heading</h2>
<p class="ecl-u-type-paragraph ecl-u-mt-m">Paragraph text</p>
```

## Support

- ECL Reference: https://ec.europa.eu/component-library
- COMM Europa Management: Europamanagement@ec.europa.eu
- DIGIT eUI Support: DIGIT-EUI-SUPPORT@ec.europa.eu

## See Also

- [ECL home](home.md)
- [ECL component docs](components/)
