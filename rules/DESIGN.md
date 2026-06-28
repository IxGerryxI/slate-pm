---
name: 
colors:
  surface: '#0d131f'
  surface-dim: '#0d131f'
  surface-bright: '#333946'
  surface-container-lowest: '#080e1a'
  surface-container-low: '#161c28'
  surface-container: '#1a202c'
  surface-container-high: '#242a37'
  surface-container-highest: '#2f3542'
  on-surface: '#dde2f3'
  on-surface-variant: '#c3c6d7'
  inverse-surface: '#dde2f3'
  inverse-on-surface: '#2a303d'
  outline: '#8d90a0'
  outline-variant: '#434655'
  surface-tint: '#b4c5ff'
  primary: '#b4c5ff'
  on-primary: '#002a78'
  primary-container: '#2563eb'
  on-primary-container: '#eeefff'
  inverse-primary: '#0053db'
  secondary: '#b7c8e1'
  on-secondary: '#213145'
  secondary-container: '#3a4a5f'
  on-secondary-container: '#a9bad3'
  tertiary: '#ffb596'
  on-tertiary: '#581e00'
  tertiary-container: '#bc4800'
  on-tertiary-container: '#ffede6'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#dbe1ff'
  primary-fixed-dim: '#b4c5ff'
  on-primary-fixed: '#00174b'
  on-primary-fixed-variant: '#003ea8'
  secondary-fixed: '#d3e4fe'
  secondary-fixed-dim: '#b7c8e1'
  on-secondary-fixed: '#0b1c30'
  on-secondary-fixed-variant: '#38485d'
  tertiary-fixed: '#ffdbcd'
  tertiary-fixed-dim: '#ffb596'
  on-tertiary-fixed: '#360f00'
  on-tertiary-fixed-variant: '#7d2d00'
  background: '#0d131f'
  on-background: '#dde2f3'
  surface-variant: '#2f3542'
typography:
  display-sm:
    fontFamily: Geist
    fontSize: 30px
    fontWeight: '600'
    lineHeight: 36px
    letterSpacing: -0.02em
  headline-md:
    fontFamily: Geist
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
    letterSpacing: -0.01em
  headline-sm:
    fontFamily: Geist
    fontSize: 18px
    fontWeight: '500'
    lineHeight: 28px
  body-lg:
    fontFamily: Geist
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-md:
    fontFamily: Geist
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  body-sm:
    fontFamily: Geist
    fontSize: 13px
    fontWeight: '400'
    lineHeight: 18px
  label-md:
    fontFamily: JetBrains Mono
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
    letterSpacing: 0.02em
  label-sm:
    fontFamily: JetBrains Mono
    fontSize: 11px
    fontWeight: '500'
    lineHeight: 14px
    letterSpacing: 0.03em
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  sidebar-width: 64px
  sidebar-expanded: 240px
  gutter: 12px
---

## Brand & Style
The brand personality is precise, efficient, and sophisticated, catering to high-output professionals who require a distraction-free environment. The aesthetic follows a **Modern Minimalist** approach with a focus on information density and technical clarity.

The visual language emphasizes utility over decoration. It utilizes a deep-space background to reduce eye strain during long working sessions, while employing sharp, high-contrast accents to guide the user's focus toward primary actions. The UI should feel like a high-end terminal—responsive, robust, and intentional.

## Colors
The palette is engineered for a premium dark mode experience. The core background is a deep charcoal slate (#121824), providing a grounded base that eliminates glare. Component surfaces use a slightly lighter slate (#1E293B) to create subtle hierarchical separation.

Primary actions and "active" indicators use a vibrant Electric Blue (#2563EB), ensuring high visibility against the dark backdrop. Accents and secondary data visualizations utilize a palette of muted grays and slates to maintain a low cognitive load, reserving color only for critical state changes and progress tracking.

## Typography
This design system uses **Geist** as the primary typeface for its exceptional legibility and technical, monolinear quality that fits a developer-centric or high-power SaaS environment. 

For technical metadata, status tags, and AI dock inputs, **JetBrains Mono** is introduced to provide a distinct "code-adjacent" feel, aiding in the differentiation between content and system labels. The type scale is compact, favoring density over white space to allow more data to be visible on a single screen without scrolling.

## Layout & Spacing
The layout follows a **Fixed-Fluid Hybrid** model optimized for desktop productivity.
- **Narrow Sidebar**: A 64px collapsed rail for icons, expanding to 240px on hover or toggle for full navigation labels.
- **Kanban Columns**: Fixed width of 320px with 12px gutters, allowing horizontal overflow for large project boards.
- **Spacing Rhythm**: A 4px baseline grid is used. Padding within cards and list items is kept tight (8px-12px) to maximize the volume of visible tasks.
- **AI Input Dock**: Positioned at the bottom center of the viewport, fixed with a maximum width of 768px, floating 24px above the bottom edge.

## Elevation & Depth
In this dark UI, depth is communicated through **Tonal Layering** and **Sharp Outlines** rather than heavy shadows.
- **Level 0 (Background)**: #121824 (Base canvas).
- **Level 1 (Surfaces)**: #1E293B (Cards, sidebar, header). These elements use a 1px solid border (#334155) to define edges against the background.
- **Level 2 (Overlays)**: #1E293B with a very subtle 8px blur shadow (Black, 40% opacity). Used for dropdowns and context menus.
- **Active State**: Primary Electric Blue is used as a 2px left-border "accent" or a subtle outer glow for focused inputs.

## Shapes
The shape language is **Soft-Sharp**. While a subtle radius (4px/0.25rem) is applied to all components to prevent the UI from feeling overly aggressive, the general silhouette remains rectangular and disciplined.

Buttons and input fields maintain this 4px radius. Progress bars and status chips use the same logic—avoiding full pills to maintain a professional, structured desktop application aesthetic.

## Components
- **Buttons**: Primary buttons use a solid Electric Blue fill with white text. Secondary buttons are outlined with #334155 and use Geist Medium text.
- **Project Cards**: Feature a 1px border (#334155), a `label-sm` category tag, and a 4px tall progress bar at the bottom edge using Electric Blue for completion status.
- **Kanban Columns**: Transparent backgrounds with a dashed #334155 top border. Headers use `headline-sm` with a numeric task count in `label-md`.
- **AI Input Dock**: A glassmorphic effect with a `backdrop-filter: blur(12px)` and #1E293B at 80% opacity. It features a JetBrains Mono placeholder and a single "Spark" icon for submission.
- **Collapsible Groups**: Task groups in list views use a chevron-left icon (16px) and a subtle hover state highlight (#334155 at 50% opacity).
- **Checkboxes**: Custom square boxes with a 2px radius; Electric Blue fill with a white checkmark when active.
