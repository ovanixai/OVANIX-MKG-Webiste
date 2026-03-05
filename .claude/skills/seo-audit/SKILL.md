---
name: seo-audit
description: Use when someone asks to audit SEO, improve search rankings, check meta tags, fix hreflang, analyze page structure, or run an SEO report on a website.
argument-hint: [URL or file/folder path — optional, defaults to all .html files]
disable-model-invocation: true
---

## What This Skill Does

Acts as an expert backend SEO consultant for MKG Quebec-based websites (French/English bilingual). Audits HTML files or a live URL, produces a severity-rated report with per-page scores, infers target keywords for confirmation, then offers a gated fix pass.

---

## Step 1 — Detect Input

Check if an argument (``) was provided:

- **URL** (starts with `http://` or `https://`): fetch with WebFetch
- **File or folder path**: use Read (single file) or Glob `**/*.html` (directory)
- **No argument**: Glob `**/*.html` from the project root to find all HTML pages

Collect all pages into a list. Announce: "Found N pages to audit." and list them.

---

## Step 2 — Per-Page Audit

For each page, extract and evaluate:

### 2a. Meta Tags
- **Title tag**
  - Present? If missing → `[Critical]`
  - Length: ideal 50–60 chars. Under 30 or over 70 → `[Warning]`
  - Record for cross-page uniqueness check (Step 3)
- **Meta description**
  - Present? If missing → `[Critical]`
  - Length: ideal 120–158 chars. Outside range → `[Warning]`
  - Record for cross-page duplicate check (Step 3)
- **Open Graph tags** (`og:title`, `og:description`, `og:image`, `og:url`)
  - Each missing tag → `[Warning]`
- **Canonical tag** (`<link rel="canonical">`)
  - Missing → `[Warning]`
  - Self-referencing correctly? Malformed or pointing elsewhere → `[Critical]`
  - Record URL for cross-page conflict check (Step 3)
- **hreflang tags** (critical for Quebec bilingual sites)
  - French (`fr`, `fr-CA`) and English (`en`, `en-CA`) versions declared?
  - Each language version must reference the other (reciprocal pair)
  - `x-default` present?
  - Missing hreflang → `[Critical]` for bilingual pages
  - Non-reciprocal pair → `[Critical]`
  - Missing `x-default` → `[Warning]`

### 2b. Page Structure
- **H1**: exactly one H1? Zero → `[Critical]`, multiple → `[Warning]`
- **H2–H6 hierarchy**: logical nesting? Skipped levels → `[Warning]`
- **Image alt text**: each `<img>` without `alt` or with empty `alt` → `[Warning]` (list the src)
- **Semantic HTML**: checks for `<main>`, `<header>`, `<nav>`, `<footer>` — missing → `[Info]`
- **Internal links**: anchor tags with no `href` or `href="#"` → `[Info]`

### 2c. Technical SEO
- **`robots.txt`**: check if it exists in the project root → missing → `[Warning]`
- **`sitemap.xml`**: check if it exists in the project root → missing → `[Warning]`
- **Schema markup** (`<script type="application/ld+json">`): present? If not → `[Info]`
- **Performance hints**: check for render-blocking `<script>` tags in `<head>` without `defer`/`async` → `[Warning]`; unoptimized images (no `width`/`height` attributes) → `[Info]`

### 2d. Page Score
Assign a status based on findings for that page:
- **Failing** — 1 or more `[Critical]` issues
- **Needs Work** — only `[Warning]` issues, no `[Critical]`
- **Pass** — only `[Info]` issues or no issues

---

## Step 3 — Cross-Page Analysis

After all pages are processed, check for:

- **Duplicate titles**: list any title that appears on 2+ pages → `[Critical]`
- **Duplicate meta descriptions**: list any description that appears on 2+ pages → `[Critical]`
- **Conflicting canonicals**: pages that point to the same canonical URL when they shouldn't → `[Warning]`
- **Broken hreflang pairs**: if page A declares `hreflang` pointing to page B, confirm page B reciprocally declares `hreflang` pointing back to page A → `[Critical]`

---

## Step 4 — Keyword Inference

For each page that needs a title or description rewrite, infer the target keyword:

1. Extract: H1 text, H2 text (first two), visible body copy (first 200 chars of `<body>` text nodes), and URL slug
2. Propose: "Page: `/about.html` → Inferred keyword: **gestion immobilière Montréal**. Correct?"
3. **STOP and wait for user confirmation before writing any rewrites.**
4. If the user corrects a keyword, use their version. If they confirm, proceed.

Only infer keywords for pages that will need new or rewritten tags. Skip pages scoring "keep as-is" (see Step 5).

---

## Step 5 — Generate Rewrites (Only Where Needed)

For each page requiring changes:

- **If title already scores well** (correct length, unique, relevant): mark as `keep as-is — no change needed`
- **If meta description already scores well**: mark as `keep as-is — no change needed`
- Only write a proposed rewrite for tags that have actual issues
- Proposed rewrites must incorporate the confirmed keyword naturally
- Never pad or keyword-stuff — write for humans first

Show proposed rewrites in a diff-style block:

```
Page: /about.html
  CURRENT title:  "About"
  PROPOSED title: "Gestion immobilière à Montréal | MKG Gestion"

  CURRENT description: (missing)
  PROPOSED description: "MKG Gestion accompagne les propriétaires et locataires à Montréal. Découvrez nos services de gestion immobilière professionnelle."
```

---

## Step 6 — Output

### 6a. Save report to file

Write the full report to `seo-report.md` in the project root using the template in [report-template.md](report-template.md).

### 6b. Post chat summary

Output in chat:

```
## SEO Audit Complete

Pages audited: N
Failing: X | Needs Work: Y | Passing: Z

Critical issues: X
Warnings: Y
Info: Z

Top issues:
- [list top 3 most critical findings]

Full report saved to: seo-report.md
```

---

## Step 7 — Offer Fix Pass

After showing the summary, ask:

> "Want me to apply these fixes? I'll only edit pages that need changes and flag any existing tags before overwriting."

- If yes: apply fixes one file at a time using Edit. Before each file, list what will change and confirm.
- If no: stop. The report is the deliverable.

**Never modify any file without an explicit yes.**

---

## Guardrails

- Never modify files without explicit user confirmation
- Never fetch a URL that wasn't explicitly passed as an argument
- Never remove or overwrite an existing meta tag without flagging it first
- Never rewrite a title or description that already scores well — mark it `keep as-is`
- Never invent keywords — only infer from H1–H3 text, body copy, and URL slug
- Never hallucinate hreflang language codes — only use codes present in the HTML

---

## Notes

- This skill was built for MKG Quebec bilingual sites — hreflang for `fr-CA` / `en-CA` pairs is a first-class concern, not an afterthought
- If a page has no `<html lang="">` attribute, flag it as `[Warning]` — required for hreflang to work correctly
- Schema markup recommendations should match page type: use `LocalBusiness` for homepage, `WebPage` for others unless content suggests otherwise
- robots.txt and sitemap.xml checks are project-level — only check once, not per page
