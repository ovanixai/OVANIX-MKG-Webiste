# Mobile Optimization — MKG Gestion Website

**Date:** 2026-04-24  
**Scope:** All 7 pages — mobile responsiveness deep dive without touching desktop

---

## What Was Fixed

### 1. Hamburger Menu (all 7 pages)
**Problem:** No mobile navigation at all. All nav links were always visible in a flex row, completely broken on screens ≤900px.

**Fix:** Added `.nav-hamburger` button (3-line → X animation) and a full-screen dark overlay (`.nav-links.open`) toggled by JavaScript. The overlay covers the entire viewport with `position: fixed; inset: 0; z-index: 205; background: rgba(14,12,10,0.97)`.

Mobile-only franchise links (Thaïzone, Yuzu Sushi) are shown directly in the menu since the dropdown is hidden on mobile. Desktop dropdown is preserved via `.nav-desktop-only` / `.nav-mobile-only` classes.

### 2. Logo Height (all 7 pages)
**Problem:** Logo was fixed at `height: 160px` — took up most of the nav on mobile.

**Fix:** Added `height: clamp(48px, 9vw, 72px)` in the `@media (max-width: 900px)` block.

### 3. index.html Layout
- Hidden large `#quote-orb` (700px fixed element causing horizontal scroll)
- Hidden `.scroll-indicator` on mobile
- Hero heading clamped to `clamp(32px, 8vw, 84px)`
- Quote portrait `flex-basis` changed from `420px` to `min(300px, 85vw)`

### 4. carrieres/index.html Layout
- Offres grid forced to single column at 900px (was staying 2-col)
- Hero and offer image heights reduced
- Button touch targets increased: `padding: 14px 22px; font-size: 13px`

### 5. notre-equipe/index.html Layout
- Hero breakpoint changed to 900px (was 768px) — panel padding reduced from 148px top
- Hero photo clip-path removed on mobile
- Managers grid `minmax` reduced from 220px → 140px (was causing overflow)
- Accordion toggle padding and label font scaled down

### 6. promotions/index.html Layout
- Hidden `#hero-orb-1`, `#hero-orb-2`, `#how-orb` (600–700px fixed elements)
- Promo cards grid forced to single column (was using `minmax(340px, 1fr)`)
- Ghost numbers hidden/scaled
- Filter bar padding reduced

### 7. realisations/index.html Layout
- Hero padding reduced from `180px 64px` top
- Timeline image heights reduced gracefully
- Year ghost numbers scaled down

### 8. Franchise pages (thaizone + yuzu-sushi)
- Nav + hamburger + logo fixes applied identically

---

## What Was NOT Changed
- No desktop styles touched (all fixes are inside `@media (max-width: 900px)` or `max-width: 560px`)
- No content, copy, or images modified
- No SEO/meta tags changed

---

## Verification Results

| Check | Result |
|---|---|
| Horizontal scroll at 390px | ✅ None on all 5 tested pages |
| Hamburger menu opens | ✅ Full-screen dark overlay, all links visible |
| Hamburger → X animation | ✅ Smooth 3-line → X on open |
| Close on link click | ✅ Menu closes when navigating |
| Logo size on mobile | ✅ Compact (clamp 48–72px) |
| Desktop nav unchanged | ✅ Full horizontal links, no hamburger shown |
| Desktop layout unchanged | ✅ Confirmed on carrieres, equipe pages |

---

## Screenshots

- [Mobile menu open](assets/mobile-menu-open.png) — dark overlay, X close button, all links
- [Mobile solid nav](assets/mobile-solid-nav.png) — compact logo + hamburger on scroll
- [Desktop hero (carrieres)](assets/desktop-carrieres-hero.png) — confirmed unchanged
