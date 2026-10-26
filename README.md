# @eyee/design-tokens

Official **Crédit Agricole CACEIS** design tokens, Tailwind CSS v4 theme, and canonical brand assets, built strictly according to the **Graphic Guidelines 2026**.

This package provides OKLCH-based design tokens, CSS variables, Tailwind CSS v4 `@theme inline` utilities, and transparent high-resolution brand logo assets that seamlessly integrate with upstream `shadcn/ui` components and enterprise application layouts.

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

All logo assets are 2000px high-resolution, transparent RGBA PNGs covering both orientations and all 3 authorized color treatments:

```text
assets/logos/
├── caceis-logo-horizontal-color.png    # Primary horizontal logo (Full Colour)
├── caceis-logo-horizontal-white.png    # Horizontal logo (100% Reversed White)
├── caceis-logo-horizontal-black.png    # Horizontal logo (Monochrome Black)
├── caceis-logo-vertical-color.png      # Primary vertical stacked logo (Full Colour)
├── caceis-logo-vertical-white.png      # Vertical stacked logo (100% Reversed White)
└── caceis-logo-vertical-black.png      # Vertical stacked logo (Monochrome Black)
```

### Brand Usage & Compliance Rules

1. **Orientation Selection:**
   * **Vertical (Stacked):** Preferred default format for print, hero cards, splash screens, and login dialogs.
   * **Horizontal:** Authorized alternative optimized for top navigation headers, standard web bars, and email footers.
2. **Breathing Area (Exclusion Zone):**
   * Keep a minimum margin of **`1.5X`** around all 4 sides of the logo, where **$X$** is the height of the green horizontal base bar in the monogram. No text, buttons, or edges may cross this boundary.
3. **Minimum Digital Size:**
   * Digital web applications must render the logo at a minimum width of **`110 px`** (`min-w-[110px]`) to maintain legibility.
4. **Background Contrast Rules:**
   * **Full Colour (`*-color.png`):** Use strictly on white, light grey, or very light almond-tinted surfaces. *Never* place on dark or low-contrast backgrounds.
   * **Reversed White (`*-white.png`):** Use on dark backgrounds, solid CACEIS Green headers (`#006A4E`), or collapsed dark navigation sidebars.
   * **Monochrome Black (`*-black.png`):** Reserved for single-color print or strict high-contrast grayscale documentation.

---

## 4. Usage in React / Next.js / Vite Applications

### Direct Import via Bundler (Standard npm)

```tsx
import logoHorizontalColor from "@eyee/design-tokens/assets/logos/caceis-logo-horizontal-color.png";
import logoHorizontalWhite from "@eyee/design-tokens/assets/logos/caceis-logo-horizontal-white.png";

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

   # Scoped registry for @eyee packages (Nexus npm-hosted)
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
