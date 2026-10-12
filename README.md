# Responsive Pricing Table

A modern, responsive pricing table component crafted strictly with **HTML5** and **CSS3**, aligned with front-end engineering assessment guidelines and modern web design standards.

## Project Overview

- **Objective:** Build a responsive, accessible pricing table featuring three pricing plans, distinct visual highlighting for a featured plan, interactive hover states, and smooth small-screen stacking.
- **Tech Stack:** Pure **HTML5** & **CSS3** (zero runtime dependencies, zero frameworks, zero JavaScript).
- **Core Principles:** Semantic markup, CSS Custom Properties (Tokens), Flexbox layouts, progressive enhancement, and mobile-first responsive mechanics.

---

## Approach & Architecture

### 1. Semantic HTML5 Structure
- Enclosed inside a `<main class="page-wrapper">` container for accessible landmark structuring.
- Grouped within a `<section class="pricing-table" aria-label="Pricing Plans">` block.
- Each pricing tier is encapsulated inside an `<article class="pricing-card">`, containing:
  - Header: Plan title (`<h2>`), target audience description, and dynamic price display (`<div class="price-container">`).
  - Feature List: Accessible unordered list (`<ul class="feature-list">`) with SVG-style semantic check (`✓`) and cross (`✕`) indicators.
  - Call to Action: Explicit `<button type="button">` with distinct primary/secondary visual hierarchy.

### 2. Dual-Axis Flexbox Layout Strategy
- **Container Layout (Horizontal Distribution):**
  - Uses `display: flex; justify-content: center; align-items: stretch; gap: 2rem;`.
  - Setting `align-items: stretch` guarantees that all three pricing cards naturally adopt identical visual heights regardless of variable text length.
  - Setting `flex: 1 1 0` on `.pricing-card` ensures equal distribution of the container's inline width across the three columns.
- **Card-Internal Layout (Vertical Distribution):**
  - Uses `display: flex; flex-direction: column;`.
  - Feature lists are given `flex-grow: 1;`.
  - CTA wrapper `.card-action` utilizes `margin-top: auto;` to push the button down to the card's baseline, guaranteeing uniform button alignment across all three columns.

### 3. Visual Polish & Micro-Interactions
- Layered box shadows for soft, realistic ambient lighting without harsh edges.
- Smooth CSS transitions (`transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1)`) for card elevation (`translateY(-8px)`) and button hover glow.
- Balanced top whitespace and compact typography using Google Font **Inter**.

---

## Key Deliverables & Outcomes

| Deliverable | Implementation Details | Status |
| :--- | :--- | :--- |
| **Three Pricing Cards** | **Basic** ($9/mo), **Pro** ($29/mo), and **Enterprise** ($79/mo) with complete feature lists and dedicated action buttons. | Verified |
| **Highlighted 'Popular' Plan** | The **Pro** tier is highlighted with a 2px colored border, elevated glowing box-shadow, desktop scale (`1.04`), and floating `'Most Popular'` ribbon badge. | Verified |
| **Responsive Stacking** | On screens $\le 768\text{px}$, the Flexbox container transitions to `flex-direction: column; align-items: center;` with cards scaling to 100% width (max 440px). | Verified |
| **Hover Transitions** | Cards lift upward (`translateY(-8px)`) with expanded shadow depth; buttons exhibit active elevation, background color shifts, and focus ring accessibility. | Verified |
| **No External Scripts** | Strict compliance with assessment constraints: built exclusively using HTML5 and CSS3. | Verified |

---

## Assessment Interview Questions

### Q1: How would you highlight one plan over the others?

To establish strong visual hierarchy and emphasize the **Pro (Most Popular)** plan, a multi-layered design pattern is employed:

1. **Elevation & Scale:**
   - Desktop cards scale up slightly: `transform: scale(1.04);` and sit on a higher stacking context (`z-index: 2;`).
2. **Accented Border:**
   - Standard cards use a subtle border (`1px solid #e2e8f0`), while the featured card uses a bold colored accent (`2px solid var(--primary-color)`).
3. **Layered Ambient Glow / Shadow:**
   - While default cards use subtle greyscale shadows, the featured card incorporates a colored brand shadow:
     ```css
     box-shadow: 0 20px 35px -10px rgba(79, 70, 229, 0.25), 
                 0 4px 12px -2px rgba(79, 70, 229, 0.15);
     ```
4. **Floating Ribbon Badge:**
   - A high-contrast pill badge pinned to the top border (`top: -15px; left: 50%; transform: translateX(-50%);`) reading `"Most Popular"`.
5. **High-Contrast Call-to-Action:**
   - Standard plans use neutral ghost/secondary buttons (`.btn-secondary`), whereas the popular plan uses a solid, saturated primary button (`.btn-primary`) with glowing focus rings.

---

### Q2: What CSS properties create a card shadow?

The primary property is **`box-shadow`**. Its full syntax is:

```css
box-shadow: [inset] <offset-x> <offset-y> <blur-radius> <spread-radius> <color>;
```

#### Detailed Breakdown of Values:
- **`offset-x`**: Horizontal distance the shadow is cast (positive = right, negative = left).
- **`offset-y`**: Vertical distance the shadow is cast (positive = downward, negative = upward).
- **`blur-radius`**: Gaussian blur extent; larger values create softer, more diffused shadows.
- **`spread-radius`**: Expands (positive) or contracts (negative) the shadow footprint before blurring.
- **`<color>`**: Shadow tint, commonly specified using semi-transparent `rgba()` or `hsla()` values.
- **`inset`** *(optional)*: Directs the shadow inside the card border rather than outside.

#### Best Practice Implementation Used in This Project:
To achieve realistic, modern lighting rather than a muddy flat block, multiple shadows are layered together:

```css
/* Standard Card: Subtle directional drop + soft ambient occlusion */
--shadow-default: 
  0 4px 6px -1px rgba(0, 0, 0, 0.05),
  0 2px 4px -2px rgba(0, 0, 0, 0.05);

/* Featured Card: Vibrant brand color glow with depth */
--shadow-popular: 
  0 20px 35px -10px rgba(79, 70, 229, 0.25), 
  0 4px 12px -2px rgba(79, 70, 229, 0.15);
```

*(Note: For irregular or transparent shapes with SVG alpha masks, `filter: drop-shadow(...)` can also be used).*

---

### Q3: How does Flexbox distribute space between items?

CSS Flexible Box Layout distributes space along both the **main axis** and **cross axis** through several distinct mechanisms:

1. **Main Axis Alignment (`justify-content`):**
   - `space-between`: Distributes items evenly; the first item aligns flush with the start edge, the last item flush with the end edge, with remaining free space divided equally between items.
   - `space-around`: Distributes items such that each item has equal space on both sides (outer edges receive half the space of inner gaps).
   - `space-evenly`: Distributes space so that every gap (between items and between edges and items) is identical.
   - `center` / `flex-start` / `flex-end`: Clusters items together without extra interstitial spacing.

2. **Gutter Spacing (`gap`):**
   - The modern `gap` property (`gap: 2rem;`) defines clear spacing between items without requiring margin resets on `:first-child` or `:last-child`.

3. **Flex Item Sizing Factors:**
   - **`flex-grow`**: Determines how much of the remaining positive free space the item absorbs relative to sibling items.
   - **`flex-shrink`**: Controls the rate at which items contract when container space is insufficient.
   - **`flex-basis`**: Specifies the initial size of an item before remaining space is distributed.
   - In our layout: `flex: 1 1 0;` instructs all three cards to share container width uniformly.

4. **Auto Margins inside Flex Containers (`margin: auto`):**
   - In Flexbox, auto margins absorb all available free space along that direction.
   - On `.card-action`, declaring `margin-top: auto;` pushes the CTA button to the bottom of the card column, aligning all three action buttons uniformly along the bottom edge.

---

## Deployment Configuration

Because this project is built entirely with static **HTML5 and CSS3**, it requires **zero build steps, compilers, or server-side runtimes**. It can be served from any CDN or web server.

### 1. GitHub Pages (Recommended)
1. Push this repository to GitHub:
   ```bash
   git init
   git add .
   git commit -m "feat: complete responsive pricing table assessment"
   git branch -M main
   git remote add origin https://github.com/<username>/<repo-name>.git
   git push -u origin main
   ```
2. In the repository settings on GitHub:
   - Navigate to **Settings** > **Pages**.
   - Under **Build and deployment** > **Source**, select **Deploy from a branch**.
   - Set Branch to `main` and Folder to `/ (root)`.
   - Click **Save**. The page goes live immediately.

### 2. Vercel / Netlify
- **Build Command:** *(leave empty)*
- **Publish Directory:** `.` *(root)*
- Deploy time: $< 5\text{ seconds}$.

---

## Rollback Strategy & Evidence

### 1. Rollback Mechanism
- **Version Control Rollback:** Because the codebase is fully versioned with Git, any production issue or regression can be rolled back instantly to the prior stable commit:
  ```bash
  git revert HEAD --no-edit
  git push origin main
  ```
- **Zero-Downtime Atomic Rollback on CDNs:** On platforms such as Vercel, Netlify, or Cloudflare Pages, each deployment produces an immutable deployment URL. Rolling back takes one click to promote the preceding successful deployment.

### 2. Rollback Evidence & Iteration Log
- **v1.0 (Initial Build):** Created full prototype with additional JavaScript features.
- **v1.1 (Rollback to Assessment Scope):** Reverted cleanly to strictly HTML5 & CSS3 to adhere to assessment guidelines.

---

## File Structure

```
Pricing_Table/
├── index.html
├── style.css   
└── README.md   
```

---

