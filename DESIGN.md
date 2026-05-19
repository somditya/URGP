---
name: Cinematic Institutionalism
colors:
  surface: '#fff8f8'
  surface-dim: '#dfd8d8'
  surface-bright: '#fff8f8'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f9f2f2'
  surface-container: '#f3ecec'
  surface-container-high: '#ede7e7'
  surface-container-highest: '#e8e1e1'
  on-surface: '#1d1b1b'
  on-surface-variant: '#5a403c'
  inverse-surface: '#333030'
  inverse-on-surface: '#f6efef'
  outline: '#8e706b'
  outline-variant: '#e3beb8'
  surface-tint: '#b52619'
  primary: '#610000'
  on-primary: '#ffffff'
  primary-container: '#8b0000'
  on-primary-container: '#ff907f'
  inverse-primary: '#ffb4a8'
  secondary: '#5b5f62'
  on-secondary: '#ffffff'
  secondary-container: '#e0e3e7'
  on-secondary-container: '#616568'
  tertiary: '#735c00'
  on-tertiary: '#ffffff'
  tertiary-container: '#cca730'
  on-tertiary-container: '#4f3e00'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#ffdad4'
  primary-fixed-dim: '#ffb4a8'
  on-primary-fixed: '#410000'
  on-primary-fixed-variant: '#920703'
  secondary-fixed: '#e0e3e7'
  secondary-fixed-dim: '#c4c7cb'
  on-secondary-fixed: '#181c1f'
  on-secondary-fixed-variant: '#43474b'
  tertiary-fixed: '#ffe088'
  tertiary-fixed-dim: '#e9c349'
  on-tertiary-fixed: '#241a00'
  on-tertiary-fixed-variant: '#574500'
  background: '#fff8f8'
  on-background: '#1d1b1b'
  surface-variant: '#e8e1e1'
  noir-black: '#0B0D0E'
  celluloid-grey: '#5E5E5E'
  alert-gold: '#E4760F'
  institutional-green: '#0B6B39'
typography:
  headline-xl:
    fontFamily: Libre Caslon Text
    fontSize: 48px
    fontWeight: '700'
    lineHeight: 56px
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Libre Caslon Text
    fontSize: 32px
    fontWeight: '700'
    lineHeight: 40px
  headline-md:
    fontFamily: Libre Caslon Text
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  body-lg:
    fontFamily: Hanken Grotesk
    fontSize: 18px
    fontWeight: '400'
    lineHeight: 28px
  body-md:
    fontFamily: Hanken Grotesk
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  label-md:
    fontFamily: Hanken Grotesk
    fontSize: 14px
    fontWeight: '600'
    lineHeight: 20px
    letterSpacing: 0.05em
  headline-lg-mobile:
    fontFamily: Libre Caslon Text
    fontSize: 28px
    fontWeight: '700'
    lineHeight: 36px
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  unit: 8px
  container-max: 1280px
  gutter: 24px
  margin-mobile: 16px
  margin-desktop: 64px
---

## Brand & Style

The design system is engineered for the Satyajit Ray Film & Television Institute (SRFTI) to bridge the gap between rigorous academic administration and the poetic legacy of cinema. The brand personality is **Creative yet Authoritative**—it commands the respect of a national institution while honoring the visual storytelling craft.

The chosen style is **Modern Corporate with Cinematic Motifs**. It utilizes a structured, high-contrast layout that prioritizes accessibility and clarity for grievance redressal. The aesthetic draws from *Film Noir* and classic cinematic title cards, characterized by dramatic use of negative space, sharp horizontal lines reminiscent of film frames, and a sophisticated, dark-mode leaning palette.

**Key visual principles:**
- **Symmetry and Framing:** Use of margins and borders to "frame" content, mimicking a camera viewfinder.
- **Editorial Pace:** Generous white space to ensure the grievance filing process feels calm and methodical rather than chaotic.
- **Subtle Texture:** Minimalist use of grain or very light aperture patterns in background layers to prevent a purely sterile "SaaS" look.

## Colors

The palette is rooted in the "Noir" aesthetic, dominated by deep reds and structural blacks. 

- **Primary (Deep Cinematic Red):** Used for primary actions, navigation accents, and critical status indicators. It evokes the velvet of theater curtains and the intensity of the creative process.
- **Secondary (Ebon):** Provides the structural weight. Used for headers and high-contrast text to ensure authority.
- **Tertiary (Amber/Gold):** Reserved for "Active" states, warnings, or highlighting specific "e-Samadhan" functionality. 
- **Neutral (Parchment):** A soft, off-white background (`#F0E9E9`) that reduces eye strain compared to pure white, providing a tactile, paper-like feel for academic forms.

**Accessibility Note:** High contrast (minimum 7:1) is maintained for all text-on-background combinations to ensure the portal is usable by all members of the student body and faculty.

## Typography

The typography strategy pairs **Libre Caslon Text** (Headings) with **Hanken Grotesk** (Body).

- **Headings:** Libre Caslon Text brings an editorial, "literary" quality that reflects the academic prestige of SRFTI. It should be used for page titles and section headers. Large headings should use slightly tighter letter-spacing to mimic vintage film posters.
- **Body Text:** Hanken Grotesk offers a sharp, contemporary counter-balance. It is highly legible for long-form grievance descriptions and policy documents.
- **Labels:** Use uppercase Hanken Grotesk with increased tracking (letter-spacing) for form labels and metadata to maintain a clean, organized hierarchy.

## Layout & Spacing

The design system employs a **Fixed Grid** philosophy for desktop to maintain a cinematic "aspect ratio" for content, while transitioning to a fluid model for mobile.

- **Grid:** A 12-column grid with a 1280px max-width container. 
- **Rhythm:** An 8px base unit drives all padding and margins. 
- **The "Letterbox" Effect:** Large horizontal margins (64px+) on desktop focus the user's attention on the central form, minimizing distractions during the sensitive process of filing a grievance.
- **Breakpoints:** 
  - Mobile: < 600px (1 column, 16px margins)
  - Tablet: 600px - 1024px (6 columns, 32px margins)
  - Desktop: > 1024px (12 columns, fixed width)

## Elevation & Depth

Hierarchy is established through **Tonal Layers** and **Low-Contrast Outlines** rather than heavy shadows.

- **Surface Levels:** The base page uses the Neutral color. Form containers and cards use a pure white (`#FFFFFF`) surface with a 1px solid border in `celluloid-grey` at 20% opacity.
- **Interactivity:** On hover, cards do not lift; instead, they gain a subtle 2px left-border accent in `primary-red`.
- **Depth:** Modal overlays should use a 60% opacity `noir-black` backdrop with a moderate blur (8px) to keep the focus entirely on the resolution or input task at hand.

## Shapes

The shape language is **Soft (0.25rem)**. 

While the brand is authoritative, entirely sharp corners can feel overly aggressive in a "grievance" context. A subtle 4px radius on buttons and input fields provides a modern touch without losing the institutional "structured" feel. 

- **Buttons:** 4px radius.
- **Cards/Containers:** 8px (rounded-lg) to distinguish major content blocks from smaller UI elements.
- **Avatars/Icons:** Should remain square or slightly rounded to fit the "film frame" motif.

## Components

- **Buttons:** Primary buttons are solid `primary-red` with white text. Secondary buttons are outlined in `noir-black`. Use a "shutter" transition effect (vertical fill) for hover states.
- **Input Fields:** Use a minimalist "Underline" style or a subtle 1px box. Focus states should trigger a `tertiary-gold` border to indicate the "active scene."
- **Progress Steppers:** For multi-part grievance forms, use a design inspired by a **Film Strip**. Each step is a "frame," and completed steps are filled with the primary red.
- **Chips/Status Badges:**
  - *Pending:* Amber/Gold background.
  - *Resolved:* Institutional Green.
  - *Rejected:* Noir Black.
- **Cards:** Used to summarize past grievances. Include a "Scene Number" or "Reference ID" in a bold monospaced font in the top right corner to reinforce the technical/cinematic theme.
- **Alerts:** Use high-contrast banners. Red for urgent actions, Gold for informational warnings.