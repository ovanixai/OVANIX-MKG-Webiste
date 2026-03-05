# SEO Audit Report
**Generated:** [DATE]
**Project:** [PROJECT NAME or root path]
**Pages audited:** [N]

---

## Overview

| Page | Status | Critical | Warnings | Info |
|------|--------|----------|----------|------|
| /index.html | Failing / Needs Work / Pass | 0 | 0 | 0 |

---

## Cross-Page Issues

> Issues that span multiple pages and must be resolved globally.

### Duplicate Titles
- [List pages with identical titles, or "None"]

### Duplicate Meta Descriptions
- [List pages with identical descriptions, or "None"]

### Conflicting Canonicals
- [List canonical conflicts, or "None"]

### Broken hreflang Pairs
- [List non-reciprocal hreflang declarations, or "None"]

---

## Per-Page Findings

### /[page-name].html
**Status:** Failing / Needs Work / Pass
**Inferred keyword:** [keyword]

| Severity | Area | Issue | Recommendation |
|----------|------|-------|----------------|
| [Critical] | Meta | Title missing | Add: "..." |
| [Warning] | hreflang | fr-CA declared but no reciprocal en-CA | Add hreflang on en version |
| [Info] | Structure | No schema markup | Consider adding LocalBusiness schema |

**Proposed rewrites:**
```
CURRENT title:       "..."
PROPOSED title:      "..."   ← keep as-is (scores well) / replace

CURRENT description: "..."
PROPOSED description: "..."  ← keep as-is / replace
```

---

<!-- Repeat Per-Page Findings block for each page -->

---

## Technical SEO

| Check | Status | Notes |
|-------|--------|-------|
| robots.txt | Present / Missing | |
| sitemap.xml | Present / Missing | |
| Render-blocking scripts | Found / None | List files if found |
| Images missing width/height | N found | List src if found |

---

## Quick Wins

> The 3–5 fixes that will have the biggest SEO impact with the least effort. Do these first.

1. **[Fix name]** — [1-sentence explanation of impact] → affects [N] pages
2. **[Fix name]** — [explanation] → affects [N] pages
3. **[Fix name]** — [explanation] → affects [N] pages
4. *(optional)* **[Fix name]** — [explanation]
5. *(optional)* **[Fix name]** — [explanation]

---

## Severity Reference

| Level | Meaning |
|-------|---------|
| `[Critical]` | Directly hurts rankings or breaks bilingual indexing. Fix immediately. |
| `[Warning]` | Suboptimal — reduces SEO effectiveness. Fix soon. |
| `[Info]` | Best-practice gaps with minor impact. Fix when convenient. |
