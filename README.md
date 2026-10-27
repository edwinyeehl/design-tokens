# @eyee/design-tokens

Official **Crédit Agricole CACEIS** design tokens, Tailwind CSS v4 theme, and canonical brand vector assets, built strictly according to the **Graphic Guidelines 2026**.

This package provides OKLCH-based design tokens, CSS variables, Tailwind CSS v4 `@theme inline` utilities, and razor-sharp, tightly trimmed SVG vector brand assets (along with lightweight WebP fallbacks) that seamlessly integrate with upstream `shadcn/ui` components and enterprise application layouts.

---

## 1. Official 2026 Brand Palette

| Token / Colour | Role | Hex | RGB | CMYK | Pantone | OKLCH |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Green** | Core brand, headlines, primary actions | `#006A4E` | `0, 106, 78` | `100, 0, 70, 45` | `342` | `oklch(0.465 0.095 167.0)` |
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
  * Web/Digital Font: **`Montserrat`** (Bold / ExtraBold) — official digital substitute for Gotham.
* **Body Copy:**
  * Coloured in Peacock Blue (`#004652` / `var(--foreground)`), not pure black.
  * Web/Digital Font: **`Montserrat`** (Regular / Medium).
* **Fallback Font:** `Arial`, `sans-serif`.

---

## 3. Official Brand Logos (`assets/logos/`)

All logo assets are provided as **tightly trimmed vector SVGs** (edge-to-edge bounding boxes, zero phantom margins, resolution-independent) alongside modern transparent **WebP** raster formats:

```text
assets/logos/
├── caceis-logo-horizontal-color.svg    # Primary horizontal logo (Full Colour, 1578x234 viewBox)
├── caceis-logo-horizontal-white.svg    # Horizontal logo (100% Reversed White, 1578x234 viewBox)
├── caceis-logo-horizontal-black.svg    # Horizontal logo (Monochrome Black, 1578x234 viewBox)
├── caceis-logo-vertical-color.svg      # Primary vertical stacked logo (Full Colour, 1514x894 viewBox)
├── caceis-logo-vertical-white.svg      # Vertical stacked logo (100% Reversed White, 1514x894 viewBox)
├── caceis-logo-vertical-black.svg      # Vertical stacked logo (Monochrome Black, 1514x894 viewBox)
└── *.webp                              # Transparent WebP trimmed fallbacks
```

### Brand Usage & Compliance Rules

1. **Orientation Selection:**
   * **Vertical (Stacked):** Preferred default format for hero cards, splash screens, and login dialogs.
   * **Horizontal:** Authorized alternative optimized for top navigation headers, standard web bars, and email footers.
2. **Breathing Area (1.5X Exclusion Zone):**
   * Keep a minimum margin of **`1.5X`** around all 4 sides of the logo, where **$X$** is the height of the green horizontal base bar in the monogram ($\approx 12\%$ of total logo height).
   * Because the SVGs are trimmed edge-to-edge, applying standard container padding (**`p-2`** or **`p-3`**) in CSS naturally satisfies this brand rule without phantom margin drift.
3. **Minimum Digital Size:**
   * Digital web applications must render the logo at a minimum width of **`110 px`** (`min-w-[110px]`) to maintain legibility.
4. **Background Contrast Rules:**
   * **Full Colour (`*-color.svg` / `*-color.webp`):** Use strictly on white, light grey, or very light almond-tinted surfaces. *Never* place on dark or low-contrast backgrounds.
   * **Reversed White (`*-white.svg` / `*-white.webp`):** Use on dark backgrounds, solid CACEIS Green headers (`#006A4E`), or collapsed dark navigation sidebars.
   * **Monochrome Black (`*-black.svg` / `*-black.webp`):** Reserved for single-color print or strict high-contrast grayscale documentation.

---

## 4. Usage in React / Next.js / Vite Applications

### Option A: Standard `img` Tag (Responsive SVG or WebP)

```tsx
import logoHorizontalColor from "@eyee/design-tokens/assets/logos/caceis-logo-horizontal-color.svg";
import logoHorizontalWhite from "@eyee/design-tokens/assets/logos/caceis-logo-horizontal-white.svg";

interface HeaderBrandProps {
  isDarkMode?: boolean;
}

export function HeaderBrand({ isDarkMode = false }: HeaderBrandProps) {
  return (
    <div className="flex items-center p-3">
      <img
        src={isDarkMode ? logoHorizontalWhite : logoHorizontalColor}
        alt="Crédit Agricole CACEIS"
        className="h-8 w-auto min-w-[110px] object-contain"
      />
    </div>
  );
}
```

### Option B: SVGR / Inline Component (Vite / Next.js)

```tsx
import LogoColor from "@eyee/design-tokens/assets/logos/caceis-logo-horizontal-color.svg?react";

export function Brand() {
  return (
    <div className="p-3">
      <LogoColor className="h-8 w-auto min-w-[110px]" />
    </div>
  );
}
```

---

## 5. Installation & Consumption Options (Standard npm)

### Option A: Direct Git Dependency (Zero Nexus Overhead)
Install directly from internal Gitea using standard `npm` without waiting for Nexus repository approvals:

```bash
npm install git+https://git.cicd.caceis.group.gca/eyee/design-tokens.git#main
```
Or for public GitHub access:
```bash
npm install git+https://github.com/edwinyeehl/design-tokens.git#main
```

In your application's `package.json`:
```json
{
  "dependencies": {
    "@eyee/design-tokens": "git+https://git.cicd.caceis.group.gca/eyee/design-tokens.git#main"
  }
}
```

---

### Option B: CACEIS Internal Nexus Repository
If publishing to the internal Nexus npm-hosted repository:

1. **Configure `.npmrc` in your consumer project:**
   ```ini
   # Default registry (Nexus npm-group for public packages)
   registry=https://nexus.cicd.caceis.group.gca/repository/npm-group/

   # Scoped registry for internal @eyee packages
   @eyee:registry=https://nexus.cicd.caceis.group.gca/repository/npm-hosted/
   always-auth=true
   ```

2. **Authenticate with Nexus:**
   ```bash
   npm login --registry=https://nexus.cicd.caceis.group.gca/repository/npm-hosted/ --scope=@eyee
   ```

3. **Install:**
   ```bash
   npm install @eyee/design-tokens
   ```

---

### Option C: Native `shadcn` CLI Theme
For applications consuming the custom `@eyee` registry defined in `components.json`:

```bash
npx shadcn@latest add @eyee/theme
```

---

## 6. CSS Integration (`src/index.css`)

```css
@import "tailwindcss";
@import "@eyee/design-tokens";
```

### Tailwind CSS v4 Direct Brand Utilities

```html
<!-- Direct brand palette utility classes -->
<div class="bg-caceis-green text-white">Primary Header</div>
<div class="bg-caceis-blue text-white">Action Badge</div>
<div class="text-caceis-peacock">Official body text</div>
<div class="bg-caceis-almond">Tinted surface card</div>
<span class="bg-caceis-red text-white">Alert tag</span>
<span class="bg-caceis-aniseed text-caceis-peacock">Highlight</span>
```

---

## 7. Publishing to Nexus (Standard npm)

```bash
# 1. Bump version in package.json
npm version patch

# 2. Publish to Nexus hosted registry
npm publish --registry https://nexus.cicd.caceis.group.gca/repository/npm-hosted/
```
