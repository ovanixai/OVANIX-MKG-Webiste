# IMPLEMENTATION_METADA.md - Website Metadata & Social Media Optimization

This plan outlines the steps to implement a robust metadata system for the MKG Gestion website, ensuring high-quality previews on social media (LinkedIn, Facebook, Twitter) and improved SEO.

## Background

The previous URL previews were blank or generic. We will replace them with specific branding and a professional snapshot of the website.

## Assets to be Created

### 1. Open Graph (OG) Image
- **Description**: A custom 1200x630px image reflecting the premium aesthetic of MKG Gestion ("Luxury Editorial Minimalism").
- **Content**: Moody, cinematic photography of a restaurant interior + MKG Gestion logo & typography.
- **Filename**: `og-image.png` (to be saved in `brand_assets/website_improvement/`)

### 2. Favicons
- **Description**: A full set of favicons for all devices.
- **Filename**: `favicon.ico`, `apple-touch-icon.png`, etc.

## Proposed Metadata Changes

### Global Standard Tags
Add the following to the `<head>` of all pages:
```html
<meta name="description" content="Leader québécois en gestion de franchises de restauration (Thaïzone, Yuzu Sushi). Excellence et innovation culinaire.">
<meta name="keywords" content="Restauration, Franchise, Québec, MKG Gestion, Thaïzone, Yuzu Sushi">
<meta name="author" content="MKG Gestion">
<meta name="theme-color" content="#111111">
```

### social Media (Open Graph & Twitter)
```html
<!-- Open Graph / Facebook / LinkedIn -->
<meta property="og:type" content="website">
<meta property="og:url" content="https://mkg-gestion.com/">
<meta property="og:title" content="MKG Gestion — Restauration · Franchise · Québec">
<meta property="og:description" content="Expertise et passion dans la gestion de franchises renommées au Québec.">
<meta property="og:image" content="brand_assets/website_improvement/og-image.png">

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:url" content="https://mkg-gestion.com/">
<meta name="twitter:title" content="MKG Gestion — Restauration · Franchise · Québec">
<meta name="twitter:description" content="Expertise et passion dans la gestion de franchises renommées au Québec.">
<meta name="twitter:image" content="brand_assets/website_improvement/og-image.png">
```

## Verification Plan

### Automated
1. **Check local files**: Verify the `<head>` content in `index.html`.
2. **Link Validation**: Ensure the paths to images are correct and accessible.

### Manual
1. **Social Media Debuggers**:
   - Facebook Sharing Debugger
   - LinkedIn Post Inspector
   - Twitter Card Validator
2. **Mobile Check**: Verify the theme color and favicon appear correctly on mobile browsers.
