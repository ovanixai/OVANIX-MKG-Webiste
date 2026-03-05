# Ennismore — Brand Guidelines
> For use when prompting Claude Code to build a similar website.

---

## Overall Aesthetic

Luxury editorial minimalism. The site feels like a high-end print magazine brought to life — restrained, confident, and culturally aware. No clutter. Every element earns its place.

---

## Typography

- **Primary typeface:** A classic serif (similar to Canela, Freight Display, or Editorial New) — used for all headings and display text. Feels editorial, slightly literary.
- **Secondary typeface:** A clean sans-serif (similar to Suisse Int'l or Aktiv Grotesk) — used for navigation, labels, captions, and body copy.
- **Key typographic move:** Headlines alternate between roman and *italic* within the same line to create rhythm and emphasis. Example: `Inspire *Discovery*`, `*Lifestyle* Collective`, `*In-House* Studios`. The italic word is always the expressive, poetic one.
- Type sizing is bold and generous on hero sections.
- Section labels use small all-caps or spaced-out small text as eyebrow labels (e.g. "WHO WE ARE").

---

## Color Palette

| Role | Value |
|------|-------|
| Background | `#FFFFFF` — pure white, used almost everywhere |
| Primary text | `#111111` or `#1a1a1a` — near-black |
| Logo / Accent | Black |
| Accent colors | None — color comes entirely from photography |
| Footer | White background, black text |

---

## Layout & Spacing

- Extremely **generous whitespace** — large padding between sections.
- Full-bleed **horizontal scrolling carousels** for brand/portfolio grids.
- Section content is center-aligned or left-aligned with wide margins.
- Brand card grid uses a **tight mosaic / asymmetric layout** with images and short taglines underneath.
- **No borders, no dividers** between sections — space alone creates separation.

---

## Imagery

- Full-screen, **cinematic photography** — moody, atmospheric, editorial.
- Hero section is a **full-viewport video or image** with minimal overlaid text.
- Images are dark, warm, and textural — evocative rather than informational.
- Photography feels like it belongs in a luxury travel or lifestyle magazine.

---

## Navigation

- Minimal sticky top nav — logo left, links right.
- Transparent/white nav that sits cleanly over hero content.
- Dropdown menus include **image thumbnails** alongside nav items (mega-menu style).
- Nav links are small, spaced, mixed case.

---

## Motion & Interaction

- Smooth, **slow fade-ins** as content enters the viewport on scroll.
- Hover states on cards are subtle — slight scale or soft overlay.
- Hero video **autoplays, muted, looped**.
- Scrolling feels unhurried and intentional — no aggressive animations.

---

## Voice & Microcopy

- Short, poetic section titles: *"A bustling cocoon"*, *"The freedom of a festival"*, *"A good neighbour with an open house"*
- Tone: sophisticated but not stiff — culturally curious, slightly poetic.
- CTAs are sentence case: "Learn More", "Watch Film".

---

## Components to Replicate

1. **Full-viewport hero** — video background + serif italic headline, minimal overlay text
2. **Section eyebrow label** — small caps label (e.g. "WHO WE ARE") + large serif heading with italic emphasis word
3. **Horizontal scroll carousel** — brand/portfolio cards with image + short poetic tagline
4. **Two-column editorial text blocks** — wide margins, generous line height
5. **Full-bleed image sections** — alternating left/right layout
6. **Minimal footer** — logo + copyright + 4–5 links + social icons (Instagram, LinkedIn)

---

## Quick-Reference Prompt Snippet

Use this block when prompting Claude Code:

```
Design language: luxury editorial minimalism — high-end print magazine aesthetic.
Typography: serif display font (e.g. Canela or Editorial New) for headings; clean sans-serif for body. Headlines mix roman + italic for expressive emphasis on key words.
Colors: pure white background, near-black text (#111), no accent colors — imagery provides all color.
Layout: generous whitespace, no dividers, full-bleed sections, horizontal scroll carousels for card grids.
Imagery: full-viewport cinematic hero video (autoplay, muted, looped); moody editorial photography.
Nav: minimal sticky top bar, logo left, links right, mega-menu dropdowns with image thumbnails.
Motion: slow scroll fade-ins, subtle hover scale, no aggressive animations.
Tone: sophisticated and poetic — short evocative copy, sentence-case CTAs.
```
