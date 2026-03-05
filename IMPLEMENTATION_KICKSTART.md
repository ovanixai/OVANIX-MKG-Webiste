# IMPLEMENTATION KICKSTART — MKG Gestion Website

> Complete blueprint to reproduce the OVANIX-MKG website from scratch.
> Language: French (Québec) · Stack: Vanilla HTML/CSS/JS · No build step required.

---

## 1. Project Overview

| Property | Value |
|----------|-------|
| **Company** | MKG Gestion — restaurant franchise management group |
| **Franchises** | Thaïzone (Thai cuisine) · Yuzu Sushi (Japanese) |
| **Location** | Québec, Canada |
| **Language** | French (lang="fr") |
| **Stack** | Single-file HTML pages, inline CSS, inline JS, Tailwind CDN |
| **Server** | `node serve.mjs` → localhost:3000 |
| **Screenshots** | `node screenshot.mjs http://localhost:3000` → `temporary screenshots/` |

---

## 2. File & Folder Structure

```
/
├── index.html                          # Homepage (main)
├── carrieres/
│   └── index.html                      # Careers page
├── nos-franchises/
│   ├── thaizone/
│   │   └── index.html                  # Thaïzone restaurant directory
│   └── yuzu-sushi/
│       └── index.html                  # Yuzu Sushi restaurant directory
├── brand_assets/
│   ├── MKG Logo.png                    # 2.0 MB — primary logo (white/black dual-use)
│   ├── thaizone logo vrai.png          # 14 KB — Thaïzone brand logo
│   ├── yuzu suhi logo.png              # 8.1 KB — Yuzu Sushi brand logo
│   ├── max image.jpg                   # 104 KB — founder portrait (Max Kirchbach)
│   ├── carriere section 1 image.avif   # 81 KB — careers hero image
│   ├── quote section.png               # 1.1 MB — reference image
│   └── spherical & co layout.png       # 4.9 MB — layout reference
├── serve.mjs                           # HTTP server (port 3000)
├── screenshot.mjs                      # Puppeteer full-page capture
├── screenshot-section.mjs              # Section-specific capture
├── package.json                        # puppeteer 22.0.0
└── CLAUDE.md                           # Project rules
```

---

## 3. Design System

### 3.1 Typography

| Role | Font | Weights | Usage |
|------|------|---------|-------|
| **Display / Heading** | Playfair Display, serif | 400, 500, italic | H1, H2, H3, stats, blockquotes |
| **Body / UI** | DM Sans, sans-serif | 300, 400, 500 | All body text, nav, buttons, labels |

**Google Fonts import:**
```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,500;1,400;1,500&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&display=swap" rel="stylesheet">
```

**Type scale:**
- Hero H1: `clamp(48px, 6vw, 84px)` · line-height: 1.05 · letter-spacing: -0.025em
- Section H2: `clamp(34px, 4vw, 56px)` · line-height: 1.08 · letter-spacing: -0.025em
- Blockquote: `clamp(26px, 3.2vw, 44px)` · line-height: 1.32 · italic
- Eyebrow labels: 10.5–11px · letter-spacing: 0.2em · uppercase · color: #999
- Body paragraphs: 17px · line-height: 1.85 · weight: 300 · color: #444
- Small body: 14–15px · line-height: 1.72–1.88 · color: #666
- Nav links: 13px · letter-spacing: 0.03em
- CTA buttons: 11–12px · letter-spacing: 0.1–0.12em · uppercase

### 3.2 Color Palette

| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#fff` | Page background, cards |
| `--ink` | `#111` | Primary text, active states |
| `--ink-2` | `#444` | Body paragraphs |
| `--ink-3` | `#666` | Secondary text, descriptions |
| `--ink-4` | `#888` / `#999` | Eyebrows, labels |
| `--ink-5` | `#aaa` | Footer text, muted labels |
| `--hero-dark-1` | `#0e0d0a` | Hero background darkest |
| `--hero-dark-2` | `#1a1510` | Hero background mid |
| `--hero-dark-3` | `#2d2416` | Hero background highlight |
| `--hero-bloom` | `rgba(200,160,90,0.12)` | Gold bloom overlay |
| `--quote-dark-1` | `#14130e` | Quote section darkest |
| `--quote-dark-2` | `#181410` | Quote section mid |
| `--quote-dark-3` | `#1e1a12` | Quote section light |
| `--quote-glow` | `rgba(180,140,70,0.1)` | Quote radial glow |
| `--thaizone` | `#E91E8C` | Thaïzone brand accent (magenta) |
| `--yuzu` | `#D4A547` | Yuzu Sushi brand accent (gold) |
| `--border` | `rgba(0,0,0,0.07)` | Subtle dividers, card borders |
| `--nav-solid-bg` | `rgba(255,255,255,0.97)` | Nav after scroll |
| `--careers-dark` | `#0f1523` | Careers values section dark panel |

### 3.3 Spacing Tokens

| Token | Value | Usage |
|-------|-------|-------|
| Section padding (desktop) | `128px 64px` | All main sections |
| Section padding (900px) | `88px 28px` | Tablet breakpoint |
| Section padding (mobile) | `80px 28px` | Mobile |
| Content max-width | `1360px` | All section-inner containers |
| Nav padding (expanded) | `28px 64px` | Homepage transparent state |
| Nav padding (solid) | `18px 64px` | After 60px scroll |
| Hero content padding | `0 64px 88px` | Hero bottom alignment |
| Footer padding | `72px 64px 40px` | Footer desktop |
| Grid gap (tight) | `2px` | Values cards grid |
| Grid gap (medium) | `14px` | Franchise + portfolio grids |
| Grid gap (large) | `20px` | Job offers grid |

### 3.4 Animation System

**Fade-up (scroll reveal):**
```css
.fade-up {
  opacity: 0;
  transform: translateY(36px);
  transition: opacity 1s cubic-bezier(0.16, 1, 0.3, 1),
              transform 1s cubic-bezier(0.16, 1, 0.3, 1);
}
.fade-up.d1 { transition-delay: 0.12s; }
.fade-up.d2 { transition-delay: 0.24s; }
.fade-up.d3 { transition-delay: 0.38s; }
.fade-up.d4 { transition-delay: 0.54s; }
.fade-up.visible { opacity: 1; transform: translateY(0); }
```

**Easing:** `cubic-bezier(0.16, 1, 0.3, 1)` — spring-like, used for all transitions
**Hover scale:** `transform: scale(1.04)` on images · 0.7–0.8s duration
**Scroll pulse (hero indicator):** `scrollPulse` keyframe, top: -100% → 200%, 2.2s ease-in-out infinite

**IntersectionObserver settings:**
- threshold: 0.1
- rootMargin: `'0px 0px -44px 0px'`
- Hero elements triggered on `window load` with 100ms setTimeout

### 3.5 Breakpoints

| Breakpoint | Value | Changes |
|------------|-------|---------|
| Desktop | > 900px | Full layout |
| Tablet | ≤ 900px | Nav padding shrinks, single-column sections, franchise cards 380px tall |
| Mobile | ≤ 768px | Quote section reverses to column, hero padding-top 104px (careers) |
| Small mobile | ≤ 560px | Values grid becomes 1-col, jobs grid becomes 1-col |

---

## 4. Global CSS Rules

```css
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; }
body {
  background: #fff;
  color: #111;
  font-family: 'DM Sans', sans-serif;
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
}
.serif { font-family: 'Playfair Display', serif; }
.eyebrow {
  font-size: 10.5px;
  font-weight: 400;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: #999;
}
.section { padding: 128px 64px; }
.section-inner { max-width: 1360px; margin: 0 auto; }
```

---

## 5. Page-by-Page Blueprint

---

### 5.1 Homepage (`index.html`)

**Page title:** `MKG Gestion — Restauration · Franchise · Québec`

#### SECTION 1: Navigation (`#main-nav`)

- **Position:** Fixed top, z-index: 200
- **States:**
  - **Transparent (default):** padding 28px 64px · logo filter: brightness(0) invert(1) · links color: rgba(255,255,255,0.85)
  - **Solid (scrollY > 60):** background rgba(255,255,255,0.97) · box-shadow 0 1px 0 rgba(0,0,0,0.07) · padding 18px 64px · backdrop-filter blur(12px) · logo filter: brightness(0)
- **Logo:** `brand_assets/MKG Logo.png` · height: 160px · transition: filter 0.4s ease
- **Nav items (left to right):**
  1. "Nos Franchises" — dropdown trigger (button, not anchor)
  2. "Nos Valeurs" → `#valeurs`
  3. "Engagement" → `#engagement`
  4. "Carrières" → `/carrieres/`
  5. "Nos Succursales" → `#franchises` — styled as `.nav-cta` (bordered button)

**Franchise Dropdown:**
- Chevron SVG: 10×6px, rotates 180° when open
- Dropdown panel: background rgba(14,13,10,0.97) transparent · border 1px rgba(255,255,255,0.08) · backdrop-filter blur(14px) · min-width 176px · padding 8px 0
- On solid nav: background rgba(255,255,255,0.98) · border rgba(0,0,0,0.09) · box-shadow 0 8px 32px rgba(0,0,0,0.09)
- Items: colored dot (6px circle) + text
  - Thaïzone: dot `#E91E8C`
  - Yuzu Sushi: dot `#D4A547`
- Dropdown opens on mouseenter AND click, closes on mouseleave, outside click, Escape key
- ARIA: aria-haspopup, aria-expanded, aria-controls, role="menu", role="menuitem"

---

#### SECTION 2: Hero (`#hero`)

- **Height:** 100vh · min-height: 680px · align-items: flex-end
- **Layers (bottom to top):**
  1. `#hero-bg` — `radial-gradient(ellipse 120% 80% at 70% 40%, #2d2416 0%, #1a1510 45%, #0e0d0a 100%)` · parallax on scroll: `translateY(scrollY * 0.28px)`
  2. `#hero-bg::after` — SVG fractalNoise texture (baseFrequency 0.75, 4 octaves) · opacity 0.6 · mix-blend-mode: overlay
  3. `#hero-bloom` — `radial-gradient(ellipse at center, rgba(200,160,90,0.12) 0%, transparent 70%)` · 900×600px centered at top
  4. `#hero-overlay` — `linear-gradient(to top, rgba(0,0,0,0.72) 0%, rgba(0,0,0,0.18) 45%, rgba(0,0,0,0.05) 100%)`
  5. `.hero-content` — actual text, z-index: 2
- **Content (`.hero-content`, padding 0 64px 88px, max-width 1360px):**
  - Eyebrow: "Restauration · Franchise · Québec" · 11px · rgba(255,255,255,0.55) · mb: 22px
  - H1: "MKG Gestion : En tête des *saveurs* de demain." · `<em>` for italic "saveurs" · max-width: 780px
  - Subtitle (16px, weight 300, rgba(255,255,255,0.62), max-width 480px, mt 28px): "Un groupe de gestion de premier plan supervisant un portefeuille de plus de 10 établissements Thaïzone et Yuzu Sushi. Alliant rigueur opérationnelle et passion pour l'hospitalité."
  - CTA link: "Découvrez Nos Succursales" → `#franchises` · `.hero-cta` class · animated underline 52px→80px on hover
- **Scroll indicator** (position absolute, bottom: 44px, right: 64px):
  - Vertical line: 1px × 54px · rgba(255,255,255,0.25) · animated pulse overlay
  - Label: "Défiler" · 10px · writing-mode: vertical-rl · rgba(255,255,255,0.35)
- **Fade-up classes:** eyebrow (no delay), h1 (.d1), subtitle (.d2), CTA (.d3) — triggered on window load

---

#### SECTION 3: Mission Statement (`#about`)

- `.section` padding · 2-column grid: `1fr 1fr` · gap: 96px · align-items: start
- **Left column:**
  - Eyebrow (mb 22px): "Notre mission"
  - H2: "L'excellence à chaque *bouchée*, l'intégrité à chaque *opération*." · max-width none
- **Right column** (padding-top: 52px):
  - Para 1: "Chez MKG Gestion, nous ne gérons pas seulement des restaurants ; nous cultivons des destinations culinaires. Nous comblons l'écart entre l'efficacité d'entreprise et la passion authentique de la restauration locale."
  - Para 2: "Garantissant une expérience de classe mondiale à chaque client, à travers chacun de nos établissements au Québec."
  - **Stats row** (flex, gap 52px, mt 52px):
    - `10+` · "Établissements" — superscript `+` in 0.6em normal font
    - `2 franchises` · "Sous gestion" — "franchises" in 0.55em normal font
    - `100%` · "Passion québécoise" — `%` in 0.55em normal font
  - Stat number: Playfair 48px · weight 400 · letter-spacing -0.02em
  - Stat label: 11px · letter-spacing 0.12em · uppercase · color #999 · mt 10px

---

#### SECTION 4: Full-Bleed Quote (`#quote-section`)

- **Not** a `<section>` tag — uses `<div>`
- min-height: 62vh · padding: 80px 0 · display: flex · align-items: center · overflow: hidden
- **Layers:**
  1. `#quote-bg` — `linear-gradient(120deg, #181410 0%, #1e1a12 50%, #14130e 100%)` + `::after` radial glow rgba(180,140,70,0.1)
  2. `#quote-overlay` — rgba(0,0,0,0.25)
  3. `#quote-inner` — z-index 2, flex row, gap 64px, max-width 1360px, padding 0 64px
- **Left column (`#quote-text-col`, flex:1):**
  - Blockquote (Playfair italic): "Gérer un restaurant, c'est d'abord choisir d'être présent — pour l'équipe, pour le client, pour la communauté."
  - Attribution: "— FONDATEUR, MAX KIRCHBACH" · 12px · letter-spacing 0.14em · uppercase · rgba(255,255,255,0.38) · mt 28px
- **Right column (`#quote-img-col`, flex: 0 0 420px):**
  - Image: `brand_assets/max image.jpg` · 420×480px · object-fit: cover · object-position: center top
  - `::before` gradient: left-to-right #181410→transparent (40%) — blends image into background
  - `::after` gradient: top #14130e→transparent (30%) — blends image bottom
- **Mobile (≤768px):** flex-direction: column-reverse · image full-width 280px tall · text centered

---

#### SECTION 5: Values (`#valeurs`)

- `.section` padding
- **Header row:** flex space-between, align flex-end
  - Eyebrow: "Nos valeurs"
  - H2: "Ce en quoi nous croyons *vraiment*" · max-width 520px
- **Grid (`.values-grid`):** 4 columns · gap: 2px · margin-top: 72px
- **Each `.value-card`:**
  - Padding: 44px 36px 40px · border: 1px solid rgba(0,0,0,0.07) · bg: #fff
  - Hover: box-shadow 0 12px 48px rgba(0,0,0,0.07) · translateY(-5px) · z-index: 1
  - `.value-card-num` (absolute top-right, Playfair 88px, opacity 0.05): 01, 02, 03, 04
  - `.value-name` (10px, all-caps, #aaa, mb 18px): Constance / L'humain d'abord / Innovation / Communauté
  - `.value-title` (Playfair 20px, italic em): "Des standards *inébranlables*" / "Valoriser les *talents*" / "Croissance *adaptative*" / "Ancrage *local*"
  - `.value-desc` (14px, 1.78 line-height, #666, weight 300): descriptive text for each

| # | Name | Title | Description |
|---|------|-------|-------------|
| 01 | Constance | Des standards *inébranlables* | Nous veillons à ce que chaque assiette respecte les plus hauts standards de la marque dans l'ensemble de nos établissements. |
| 02 | L'humain d'abord | Valoriser les *talents* | Nous investissons dans nos équipes pour favoriser la croissance, le leadership et le succès à long terme. |
| 03 | Innovation | Croissance *adaptative* | Nous tirons parti des technologies modernes de gestion et des opérations lean pour rester à l'avant-garde des tendances. |
| 04 | Communauté | Ancrage *local* | Engagés à contribuer positivement aux quartiers où nos franchises s'implantent et à créer de la valeur durable. |

---

#### SECTION 6: Franchises (`#franchises`)

- `.section` · `padding-top: 0` (override)
- **Header:**
  - Eyebrow: "Nos franchises"
  - Flex row space-between: H2 "Deux *identités*, une même exigence" (max-width 520px) + right-aligned tagline (14px, #888, max-width 320px, text-align right)
- **Grid (`.franchise-grid`):** `1fr 1fr` · gap: 14px · margin-top: 64px
- **Each `.franchise-card`:**
  - Image: 100% wide · 520px tall · object-fit: cover · hover: scale(1.04) over 0.8s
  - Thaïzone: `brand_assets/thaizone logo vrai.png` with `object-fit: contain; background: #fff; padding: 60px 80px`
  - Yuzu Sushi: `brand_assets/yuzu suhi logo.png` with `object-fit: contain; background: #fff`
  - `.franchise-overlay` (absolute inset, flex column justify flex-end, padding 44px):
    - Gradient: `linear-gradient(to top, rgba(0,0,0,0.72) 0%, rgba(0,0,0,0.1) 50%, transparent 100%)`
    - `.franchise-brand` (Playfair 36px, white): Thaïzone / Yuzu Sushi
    - `.franchise-tagline` (14px, weight 300, rgba(255,255,255,0.62), max-width 320px, mb 24px)
    - `.franchise-link` (11px, all-caps, animated line): hidden by default (opacity 0, translateY 8px) → visible on card hover

| Franchise | Tagline | Link |
|-----------|---------|------|
| Thaïzone | Une cuisine thaïlandaise urbaine, audacieuse, fraîche et rapide. | /nos-franchises/thaizone/ |
| Yuzu Sushi | Des sushis premium raffinés, créatifs et de haute qualité. | /nos-franchises/yuzu-sushi/ |

---

#### SECTION 7: Community Engagement (`#engagement`)

- `.section` padding
- **Header (mb 64px):**
  - Eyebrow: "Engagement communautaire"
  - H2: "Des franchises qui *s'impliquent*" · max-width 580px
- **Portfolio grid (`.portfolio-grid`):** asymmetric `1.35fr 1fr` · 2 template rows · gap 14px
- **Tall item (`.item-tall`, grid-row 1/3):** min-height 560px
  - Image: `https://placehold.co/680x680/1e1814/2e2420`
  - Category: "Québec · Communauté"
  - Title: "Programme *Jeunesse*"
  - Sub: "Formation & insertion professionnelle"
- **Short item 1:** min-height 270px
  - Image: `https://placehold.co/500x320/141820/1e2030`
  - Category: "Montréal"
  - Title: "Partenariats *locaux*"
  - Sub: "Fournisseurs du quartier & circuits courts"
- **Short item 2:** min-height 270px
  - Image: `https://placehold.co/500x320/181e14/222a1e`
  - Category: "Laval"
  - Title: "Initiative *durable*"
  - Sub: "Réduction des déchets alimentaires · −30%"
- **Each `.port-item`:** image hover scale(1.04) over 0.7s · overlay gradient (black 60% → transparent)
- **Port overlay:** padding 28px 32px · category (10px, letter-spacing 0.18em, rgba(255,255,255,0.6)) · title (Playfair 22px) · sub (12.5px, rgba(255,255,255,0.55))
- **CTA below grid** (centered, mt 52px): "En savoir plus sur notre démarche" · 12px · uppercase · border-bottom 1px solid rgba(0,0,0,0.3)

---

#### SECTION 8: Footer (`#footer`)

- `background: #fff` · padding: 72px 64px 40px · border-top: 1px solid rgba(0,0,0,0.07)
- **Top row** (flex space-between, mb 64px, gap 48px):
  - Logo: `brand_assets/MKG Logo.png` · height: 56px · filter: brightness(0)
  - **Footer cols** (flex, gap 72px):
    - Col "Nos franchises": Nos Franchises · Thaïzone · Yuzu Sushi
    - Col "Entreprise": À propos · Nos valeurs · Engagement · Carrières
  - **Social** col:
    - Title: "Nous suivre"
    - Instagram button (38×38px, border 1px rgba(0,0,0,0.14), inline SVG icon)
    - LinkedIn button (same dimensions)
    - Hover: background #111, border-color #111, icon stroke #fff
- **Bottom bar** (border-top 1px rgba(0,0,0,0.07), pt 28px, flex space-between):
  - Left: "© 2025 MKG Gestion. Tous droits réservés." · 13px · #aaa · weight 300
  - Right: "Mentions légales" · "Politique de confidentialité" · 13px · #aaa · gap 32px

---

### 5.2 Careers Page (`/carrieres/index.html`)

**Page title:** `Carrières — MKG Gestion | Rejoignez notre équipe au Québec`
**Meta description:** "Rejoignez MKG Gestion, groupe gestionnaire de 10+ restaurants Thaïzone et Yuzu Sushi au Québec. Découvrez nos offres d'emploi et faites évoluer votre carrière."
**JSON-LD:** 4 `JobPosting` schemas (Gestionnaire, Cuisinier, Conseiller Sushi, Équipier)

#### NAV (always solid, no transparent state)
- background: rgba(255,255,255,0.97) always · padding: 18px 64px · box-shadow 0 1px 0 rgba(0,0,0,0.07)
- Logo height: 56px (not 160px like homepage)
- Logo filter: brightness(0) always
- Nav items: Accueil (/) · Nos Franchises (dropdown) · Carrières (active, pointer-events none) · Postuler → #offres (CTA)
- `.active` link: opacity 0.4 · pointer-events: none · aria-current="page"
- On scroll > 60px: adds `.compact` class → padding: 12px 64px

#### SECTION 1: Hero (`#hero`)
- White background · padding-top: 148px · padding-bottom: 96px
- **Header block** (mb 72px):
  - Eyebrow: "Carrières · MKG Gestion"
  - H1 (mt 20px): "Propulsez votre talent avec MKG *Gestion*."
- **2-column grid** (55fr 45fr, gap 80px, align-items center):
  - Left (`.hero-text`): two paragraphs (17px, #444, weight 300) + CTA link "Voir les offres d'emploi" → #offres
  - Right (`.hero-img-wrap`): `brand_assets/carriere section 1 image.avif` · height: 580px · object-fit: cover + gradient overlay

**Hero text content:**
- Para 1: "Rejoindre MKG Gestion, c'est intégrer un groupe stable et en pleine croissance qui opère plus de 10 établissements Thaïzone et Yuzu Sushi à travers le Québec. Nous croyons que la réussite d'un restaurant repose avant tout sur ses équipes."
- Para 2: "Ici, l'excellence opérationnelle et le développement humain ne s'opposent pas — ils se renforcent. Chaque membre est une pièce essentielle d'une chaîne qui nourrit des milliers de clients chaque jour, avec passion et constance."

#### SECTION 2: FAQ (`#faq`)
- border-top: 1px solid rgba(0,0,0,0.07)
- **Header** (2-col grid 1fr 1fr, gap 80px, mb 72px):
  - Left: Eyebrow "FAQ" · H2: "Ce qui fait la différence *chez nous*."
  - Right (pt 52px): intro paragraph
- **FAQ list:** border-top + items with border-bottom
- **Each `.faq-item`:**
  - Trigger button: flex space-between · 26px padding-top/bottom · 16px font · letter-spacing -0.01em
  - Icon: 22×22px circle border rgba(0,0,0,0.18) containing + SVG
  - When open: icon background #111, icon SVG rotates 45°, answer expands via max-height transition (0 → 260px)
  - Accordion behavior: only one open at a time

**FAQ content:**
1. "Quels sont les avantages sociaux offerts ?" → horaires flexibles, repas en service, programme de reconnaissance, rabais
2. "Offrez-vous des possibilités d'avancement ?" → promotion interne, gestionnaires anciennement équipiers
3. "Est-ce que les horaires sont flexibles pour les étudiants ?" → oui, équilibre travail-études encouragé
4. "Quelle formation est prévue à l'embauche ?" → 2 semaines de formation structurée avec mentor dédié

#### SECTION 3: Job Offers (`#offres`)
- background: #f9f9f8 · border-top: 1px solid rgba(0,0,0,0.07)
- **Header:** Eyebrow "Offres d'emploi" · H2: "Joins-toi à *l'équipe*." + right-aligned tagline
- **Grid (`.offres-grid`):** 4 columns · gap 20px · mt 56px
- **Each `.offre-card`:**
  - White bg · border 1px rgba(0,0,0,0.07) · no border-radius
  - Hover: box-shadow 0 16px 48px rgba(0,0,0,0.09) · translateY(-4px)
  - Image: 560×360 placeholder · height 220px · object-fit cover · hover scale(1.05) 0.8s · gradient overlay
  - Body (padding 24px 24px 28px): `.offre-tag` (9.5px, #aaa, letter-spacing 0.2em) · `.offre-title` (Playfair 20px) · `.offre-desc` (13.5px, #666, weight 300) · `.offre-btn` (bordered, hover fills black)

| Tag | Title | Description | Image Color |
|-----|-------|-------------|-------------|
| Gestion | Gestionnaire de restaurant | Dirigez une équipe dynamique et assurez l'excellence opérationnelle au quotidien. | `#1a1814/2e2420` |
| Cuisine | Cuisinier / Cuisinière | Exprimez votre passion culinaire dans un environnement structuré et stimulant. | `#141820/1e2030` |
| Yuzu Sushi | Conseiller·ère Sushi | Maîtrisez l'art du sushi et offrez une expérience client haut de gamme. | `#1e1814/2c2418` |
| Équipe | Équipier·ère | Intégrez une équipe soudée et développez vos compétences en restauration. | `#0e1218/181e28` |

#### SECTION 4: Values Split (`#valeurs`) — Full-bleed
- **2-column grid** (1fr 1fr), no padding wrapper
- **Left panel (`.valeurs-left`):** white · padding: 96px 80px · border-top 1px rgba(0,0,0,0.07)
  - Header: Eyebrow + H2 "Les valeurs qui guident nos équipes *au quotidien*." (max-width 380px)
  - Each `.valeur-row` (flex, gap 24px, padding 28px 0, border-bottom):
    - `.valeur-num`: Playfair 12px, #ccc
    - `.valeur-name`: Playfair 18px, italic, mb 7px
    - `.valeur-desc`: 14px, #666, weight 300

| # | Name | Description |
|---|------|-------------|
| 01 | Excellence | Chaque geste compte. Nous visons les plus hauts standards dans chacun de nos établissements, chaque jour. |
| 02 | Collaboration | La force du groupe repose sur des équipes solidaires qui avancent ensemble vers un objectif commun. |
| 03 | Plaisir | Travailler chez nous, c'est aussi sourire. La bonne humeur est un ingrédient essentiel de notre recette. |
| 04 | Intégrité | Nous agissons avec honnêteté et transparence envers nos équipes, nos clients et nos communautés. |

- **Right panel (`.valeurs-right`):** background #0f1523 · padding 40px · 2×2 grid · row heights 280px each · gap 10px
  - 4 photo cards, each 280px tall, image fills, hover scale(1.06), gradient overlay
  - Placeholder images: 400×300px in dark blue shades (#1a2035, #141a2c, #0e1420, #121826)

---

### 5.3 Franchise Directory Pages

Both pages share identical structure — only brand colors, copy, and restaurant data differ.

#### Structure (both Thaïzone + Yuzu Sushi pages)

```
Nav (always solid, same as careers)
→ Hero banner (28vh short, dark bg)
→ Search bar (sticky, location + postal code filters)
→ Restaurant list (accordion-style entries)
→ Footer (same as homepage)
```

**Page-specific data:**

| Property | Thaïzone | Yuzu Sushi |
|----------|----------|------------|
| Title | Thaïzone — Restaurants au Québec \| MKG Gestion | Yuzu Sushi — Restaurants au Québec \| MKG Gestion |
| Accent color | `#E91E8C` (magenta) | `#D4A547` (gold) |
| Cuisine | Thaïlandaise | Japonaise, Sushi |
| # Restaurants | 8 locations | 8 locations |
| Hours | 11:00–22:00 daily | 11:30–21:30 Mon–Thu · 11:30–22:00 Fri–Sat · 12:00–21:00 Sun |

**Thaïzone locations:**
1. Plateau-Mont-Royal — 4521 Rue Saint-Denis, Montréal H2J 2L5
2. Centre-ville — 1260 Rue Sainte-Catherine O., Montréal H3G 1P2
3. Laval Centropolis — 3035 Le Carrefour Blvd, Laval H7T 1C8
4. Longueuil — 825 Rue Saint-Laurent O., Longueuil J4K 2V2
5. Brossard Quartier DIX30 — 9160 Blvd Leduc, Brossard J4Y 0H3
6. Boucherville — 500 Rue de la Rivière-aux-Pins, Boucherville J4B 5E4
7. Saint-Hubert — (see source file)
8. + additional locations

**Yuzu Sushi locations:**
1. Vieux-Montréal — 360 Rue Saint-François-Xavier, Montréal H2Y 2S8
2. Mont-Royal — 1075 Ave du Mont-Royal E., Montréal H2J 1X7
3. Laval Méga Centre — 4650 Autoroute 440 O., Laval H7P 5V5
4. Longueuil Promenades — 1111 Blvd Taschereau, Longueuil J4K 1A1
5. Brossard DIX30 — 9255 Blvd Leduc, Brossard J4Y 0M8
6. + additional locations

---

## 6. JavaScript Behaviors

### 6.1 Navigation Scroll State
```javascript
const nav = document.getElementById('main-nav');
window.addEventListener('scroll', () => {
  nav.classList.toggle('solid', window.scrollY > 60);
}, { passive: true });
```

### 6.2 Franchise Dropdown
```javascript
(function() {
  const item = document.getElementById('nav-franchises-item');
  const btn  = document.getElementById('nav-franchises-btn');
  const menu = document.getElementById('nav-franchises-menu');
  function open()  { btn.setAttribute('aria-expanded','true');  menu.classList.add('open'); }
  function close() { btn.setAttribute('aria-expanded','false'); menu.classList.remove('open'); }
  btn.addEventListener('click', e => { e.stopPropagation(); btn.getAttribute('aria-expanded')==='true' ? close() : open(); });
  item.addEventListener('mouseenter', open);
  item.addEventListener('mouseleave', close);
  item.addEventListener('keydown', e => { if (e.key === 'Escape') { close(); btn.focus(); } });
  document.addEventListener('click', e => { if (!item.contains(e.target)) close(); });
})();
```

### 6.3 Hero Parallax
```javascript
const heroBg = document.getElementById('hero-bg');
window.addEventListener('scroll', () => {
  heroBg.style.transform = `translateY(${window.scrollY * 0.28}px)`;
}, { passive: true });
```

### 6.4 Scroll Fade-In
```javascript
const io = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.1, rootMargin: '0px 0px -44px 0px' });
document.querySelectorAll('.fade-up').forEach(el => io.observe(el));

window.addEventListener('load', () => {
  document.querySelectorAll('#hero .fade-up').forEach(el => {
    setTimeout(() => el.classList.add('visible'), 100);
  });
});
```

### 6.5 FAQ Accordion (Careers only)
```javascript
document.querySelectorAll('.faq-trigger').forEach(btn => {
  btn.addEventListener('click', () => {
    const isOpen = btn.classList.contains('open');
    // Close all
    document.querySelectorAll('.faq-trigger').forEach(b => {
      b.classList.remove('open');
      b.setAttribute('aria-expanded', 'false');
      b.nextElementSibling.classList.remove('open');
    });
    // Open clicked if it wasn't open
    if (!isOpen) {
      btn.classList.add('open');
      btn.setAttribute('aria-expanded', 'true');
      btn.nextElementSibling.classList.add('open');
    }
  });
});
```

---

## 7. Brand Assets Inventory

| File | Size | Format | Usage |
|------|------|--------|-------|
| `MKG Logo.png` | 2.0 MB | PNG | Nav logo (homepage: 160px h), footer logo (56px h, filter brightness(0)) |
| `thaizone logo vrai.png` | 14 KB | PNG | Thaïzone franchise card (object-fit contain, white bg, padding 60px 80px) |
| `yuzu suhi logo.png` | 8.1 KB | PNG | Yuzu Sushi franchise card (object-fit contain, white bg) |
| `max image.jpg` | 104 KB | JPG | Quote section founder portrait (420×480px, object-position center top) |
| `carriere section 1 image.avif` | 81 KB | AVIF | Careers hero right column (height 580px, object-fit cover) |
| `quote section.png` | 1.1 MB | PNG | Reference image (not used in code) |
| `spherical & co layout.png` | 4.9 MB | PNG | Layout reference (not used in code) |

**Logo usage rules:**
- On dark background (transparent nav, hero): `filter: brightness(0) invert(1)` (renders white)
- On white background (solid nav, footer): `filter: brightness(0)` (renders black)

---

## 8. Tooling Setup

### serve.mjs
- Basic Node.js HTTP server on port 3000
- Serves all files from project root
- Handles MIME types: html, css, js, png, jpg, avif, mp4, svg, mjs, json

```bash
node serve.mjs
# Server running at http://localhost:3000
```

### screenshot.mjs
- Puppeteer 22.0.0 · viewport 1440×900 · deviceScaleFactor 1.5
- Full-page capture · saves to `temporary screenshots/screenshot-N.png`
- Optional label suffix: `node screenshot.mjs http://localhost:3000 my-label`

```bash
node screenshot.mjs http://localhost:3000
# Saves: temporary screenshots/screenshot-1.png
```

### package.json
```json
{
  "dependencies": {
    "puppeteer": "22.0.0"
  }
}
```

---

## 9. Reproduction Checklist

### Step 1: Setup
- [ ] Create root directory with file structure from Section 2
- [ ] Copy all brand assets to `brand_assets/`
- [ ] Copy `serve.mjs`, `screenshot.mjs`, `screenshot-section.mjs`
- [ ] Run `npm install` (installs puppeteer)

### Step 2: Global Styles (for every page)
- [ ] Add Tailwind CDN script tag
- [ ] Add Google Fonts link (Playfair Display + DM Sans)
- [ ] Add global CSS reset and body styles
- [ ] Add `.fade-up` animation system (including .d1–.d4 delays)
- [ ] Add `.eyebrow`, `.section`, `.section-inner` utilities
- [ ] Add responsive breakpoints (@900px, @768px, @560px)

### Step 3: Homepage
- [ ] Build navigation with dropdown (transparent → solid scroll state)
- [ ] Build hero section with 4 layers + parallax
- [ ] Build mission section (2-col grid + 3 stats)
- [ ] Build quote section (dark full-bleed, founder image with gradient blends)
- [ ] Build values section (4-card grid, 2px gap)
- [ ] Build franchises section (2-col, 520px tall cards)
- [ ] Build engagement/portfolio section (asymmetric 1.35fr/1fr grid)
- [ ] Build footer (3-col top, bottom bar)
- [ ] Add all JavaScript behaviors

### Step 4: Careers Page
- [ ] Replicate solid-always nav (logo height 56px)
- [ ] Build white hero (padding-top 148px, 2-col grid)
- [ ] Build FAQ accordion section
- [ ] Build job offers grid (4-col, #f9f9f8 background)
- [ ] Build values full-bleed split (left white, right #0f1523)
- [ ] Replicate footer
- [ ] Add careers-specific JS (compact nav, FAQ accordion)

### Step 5: Franchise Pages (×2)
- [ ] Replicate solid nav for Thaïzone (logo 56px, brand color #E91E8C)
- [ ] Replicate solid nav for Yuzu Sushi (logo 56px, brand color #D4A547)
- [ ] Build short hero banner (28vh)
- [ ] Build sticky search bar with location/postal filters
- [ ] Build restaurant directory list
- [ ] Add JSON-LD structured data for all restaurant locations
- [ ] Replicate footer

### Step 6: QA
- [ ] Start dev server: `node serve.mjs`
- [ ] Screenshot homepage: `node screenshot.mjs http://localhost:3000`
- [ ] Screenshot careers: `node screenshot.mjs http://localhost:3000/carrieres/`
- [ ] Screenshot Thaïzone: `node screenshot.mjs http://localhost:3000/nos-franchises/thaizone/`
- [ ] Screenshot Yuzu Sushi: `node screenshot.mjs http://localhost:3000/nos-franchises/yuzu-sushi/`
- [ ] Verify: Nav scroll behavior works on homepage
- [ ] Verify: Dropdown opens on hover + click, closes on outside click + Escape
- [ ] Verify: All .fade-up elements animate in on scroll
- [ ] Verify: Hero parallax (hero-bg moves at 28% scroll rate)
- [ ] Verify: Franchise card images scale on hover
- [ ] Verify: FAQ accordion works (one item open at a time)
- [ ] Verify: Mobile layout at 375px and 768px breakpoints

---

## 10. SEO & Metadata

### Homepage
```html
<title>MKG Gestion — Restauration · Franchise · Québec</title>
<html lang="fr">
```

### Careers
```html
<title>Carrières — MKG Gestion | Rejoignez notre équipe au Québec</title>
<meta name="description" content="Rejoignez MKG Gestion, groupe gestionnaire de 10+ restaurants Thaïzone et Yuzu Sushi au Québec.">
```
+ 4 `JobPosting` JSON-LD schemas

### Franchise Pages
```html
<!-- Thaïzone -->
<title>Thaïzone — Restaurants au Québec | MKG Gestion</title>
<link rel="canonical" href="https://mkggestion.com/nos-franchises/thaizone/">
<meta property="og:title" content="Thaïzone — Restaurants au Québec | MKG Gestion">

<!-- Yuzu Sushi -->
<title>Yuzu Sushi — Restaurants au Québec | MKG Gestion</title>
<link rel="canonical" href="https://mkggestion.com/nos-franchises/yuzu-sushi/">
```
+ `Restaurant` JSON-LD schemas for each location (8 per franchise)

---

*Document generated from source files — last updated 2026-03-04*
