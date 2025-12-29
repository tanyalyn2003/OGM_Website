# Copilot Instructions for OGM Website Development

## Project Overview
**Type:** Static HTML/CSS marketing website (no build process, no backend)  
**Client:** Olive Glass & Marble — custom stone, glass, and quartz countertops (Fayetteville, NC)  
**Users:** B2B (general contractors, architects, designers) + B2C (homeowners)  
**Services:** Consultation, fabrication, installation of countertops, shower doors, mirrors, glazing systems

## Architecture & File Structure
```
site/
├── index.html          # Homepage: hero, services, materials, gallery, reviews
├── about.html          # Company history, team bios, facility details
├── products.html       # 8 product categories (Quartz, Granite, Marble, Showers, Mirrors, Glazing, Sinks, Edges)
├── commercial.html     # B2B focus: project types, capabilities, contractor portfolio
├── gallery.html        # 9 project showcase items with category filter pills
├── contact.html        # Contact form, hours, review links, social
├── our-process.html    # 3-step process: Design → Fabrication → Installation
└── assets/
    ├── img/            # 7 images (home-kitchen-1-5.jpg, ogm-logo.png, msi-marble-carrara-white.png)
    ├── css/            # (placeholder for future consolidation)
    └── js/             # (placeholder for future interactivity)
```

## Design System

### Colors (CSS Custom Properties)
```css
--accent: #C9A87C;          /* Warm bronze (primary CTA, highlights) */
--accent-dark: #B89466;     /* Darker bronze (hover states) */
--bg-light: #FAF9F6;        /* Off-white page background */
--text-main: #1A1A1A;       /* Dark gray body text */
--text-muted: #6A6A6A;      /* Light gray secondary text */
--surface: #F2EEE8;         /* Beige card/section backgrounds */
--border-subtle: #DAD7D0;   /* Lightest border color */
```

### Responsive Grid Breakpoints
- **Desktop (1120px):** 3 columns (services, materials, gallery items)
- **Tablet (768px):** 2 columns
- **Mobile (640px):** 1 column (full-width stacked layout)

Use `@media (max-width: 640px)` for mobile overrides. All pages use `max-width: 1120px` container with `padding: 0 1.25rem`.

### Typography
- **Font:** `system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`
- **Line Height:** `1.6`
- **Headings:** H1 (1.8rem), H2 (1.4rem), H3 (1.1rem) — use `font-weight: 600`
- **Body:** 0.95–1rem for body text, 0.78rem for labels/captions

## Page Structure Pattern

### Every page follows this template:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>[Page Title] — Olive Glass & Marble</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="description" content="[50–160 char description]" />
  <style>
    /* Embedded CSS — see "CSS Conventions" below */
  </style>
</head>
<body>
  <header>
    <!-- Sticky nav with logo, 7 nav links (hardcoded) -->
  </header>
  <main class="container">
    <!-- Page-specific content -->
  </main>
  <footer>
    <!-- Contact info, copyright, social links -->
  </footer>
</body>
</html>
```

### Header (Sticky)
- **Position:** `position: sticky; top: 0;` with `background: rgba(26, 26, 26, 0.92)`
- **Logo:** 42×42px image (`assets/img/ogm-logo.png`) with company name + tagline ("Stone · Glass · Quartz")
- **Nav Links:** 7 links, all pages in same folder (relative paths: `index.html`, `products.html`, `commercial.html`, `our-process.html`, `about.html`, `gallery.html`, `contact.html`)
- **Color:** Text is light (`#e5e7eb`), with subtle border-bottom (`1px solid rgba(148, 163, 184, 0.3)`)

### Footer (Dark)
- **Background:** `#1A1A1A`
- **Content:** Copyright, address (714 Robeson Street, Fayetteville NC 28305), phone (910-484-5277), hours, review links (Houzz, Angi, Yelp, Yahoo, Google), social (Facebook, Instagram, Google Maps)
- **Text Color:** `#9CA3AF` (muted gray)

## CSS Conventions

### Current Status
All CSS is **embedded within `<style>` tags** in each HTML file (approximately 600 lines per page, ~70% duplication across pages).

### Key Patterns
1. **CSS Variables** defined in `:root { }` at top of every page
2. **Reset:** `* { box-sizing: border-box; margin: 0; padding: 0; }`
3. **Button Styling:** `.btn` class with `background: var(--accent)`, `padding: 0.75rem 1.6rem`, `border-radius: 999px`
4. **Container:** `max-width: 1120px; margin: 0 auto; padding: 0 1.25rem;`
5. **Grid Layouts:** `display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 1.25rem;`
6. **Transitions:** Use `transition: background 0.2s ease, transform 0.15s ease;` for interactive elements
7. **Responsive:** Mobile-first breakpoint at `@media (max-width: 640px) { ... }`

### Future Consolidation Opportunity
Extract all duplicate CSS to `site/assets/css/styles.css` — would reduce total CSS by ~60% (from 4,200 lines to ~1,500 lines). Ensure color variables remain in :root for easy rebranding.

## Content Patterns

### Business Domain Context
- **Years in business:** 20+ years (family-owned)
- **Core competency:** In-house design, templating, fabrication, installation
- **Materials:** Granite, quartz, marble, glass, mirrors
- **Service radius:** North Carolina, South Carolina, Tennessee
- **Differentiator:** "Family-owned stone & glass experts"; "We handle every step in-house"

### Page Types

#### Service Pages (index.html, about.html, our-process.html)
- Hero section with headline + supporting copy
- 3-column grid of service/process steps (Desktop → 1-column Mobile)
- Call-to-action button ("Schedule a free consultation", "Learn more", "View gallery")
- No forms; CTAs link to contact.html or external review sites

#### Product/Catalog Pages (products.html, commercial.html, gallery.html)
- Category or project showcase
- Grid layout with cards (image, title, description)
- Filter pills (visual only; no JavaScript filtering yet)
- Each card links to contact form or external resource

#### Contact Page (contact.html)
- Static HTML form (no backend integration yet; form does not submit)
- Business hours, phone, address, email
- Links to review platforms (Houzz, Angi, Yelp, Yahoo, Google)
- Social media links (Facebook, Instagram, Google Maps)

## Navigation

### Structure
All 7 pages link to each other via relative paths in the sticky header. **Navigation is hardcoded on every page** — no centralized nav component.

### Link Order (as deployed)
1. Home (`index.html`)
2. Products (`products.html`)
3. Commercial (`commercial.html`)
4. Our Process (`our-process.html`)
5. About (`about.html`)
6. Gallery (`gallery.html`)
7. Contact (`contact.html`)

**Important:** When adding new pages, update the `<nav>` section on all 7 existing pages.

## Local Development

### Preview Site Locally
```bash
cd /Users/tanyawhite/Desktop/OGM\ /OGM_Website/site
python3 -m http.server 8000
# Open http://localhost:8000
```

### Asset Paths
All asset references use relative paths from the `site/` folder:
- Images: `assets/img/filename.jpg`
- CSS: (currently embedded; would be `assets/css/styles.css` if consolidated)
- JavaScript: (currently minimal; would be `assets/js/script.js` if needed)

## Known Limitations & Improvement Opportunities

### Current (As-Is)
- ✅ All 7 pages exist and link correctly
- ✅ Design system established and consistent
- ✅ Responsive layout working (tested at 640px, 768px, 1120px)
- ✅ Images and logo in place

### Not Yet Implemented
- ❌ **CSS consolidation:** Embed CSS is 70% duplicated; extract to `site/assets/css/styles.css`
- ❌ **Contact form backend:** Currently static HTML; needs Formspree, Netlify Forms, or email service integration
- ❌ **Mobile menu:** Hamburger toggle exists in markup but non-functional (no JavaScript)
- ❌ **Gallery interactivity:** Filter pills are visual-only; requires JavaScript filtering logic
- ❌ **Hosting:** Not yet deployed (currently local preview only)

## Coding Tasks Guidelines for AI Agents

### When Adding a New Page
1. Create `site/[page-name].html` following the template in "Page Structure Pattern"
2. Include all 7 nav links (copy from any existing page)
3. Use color variables from `:root` (--accent, --text-main, etc.)
4. Make layout responsive with `@media (max-width: 640px)`
5. Add footer with copyright + contact info (copy from footer.html pattern)
6. Update `<nav>` on all 6 existing pages to include link to new page

### When Updating Design/Colors
- Modify CSS variables in `:root { }` only
- Search for hardcoded colors and replace with variable names (`var(--accent)`, `var(--text-main)`, etc.)
- Test at 640px (mobile), 768px (tablet), 1120px (desktop)

### When Adding Images
- Place in `site/assets/img/`
- Use descriptive filenames (e.g., `home-kitchen-1.jpg`, not `IMG_7126.JPG`)
- Optimize for web (aim for <200KB per image)
- Reference with relative path: `<img src="assets/img/filename.jpg" alt="description" />`

### When Adding Interactive Features (Forms, Filters, Menus)
- Create `site/assets/js/script.js` and link via `<script src="assets/js/script.js"></script>` before closing `</body>`
- Keep JavaScript minimal and focused (no frameworks; vanilla JS or lightweight library)
- Test on mobile (640px) and desktop (1120px)

## Contact Info & Review Links

**Showroom:** 714 Robeson Street, Fayetteville NC 28305  
**Phone:** 910-484-5277  
**Hours:** Mon–Thu 8–5, Fri 8–4  
**Reviews:** [Houzz](https://houzz.com) | [Angi](https://angi.com) | [Yelp](https://yelp.com) | [Yahoo](https://local.yahoo.com) | [Google](https://google.com/maps)  
**Social:** Facebook | Instagram | Google Maps

---

**Last Updated:** Current session  
**Maintained By:** AI agents and development team
