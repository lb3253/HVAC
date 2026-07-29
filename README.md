# Apex Air DFW

A single-page marketing website for **Apex Air DFW**, a fictional HVAC company serving the Dallas-Fort Worth Metroplex (Dallas, Fort Worth, Plano, Frisco, McKinney, Allen).

## Stack

Pure static HTML/CSS/JS — no build step, no npm, no framework. This is intentional so the site can be deployed directly to **Cloudflare Pages** from this GitHub repo with zero build configuration.

- `index.html` — everything: markup, CSS (in a `<style>` tag), and JS (in a `<script>` tag at the bottom)
- Fonts: Google Fonts (Inter) loaded via `<link>` — the only external dependency

## Local preview

Just open `index.html` in a browser, or serve it locally:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Deploying to Cloudflare Pages

1. Push this repo to GitHub (already done if you're reading this from the repo).
2. In the Cloudflare dashboard: **Workers & Pages → Create → Pages → Connect to Git**.
3. Select this repository.
4. Build settings:
   - **Build command:** (leave blank)
   - **Build output directory:** `/` (project root)
5. Deploy. No environment variables or build steps are needed.

## Wiring up the lead form

The contact section embeds a [Tally.so](https://tally.so) form via `<iframe>` + Tally's embed script:

```html
<div class="tally-embed">
  <iframe
    data-tally-src="https://tally.so/embed/zx4Qza?alignLeft=1&hideTitle=1&transparentBackground=1&dynamicHeight=1"
    ...>
  </iframe>
</div>
```

To point it at your own form:

1. Create your form on Tally.so and grab its form ID from the share URL (`https://tally.so/forms/<FORM_ID>` or `https://tally.so/r/<FORM_ID>`).
2. Replace `zx4Qza` in the `data-tally-src` attribute with your form ID.
3. Tally's own loader script (the last `<script>` block, just before `</body>`) handles rendering, resizing, and submission — no extra JS wiring needed.

Sizing for the embed lives in the `.tally-embed` CSS rule in the `<style>` block.

## Structure

The page is a single scroll with these sections (see `id` attributes in `index.html` for anchor targets):

1. **Navbar** — fixed, logo + phone + "Get a Free Quote" CTA, with scroll-based active-link highlighting (`IntersectionObserver`)
2. **Hero** (`#top`) — headline, subheadline, two CTAs
3. **Services** (`#services`) — AC Repair, New Installation, Maintenance Plans, Heating
4. **Why Choose Us** (`#why`) — Licensed & Insured, Same-Day Service, 10-Year Warranty
5. **Contact / Lead Form** (`#contact`) — the main conversion section
6. **Footer** — address, phone, email, copyright

## Customizing

- **Brand colors** are defined as CSS custom properties at the top of the `<style>` block in `index.html` (`--navy`, `--sky`, `--white`, `--light-gray`) — change them there to re-theme the whole site.
- **Copy/content** can be edited directly in the HTML; there's no templating layer.
