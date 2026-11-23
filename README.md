# Glam Lab

Your personal style studio. Upload photos of your clothes, mix them into outfits (or let the site surprise you), plan what to wear each day of the week, and save your looks to a style book.

## Pages

- **Home**: the hero from my original design, plus your wardrobe at a glance, how Glam Lab works, your closet in numbers, and a section on how the site was made.
- **My Wardrobe**: upload clothes into Tops, Bottoms, Shoes and Accessories. Plain, light backgrounds are removed automatically, and each piece gets a colour and a name (for example "Pink top"). Tap a piece to rename it, move it to another rail or delete it.
- **Create My Outfit**: tap or drag clothes onto the board, drag to move, drag a corner to resize, or press **Surprise me** for a random combination of clothes you own, chosen so the colours go together. Name the look and save it.
- **My Style Book**: every saved look, with **Edit outfit** and **I wore this** to track how often you wear it.
- **Plan My Week**: pick a saved look for each day and move between weeks.

### Try it with sample clothes

The wardrobe starts empty. To see how everything works without uploading anything, press **✦ Try with sample clothes**, either on the home page or below the wardrobe grid. It adds 17 example pieces (6 tops, 4 bottoms, 3 shoes, 4 accessories) and 3 example looks ("Weekend denim", "Cosy autumn" and "Office chic"), all labelled **Sample**. Press **Remove sample clothes** to clear them; your own clothes are never touched. The sample images only download when the button is pressed, so they don't slow down the first page load.

## How it was made

I designed every screen first as four design boards (`assets/board1.jpg` to `board4.jpg`). I then built the website with Claude, an AI assistant, helping with the code.

- **Look:** inspired by the playful pink, sparkles and pastel tiles of fashion-doll shops.
- **How it works:** inspired by wardrobe apps like GetWardrobe (photograph what you own, get outfit ideas from it, plan your week, track what you wear).

**Built with:** HTML, CSS and JavaScript, the Canvas API for background removal and colour detection, IndexedDB for saving, and Google Fonts (Bodoni Moda, Plus Jakarta Sans, Gochi Hand). There are no frameworks and no build step.

## SEO and performance (Block 13)

See [`CHANGELOG-SEO.md`](CHANGELOG-SEO.md) for the audit: each issue, the change made and the result. In summary: one `<h1>`, a descriptive title and meta description, a canonical URL, Open Graph tags, JSON-LD structured data, responsive WebP images with fixed dimensions (64% lighter), fewer font files, content that shows without JavaScript, `robots.txt`, `sitemap.xml` and a favicon.

## Where data is saved

Clothes, looks and plans are saved in the visitor's own browser (IndexedDB). Each person gets a private wardrobe, but it doesn't sync between devices, and clearing browser data deletes it. Nothing is uploaded to a server.

## Files

```
index.html          the whole app
assets/*.jpg        original images (fallback for older browsers)
assets/*-NNN.webp   WebP versions of each image in two sizes
assets/sample-*.webp 17 sample clothing pieces (loaded only on request)
robots.txt          crawler instructions
sitemap.xml         preferred URL for search engines
CHANGELOG-SEO.md    Block 13 audit: issue, change and result for each fix
```

## Run it locally

Open `index.html` in a browser, or run a small local server from this folder:

```bash
python3 -m http.server 8000
```

Then go to http://localhost:8000.

## Put it online with GitHub Pages

**First:** replace `YOUR-USERNAME` with your GitHub username in `index.html`, `robots.txt` and `sitemap.xml`. If your repository isn't called `glam-lab`, replace that too.

1. Create a new **Public** repository on GitHub (for example `glam-lab`).
2. Click **Add file → Upload files**, drag in every file and the `assets` folder, then click **Commit changes**.
3. Go to **Settings → Pages**, choose **Deploy from a branch**, pick `main` and `/ (root)`, then click **Save**.
4. After a minute or two the site is live at `https://<your-username>.github.io/glam-lab/`.
5. Run [PageSpeed Insights](https://pagespeed.web.dev/) on the live URL and record the scores in `CHANGELOG-SEO.md`.
