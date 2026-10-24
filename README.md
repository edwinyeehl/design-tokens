# @eyee/design-tokens

Official **Crédit Agricole CACEIS** design tokens and Tailwind CSS v4 theme, built according to the **Graphic Guidelines 2026**.

This package provides OKLCH-based design tokens, CSS variables, and Tailwind CSS v4 `@theme inline` utilities that seamlessly integrate with upstream `shadcn/ui` components and enterprise application layouts.

---

## 1. Official 2026 Brand Palette

| Token / Colour | Role | Hex | RGB | CMYK | Pantone | OKLCH |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Green** | Core brand, headlines, primary buttons | `#006A4E` | `0, 106, 78` | `100, 0, 70, 45` | `342` | `oklch(0.465 0.095 167.0)` |
| **Blue (Teal)** | Core brand & logo, secondary actions | `#009597` | `0, 149, 151` | `100, 0, 40, 15` | `321` | `oklch(0.607 0.103 196.5)` |
| **Peacock Blue** | **Official body copy & text colour** | `#004652` | `0, 70, 82` | `100, 77, 64, 0` | `7477` | `oklch(0.362 0.064 213.9)` |
| **Almond Green** | Background blocks & surface tinting | `#B4E6B4` | `180, 230, 180` | `25, 0, 35, 0` | `2253` | `oklch(0.877 0.085 144.8)` |
| **Red** | Accent, frog mascot, logo accent mark | `#ED1B2F` | `237, 27, 47` | `0, 100, 100, 0` | `485` | `oklch(0.604 0.234 24.8)` |
| **Aniseed Green** | Secondary highlight / badge accents | `#99CC00` | `153, 204, 0` | `45, 0, 100, 0` | `2292 C` | `oklch(0.780 0.198 125.7)` |

---

## 2. Typography Rules (Graphic Guidelines 2026)

* **Headlines (`h1`–`h6`):**
  * Set in uppercase only (`uppercase`).
  * Coloured in Crédit Agricole CACEIS Green (`#006A4E` / `var(--primary)`).
  * Web/Digital Font: **`Montserrat`** (Bold / ExtraBold).
* **Body Copy:**
  * Coloured in Peacock Blue (`#004652` / `var(--foreground)`), not pure black.
  * Web/Digital Font: **`Montserrat`** (Regular / Medium).
* **Fallback Font:** `Arial`, `sans-serif`.

---

## 3. Installation & Consumption

### Option A: Gitea NPM Package Registry

1. **Configure `.npmrc` in your consumer app:**
   ```ini
   registry=https://artifactory.caceis.internal/api/npm/npm-virtual/
   @eyee:registry=https://gitea.caceis.internal/api/packages/eyee/npm/
   ```

2. **Install the package:**
   ```bash
   pnpm add @eyee/design-tokens
   ```

3. **Import into your CSS entrypoint (`src/index.css` or `src/globals.css`):**
   ```css
   @import "tailwindcss";
   @import "@eyee/design-tokens";
   ```

---

### Option B: Native `shadcn` CLI Theme

If your project consumes the internal `@eyee` registry defined in `components.json`:

```bash
npx shadcn@latest add @eyee/theme
```

This applies the `theme.json` configuration directly to your Tailwind v4 CSS variables.

---

## 4. Tailwind CSS v4 Direct Utility Classes

In addition to standard `bg-primary`, `text-primary`, and `bg-secondary` semantic utilities, you can directly access the brand palette:

```html
<!-- CACEIS brand colours -->
<div class="bg-caceis-green text-white">...</div>
<div class="bg-caceis-blue text-white">...</div>
<div class="text-caceis-peacock">Official body text</div>
<div class="bg-caceis-almond">Tinted surface</div>
<span class="bg-caceis-red text-white">Accent badge</span>
<span class="bg-caceis-aniseed text-caceis-peacock">Highlight tag</span>
```

---

## 5. Repository File Structure

```
design-tokens/
├── package.json    # @eyee/design-tokens package definition
├── styles.css      # Core Tailwind v4 @layer base & @theme inline tokens
├── tokens.json     # W3C-compliant raw design token manifest
├── theme.json      # shadcn/ui registry:theme item
└── README.md       # Documentation & guidelines
```

---

## 6. Publishing to Gitea NPM Registry

To publish a new version of the tokens:

```bash
# 1. Login to Gitea npm registry
npm login --registry=https://gitea.caceis.internal/api/packages/eyee/npm/ --scope=@eyee

# 2. Publish package
npm publish
```
