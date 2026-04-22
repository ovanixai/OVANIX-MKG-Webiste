# SEO Audit Report
**Generated:** 2026-04-21
**Project:** MKG Gestion Website
**Pages audited:** 7

---

## Overview

| Page | Status | Critical | Warnings | Info |
|------|--------|----------|----------|------|
| `/` (Homepage) | Needs Work | 0 | 5 | 3 |
| `/realisations/` | Needs Work | 0 | 3 | 2 |
| `/nos-franchises/thaizone/` | **Failing** | 2 | 4 | 0 |
| `/nos-franchises/yuzu-sushi/` | **Failing** | 2 | 4 | 0 |
| `/promotions/` | **Failing** | 1 | 3 | 0 |
| `/notre-equipe/` | Needs Work | 0 | 4 | 1 |
| `/carrieres/` | Needs Work | 0 | 4 | 1 |

**Project-level:** No `robots.txt` `[Warning]` · No `sitemap.xml` `[Warning]`

---

## Cross-Page Issues

### Duplicate Titles
None — all titles are unique.

### Duplicate Meta Descriptions
None — all descriptions are unique.

### Conflicting Canonicals
- `/nos-franchises/thaizone/` and `/nos-franchises/yuzu-sushi/` have canonicals pointing to the old dev domain `ovanix-mkg-webiste.vercel.app` instead of the production domain.
- 5 pages have no canonical at all: `/`, `/realisations/`, `/promotions/`, `/notre-equipe/`, `/carrieres/`.

### Broken hreflang Pairs
No hreflang declared on any page. The site is currently French-only (no EN counterparts), so there are no broken reciprocal pairs. However, adding `hreflang="fr-CA"` self-references and an `x-default` on all pages is recommended.

---

## Per-Page Findings

---

### `/index.html` — Homepage
**Status:** Needs Work
**Inferred keyword:** gestion de franchises restauration Québec

| Severity | Area | Issue | Recommendation |
|----------|------|-------|----------------|
| `[Warning]` | Canonical | No `<link rel="canonical">` | Add self-referencing canonical to production URL |
| `[Warning]` | hreflang | No `hreflang` or `x-default` declared | Add `hreflang="fr-CA"` self-ref + `x-default` |
| `[Warning]` | Meta description | 118 chars — just under ideal minimum of 120 | Expand to ~135–150 chars (see proposed rewrite) |
| `[Warning]` | Performance | `<script src="cdn.tailwindcss.com">` in `<head>` without `defer` — render-blocking | Move below fold or add `defer` |
| `[Warning]` | Performance | Google Fonts `<link rel="stylesheet">` is render-blocking | Use `media="print" onload` swap or preload pattern |
| `[Info]` | Schema | No structured data | Add `LocalBusiness` JSON-LD for Gestion MKG |
| `[Info]` | Semantic | No `<main>` landmark element | Wrap page body content in `<main>` |
| `[Info]` | Internal links | Social buttons use `href="#"` | Replace with real Instagram/LinkedIn URLs when available |

**Proposed rewrites:**
```
CURRENT title:       "Gestion MKG — Restauration · Franchise · Québec"
PROPOSED title:      keep as-is — 47 chars, unique, keyword-rich ✓

CURRENT description: "Leader québécois en gestion de franchises de restauration (Thaïzone, Yuzu Sushi). Excellence et innovation culinaire."
                     (118 chars — just under ideal minimum)

PROPOSED description: "Gestion MKG est le leader québécois en gestion de franchises de restauration. Thaïzone et Yuzu Sushi — excellence opérationnelle et humaine au Québec."
                      (151 chars ✓)
```

---

### `/realisations/` — Réalisations
**Status:** Needs Work
**Inferred keyword:** réalisations communautaires Gestion MKG Québec

| Severity | Area | Issue | Recommendation |
|----------|------|-------|----------------|
| `[Warning]` | Canonical | No `<link rel="canonical">` | Add self-referencing canonical |
| `[Warning]` | hreflang | No `hreflang` / `x-default` | Add `hreflang="fr-CA"` self-ref + `x-default` |
| `[Warning]` | Performance | Tailwind CDN in `<head>` without `defer` | Defer or move |
| `[Info]` | Schema | No structured data | Add `WebPage` JSON-LD |
| `[Info]` | Semantic | No `<main>` element | Wrap content in `<main>` |

**Proposed rewrites:**
```
CURRENT title:       "Réalisations — Gestion MKG · Nos contributions à la communauté"
PROPOSED title:      keep as-is — 62 chars, descriptive ✓

CURRENT description: "Découvrez les réalisations et contributions communautaires de Gestion MKG — des actions concrètes qui font une différence au Québec."
PROPOSED description: keep as-is — 133 chars, well within range ✓
```

---

### `/nos-franchises/thaizone/` — Thaïzone
**Status:** Failing
**Inferred keyword:** restaurant Thaïzone Québec

| Severity | Area | Issue | Recommendation |
|----------|------|-------|----------------|
| `[Critical]` | Schema | JSON-LD lists 8 fictional Thaïzone locations (Plateau-Mont-Royal, Centre-ville, Laval, Longueuil, Brossard, Boucherville, St-Hubert, Repentigny) that do NOT match the 3 actual MKG-managed restaurants shown on the page (Charlesbourg, Rimouski, Beauport Nord) | Replace schema with the 3 real restaurant entries with correct addresses and phone numbers from the listing |
| `[Critical]` | Schema | Phone numbers are placeholders (`+15145550101`, `+15145550102`…) — none match the real phones visible on the page | Replace with real phones: (418) 626-9503, (581) 824-1515, (418) 660-8424 |
| `[Warning]` | Canonical | Points to `https://ovanix-mkg-webiste.vercel.app/nos-franchises/thaizone/` — old dev domain | Update to production domain |
| `[Warning]` | hreflang | No `hreflang` / `x-default` | Add `hreflang="fr-CA"` self-ref + `x-default` |
| `[Warning]` | Meta description | 174 chars — over ideal max of 158 | Trim (see proposed rewrite) |
| `[Warning]` | Performance | Tailwind CDN in `<head>` without `defer` | Defer or move |

**Proposed rewrites:**
```
CURRENT title:       "Thaïzone — Restaurants au Québec | Gestion MKG"
PROPOSED title:      keep as-is — 47 chars, keyword-targeted ✓

CURRENT description: "Trouvez le restaurant Thaïzone le plus proche de chez vous au Québec. Cuisine thaïlandaise fraîche, rapide et audacieuse. 8 succursales à Montréal, Laval, Longueuil et plus."
                     (174 chars — too long, and "8 succursales à Montréal" is inaccurate for MKG's actual footprint)

PROPOSED description: "Trouvez votre restaurant Thaïzone au Québec. Cuisine thaïlandaise fraîche, rapide et audacieuse, gérée avec excellence par Gestion MKG."
                      (136 chars ✓)
```

---

### `/nos-franchises/yuzu-sushi/` — Yuzu Sushi
**Status:** Failing
**Inferred keyword:** restaurant Yuzu Sushi Québec

| Severity | Area | Issue | Recommendation |
|----------|------|-------|----------------|
| `[Critical]` | Schema | JSON-LD lists 8 fictional Yuzu Sushi locations (Vieux-Montréal, Mont-Royal, Laval, Longueuil, Brossard, Terrebonne, Mascouche, Saint-Jérôme) that do NOT match the 7 actual restaurants shown on the page (Limoilou, Legendre, Haute-Ville, Rimouski, Deschênes, Jessop, Sirois) | Replace schema with the 7 real restaurant entries with correct addresses and phone numbers |
| `[Critical]` | Schema | Phone numbers are placeholders (`+15145550201`…) — none match real phones on the page | Replace with real phones: (418) 780-7230, (418) 877-5666, (418) 614-6010, (418) 730-6686, (418) 524-9890, (418) 723-1982, (418) 724-2244 |
| `[Warning]` | Canonical | Points to `https://ovanix-mkg-webiste.vercel.app/nos-franchises/yuzu-sushi/` — old dev domain | Update to production domain |
| `[Warning]` | hreflang | No `hreflang` / `x-default` | Add `hreflang="fr-CA"` self-ref + `x-default` |
| `[Warning]` | Meta description | 162 chars — over ideal max of 158 | Trim (see proposed rewrite) |
| `[Warning]` | Performance | Tailwind CDN in `<head>` without `defer` | Defer or move |

**Proposed rewrites:**
```
CURRENT title:       "Yuzu Sushi — Restaurants au Québec | Gestion MKG"
PROPOSED title:      keep as-is — 49 chars, keyword-targeted ✓

CURRENT description: "Trouvez le restaurant Yuzu Sushi le plus proche de chez vous au Québec. Sushis premium raffinés et créatifs. 8 succursales à Montréal, Laval, Longueuil et plus."
                     (162 chars — too long, and "8 succursales à Montréal" is inaccurate)

PROPOSED description: "Trouvez votre restaurant Yuzu Sushi au Québec. Sushis premium raffinés et créatifs, gérés avec excellence par Gestion MKG."
                      (123 chars ✓)
```

---

### `/promotions/` — Promotions
**Status:** Failing
**Inferred keyword:** N/A — page is currently disabled

| Severity | Area | Issue | Recommendation |
|----------|------|-------|----------------|
| `[Critical]` | Redirect | Uses `<meta http-equiv="refresh" content="0; url=/">` — a client-side soft redirect. Google may partially crawl and index this page before the redirect fires, splitting link signals | If permanently disabled: configure a server-side `301` redirect in `vercel.json` instead and remove the page from the sitemap. If temporary: add `<meta name="robots" content="noindex">` alongside the meta refresh |
| `[Warning]` | Canonical | No canonical — moot while redirect is active | Resolve redirect strategy first |
| `[Warning]` | hreflang | None | Resolve redirect strategy first |
| `[Warning]` | Meta description | 166 chars — over ideal | Fix only if page is re-enabled |

**Proposed rewrites:** N/A — resolve redirect strategy first.

---

### `/notre-equipe/` — Notre Équipe
**Status:** Needs Work
**Inferred keyword:** équipe direction Gestion MKG

| Severity | Area | Issue | Recommendation |
|----------|------|-------|----------------|
| `[Warning]` | Canonical | No `<link rel="canonical">` | Add self-referencing canonical |
| `[Warning]` | hreflang | No `hreflang` / `x-default` | Add `hreflang="fr-CA"` self-ref + `x-default` |
| `[Warning]` | Meta description | 163 chars — over ideal max of 158 | Trim (see proposed rewrite) |
| `[Warning]` | Performance | Tailwind CDN in `<head>` without `defer` | Defer or move |
| `[Info]` | Semantic | No `<main>` element | Wrap page content in `<main>` |

**Proposed rewrites:**
```
CURRENT title:       "Notre Équipe — Gestion MKG · Leadership & Direction Québec"
PROPOSED title:      keep as-is — 59 chars ✓

CURRENT description: "Découvrez l'équipe de direction et d'administration de Gestion MKG — les experts opérationnels et leaders passionnés qui font rayonner nos restaurants au Québec."
                     (163 chars — 5 chars over)

PROPOSED description: "Rencontrez l'équipe de direction de Gestion MKG — les leaders passionnés qui font rayonner nos restaurants Thaïzone et Yuzu Sushi au Québec."
                      (141 chars ✓)
```

---

### `/carrieres/` — Carrières
**Status:** Needs Work
**Inferred keyword:** emploi restauration Québec Gestion MKG

| Severity | Area | Issue | Recommendation |
|----------|------|-------|----------------|
| `[Warning]` | Canonical | No `<link rel="canonical">` | Add self-referencing canonical |
| `[Warning]` | hreflang | No `hreflang` / `x-default` | Add `hreflang="fr-CA"` self-ref + `x-default` |
| `[Warning]` | Meta description | 161 chars — over ideal max of 158 | Trim (see proposed rewrite) |
| `[Warning]` | Performance | Tailwind CDN in `<head>` without `defer` | Defer or move |
| `[Info]` | Semantic | No `<main>` element | Wrap page content in `<main>` |

**Proposed rewrites:**
```
CURRENT title:       "Carrières — Gestion MKG · Rejoignez notre équipe au Québec"
PROPOSED title:      keep as-is — 59 chars ✓

CURRENT description: "Rejoignez Gestion MKG, groupe gestionnaire de 10+ restaurants Thaïzone et Yuzu Sushi au Québec. Découvrez nos offres d'emploi et faites évoluer votre carrière."
                     (161 chars — 3 chars over)

PROPOSED description: "Rejoignez Gestion MKG en restauration au Québec. 10+ établissements Thaïzone et Yuzu Sushi — découvrez nos offres d'emploi et évoluez avec nous."
                      (145 chars ✓)
```

---

## Technical SEO

| Check | Status | Notes |
|-------|--------|-------|
| `robots.txt` | **Missing** | Needs to be created at project root |
| `sitemap.xml` | **Missing** | Needs to be created at project root |
| Render-blocking scripts | **Found — all 7 pages** | `<script src="cdn.tailwindcss.com">` in `<head>` without `defer` or `async` |
| Render-blocking CSS | **Found — all 7 pages** | Google Fonts `<link rel="stylesheet">` loaded synchronously |
| Images missing `width`/`height` | **Minimal** | Most images have explicit dimensions; a few minor gaps in decorative elements |
| Canonical domain consistency | **Issue** | OG URLs, Twitter URLs, and existing canonicals reference `ovanix-mkg-webiste.vercel.app` — should be updated to the live production domain once confirmed |

---

## Quick Wins

> The fixes with the biggest SEO impact with the least effort. Do these first.

1. **Fix the Thaïzone + Yuzu Sushi JSON-LD schema** — The structured data currently describes fictional restaurants in the wrong cities with fake phone numbers. Google uses this for rich results; wrong data actively hurts trust. Replace with the 3 real Thaïzone and 7 real Yuzu Sushi locations already visible on each page → affects 2 pages, **Critical**

2. **Add canonical tags to all 5 pages missing them** — Without canonicals, Google has to guess the preferred URL. A one-line addition per page is enough → affects 5 pages, `[Warning]`

3. **Replace the `/promotions/` meta refresh with a `vercel.json` 301 redirect** — Soft redirects can split crawl signals and cause the page to be partially indexed. A `vercel.json` rule is 3 lines and permanent → affects 1 page, **Critical**

4. **Create `robots.txt` and `sitemap.xml`** — Both are missing entirely. A basic `robots.txt` (allow all) and a manually maintained `sitemap.xml` listing the 6 live pages takes ~20 minutes and is a foundational SEO requirement → affects all pages, `[Warning]`

5. **Add `defer` to the Tailwind CDN script** — `<script src="..." defer>` is a one-word change per page that removes a render-blocking resource from the critical path, improving Core Web Vitals (LCP/FID) → affects all 7 pages, `[Warning]`

---

## Severity Reference

| Level | Meaning |
|-------|---------|
| `[Critical]` | Directly hurts rankings or creates inaccurate data. Fix immediately. |
| `[Warning]` | Suboptimal — reduces SEO effectiveness. Fix soon. |
| `[Info]` | Best-practice gaps with minor impact. Fix when convenient. |
