# ui-spec.md — UI Implementation Contract

> **Stage**: Specify (Stage 2)
> **Applicable Conditions**: Required before coding for projects with frontend interfaces
> **Prerequisite**: Feature list and page routes in `spec.md`; all components here should trace back to spec feature IDs (F-XXX)
> **Update Timing**: Sync updates when the design system changes

---

## Color Scheme

> Colors must use Hex values to avoid vague descriptions like "blue". If dark mode is supported, define two sets of color values.

### Light Theme (Default)

| Purpose | Color Value | Variable Name | Description |
| :--- | :--- | :--- | :--- |
| Primary | `#[HEX]` | `--color-primary` | Brand primary color |
| Primary-Hover | `#[HEX]` | `--color-primary-hover` | Interaction feedback |
| Secondary | `#[HEX]` | `--color-secondary` | Secondary operations |
| Success | `#[HEX]` | `--color-success` | Success state |
| Warning | `#[HEX]` | `--color-warning` | Warning state |
| Error | `#[HEX]` | `--color-error` | Error state |
| Background| `#[HEX]` | `--color-bg` | Page background |
| Text-Main | `#[HEX]` | `--color-text-primary` | Primary text |
| Text-Sub | `#[HEX]` | `--color-text-secondary` | Auxiliary text |
| Border | `#[HEX]` | `--color-border` | Dividers/Borders |

### Dark Theme (As Needed)

> If dark mode is not needed, delete this section.

| Purpose | Color Value (Dark) | Variable Name | Description |
| :--- | :--- | :--- | :--- |
| Background| `#[HEX]` | `--color-bg` | Dark page background |
| Surface | `#[HEX]` | `--color-surface` | Dark card background |
| Text-Main | `#[HEX]` | `--color-text-primary` | Dark mode primary text |
| Border | `#[HEX]` | `--color-border` | Dark mode borders |

## Typography

| Hierarchy | Font Family | Size | Weight | Line Height | Purpose |
| :--- | :--- | :--- | :--- | :--- | :--- |
| H1 | [e.g. Inter] | 32px | 700 | 1.2 | Page Title |
| H2 | [e.g. Inter] | 24px | 600 | 1.3 | Section Title |
| H3 | [e.g. Inter] | 20px | 600 | 1.4 | Subtitle |
| Body | [e.g. Inter] | 16px | 400 | 1.5 | Body Text |
| Small | [e.g. Inter] | 14px | 400 | 1.5 | Helper Text |
| Caption | [e.g. Inter] | 12px | 400 | 1.4 | Notes/Labels |

## Spacing & Radius

| Token | Value | Purpose |
| :--- | :--- | :--- |
| `--space-xs` | 4px | Compact spacing |
| `--space-sm` | 8px | Small spacing |
| `--space-md` | 16px | Default spacing |
| `--space-lg` | 24px | Large spacing |
| `--space-xl` | 32px | Section spacing |
| `--radius-sm` | 4px | Small elements |
| `--radius-md` | 8px | Cards/Buttons |
| `--radius-lg` | 16px | Modals |

## Component Standards

### Buttons

| Type | Style | Purpose |
| :--- | :--- | :--- |
| Primary | Primary color fill, white text | Main actions |
| Secondary | Border, primary color text | Secondary actions |
| Danger | Red fill, white text | Destructive actions |
| Ghost | No border, primary color text | Lightweight actions |

Sizes: `sm` (32px high) / `md` (40px high) / `lg` (48px high)

### Form Inputs

- Default height: 40px | Focus border: `--color-primary` | Error border: `--color-error`
- Disabled state: opacity 0.5, cursor: not-allowed

---

## Page Route List

| Route | Page Name | Linked Feature | Permissions |
| :--- | :--- | :--- | :--- |
| `/` | Home | — | Public |
| `/login` | Login | F-001 | Public |
| `/register` | Register | F-002 | Public |
| `/dashboard` | Dashboard | F-003 | Logged in users |

## Responsive Breakpoints

| Breakpoint | Width | Layout |
| :--- | :--- | :--- |
| Mobile | < 768px | Single column |
| Tablet | 768-1024px | Two columns |
| Desktop | > 1024px | Multi-column |

## Interaction State Definitions

> Every dynamic component must cover the following four states:

| State | UI Presentation | Description |
| :--- | :--- | :--- |
| **Loading** | Skeleton / Spinner | Data is loading |
| **Empty** | Empty state illustration + CTA | No data available |
| **Success** | Toast notification | Operation succeeded |
| **Error** | Inline error message | Operation failed |

---

*AI must consult this file when implementing any UI components to ensure visual consistency.*
