# Glam Lab: Technical SEO & Performance Audit (Block 13)

**Version audited:** v2 (`glam-lab-v2`)
**Version published after the fixes:** v3 (`glam-lab-v3`)

Each change below records the original issue, the change made, why it was made, and the result.
Results were measured locally in Chrome before publishing. After publishing on GitHub Pages, run **PageSpeed Insights** and **Lighthouse** on the live URL and add those scores in the table at the end.

---

## 1. Heading structure

| | |
|---|---|
| **Issue** | The page had **five `<h1>` elements**. The home `<h1>` was the logo image, and each of the other four sections (Wardrobe, Style Book, Plan, Create) had its own. Inside "Create", the panels "My Clothes" and "Your Outfit" were `<h2>`, at the same level as the page title. |
| **Change** | One `<h1>`: the main headline "Your Clothes. Your Style." The logo is now a plain image container. Section titles (My Wardrobe, My Style Book, Plan My Week, Create My Outfit) are `<h2>`, and the panels inside Create are `<h3>`. CSS keeps the same look, so the levels were chosen for meaning, not size. |
| **Why** | One clear main heading and a logical hierarchy help readers, screen readers and search engines understand the page. |
| **Result** | Exactly **1 `<h1>`**, with the hierarchy h1 → h2 → h3 and no skipped levels. The design looks the same. |

## 2. Page title and meta description

| | |
|---|---|
| **Issue** | The title "Glam Lab Studio" didn't say what the site is. The meta description had been added only to the GitHub copy, not to the page source. |
| **Change** | Title: **"Glam Lab \| Digital Wardrobe & Outfit Planner"**. The new meta description summarises what the site does: upload clothes, build outfits, plan the week, save looks. |
| **Why** | The title is the first line of a search result. It should be specific and accurate, and the description should summarise the page honestly. |
| **Result** | The title now names the site and its purpose, and the description matches the visible content. |

## 3. Canonical URL, social preview and structured data

| | |
|---|---|
| **Issue** | No canonical URL, no Open Graph tags for link previews, and no structured data. |
| **Change** | Added `<link rel="canonical">`, Open Graph tags (`og:title`, `og:description`, `og:url`, `og:image`), and a **JSON-LD `WebApplication`** block listing the name, description, category and only the features that appear on the page. |
| **Why** | The canonical tag names the preferred URL, for example GitHub Pages can serve the page as both `/` and `/index.html`. Structured data describes the visible content in a machine-readable way. |
| **Result** | Paste the live URL into Google's **Rich Results Test** or the **Schema Markup Validator** to check it. |

## 4. Images: modern format, responsive sizes and dimensions

| | |
|---|---|
| **Issue** | All images were JPG only, served at one size to every screen, and had no `width`/`height` attributes, which risks layout shift. |
| **Change** | Made **WebP** versions of every image in two sizes and served them with `<picture>`, `srcset` and `sizes`, keeping the JPGs as a fallback. Added `width` and `height` to every `<img>`. The main hero image gets `fetchpriority="high"` and is **not** lazy-loaded. The design-board images lower down keep `loading="lazy"` and gain `decoding="async"`. The menu logo now uses the small WebP. |
| **Why** | Images are the heaviest resources on the page. Smaller formats and the right size for each screen speed up loading (LCP), and reserved dimensions prevent content jumping (CLS). |
| **Result** | Home page image weight dropped from **≈448 KB to ≈159 KB (−64%)**, or ≈115 KB on small screens. Hero illustration: 134 KB → 50 KB. Layout shift measured at **CLS 0.000** and local **LCP ≈0.5 s** (the hero image). Live results will differ from these local numbers. |

## 5. Fonts

| | |
|---|---|
| **Issue** | Plus Jakarta Sans loaded weight **500**, which the design never uses. The "Home" link used a weight that wasn't loaded, so the browser had to substitute one. |
| **Change** | Removed weight 500 from the font request (9 → 8 font files) and set the "Home" link explicitly to Bodoni 500, which is loaded. Fonts keep `display=swap` so text shows immediately. |
| **Why** | Each font weight is a separate download. Load only the weights the design uses. |
| **Result** | One less font file to download, and no font substitution. |

## 6. Content visible without JavaScript

| | |
|---|---|
| **Issue** | The home sections "Your wardrobe at a glance" and "Your closet in numbers" were empty in the HTML and filled in by JavaScript. Without JavaScript, crawlers and visitors saw nothing there, and the boxes jumped in size when the script ran. |
| **Change** | Wrote the starting content (the four category tiles and the stats cards) directly in the HTML. JavaScript updates them once your data loads. Added a `<noscript>` message explaining that the app needs JavaScript. |
| **Why** | Important information should be in accessible HTML, and layout shouldn't change after load. |
| **Result** | Every section has content before any script runs, and the category tiles are now real links in the HTML that crawlers can follow. |

## 7. robots.txt, sitemap.xml and favicon

| | |
|---|---|
| **Issue** | There was no `robots.txt` or `sitemap.xml`, and no favicon, so browsers requested `/favicon.ico` and got a 404 error. |
| **Change** | Added `robots.txt`, which allows all crawlers and points to the sitemap; `sitemap.xml`, which lists the single preferred URL; a small SVG favicon (sparkle on pink) embedded in the page, so it needs no extra file; and `theme-color`. |
| **Why** | The sitemap tells search engines which URL is preferred, and robots.txt gives crawlers instructions (it isn't a security system). |
| **Result** | Both files are at the site root and the favicon 404 is gone. |

---

## Decisions explained (not changed)

- **Hash links (`#wardrobe`, `#create`, …):** Glam Lab is a single-page app. All its text is in one HTML document, which is why the sitemap lists one URL. The pages are still reachable through normal `<a href>` links in the menu and footer.
- **Inline script, no `defer`:** the JavaScript is written inline at the end of `<body>`, so it already runs after the HTML is parsed. No frameworks or third-party scripts are loaded.
- **User photos:** photos people upload are resized to at most 900 px and compressed in the browser before they're saved.

## Results after publishing (fill in)

| Tool | Mobile | Desktop |
|---|---|---|
| PageSpeed Insights: Performance | | |
| PageSpeed Insights: SEO | | |
| Lighthouse: Accessibility | | |
| LCP / INP / CLS | | |
| W3C HTML Validator: errors | | |

## Before publishing

Replace `YOUR-USERNAME` with your GitHub username (and `glam-lab` with your repository name, if it's different) in:

- `index.html`: canonical, `og:url`, `og:image`, JSON-LD `url`
- `robots.txt`
- `sitemap.xml`
