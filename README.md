# Aarvi Industries — Website

A single-page website for **Aarvi Industries**, a tin & metal container manufacturer based in Anand, Gujarat, India. Built as one self-contained HTML file — no build tools, no framework, no server required to run it.

---

## What's in this repo

| File | Purpose |
|---|---|
| `aarvi-industries.html` | The entire website — HTML, CSS, JavaScript and all product/logo images (embedded as base64) in a single file. This is the only file you need to deploy. |
| `README.md` | This file. |

Everything the browser needs — fonts aside — is baked into `aarvi-industries.html`. You can open it by double-clicking it, host it anywhere that serves static files, or drop it straight into Netlify/Vercel.

---

## Pages (all in the one file)

The site is a single-page app: every "page" is a `<section class="page" id="...">` in the same HTML file, and navigation just swaps which one is visible using the URL hash (`#home`, `#about`, `#products`, `#industries`, `#capabilities`, `#quality`, `#contact`, `#privacy`, `#terms`) — no page reloads.

- **Home** — hero with drum carousel, featured custom builds, product categories, stats, "why us"
- **About** — company story, timeline, mission/vision/values
- **Products** — full container range (15 sizes/variants), click any card for a spec sheet in a modal
- **Industries** — sectors served
- **Capabilities** — manufacturing process, 5-step timeline
- **Quality** — quality control commitments and checkpoints
- **Contact** — enquiry form (see *Contact form* below) + company details
- **Privacy Policy / Terms & Conditions** — linked from the footer

---

## Running it locally

No installation needed — just open the file:

```
open aarvi-industries.html        # macOS
start aarvi-industries.html       # Windows
```

Or, to preview it closer to how it'll behave once hosted (recommended before testing the contact form), serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/aarvi-industries.html
```

---

## Editing content

You don't need to touch the HTML/CSS to update most content — the page data lives in a small set of JavaScript objects near the top of the `<script>` block, roughly in this order:

- `COMPANY` — name, tagline, address, phone numbers, email, hours, social links
- `SIZES` — the size list used in the scrolling ticker strip
- `PRODUCTS` — every container in the full product grid, including description/applications/material/features shown in the click-through modal
- `CATEGORIES` — the 6 product-category cards
- `INDUSTRIES` — the industries-served cards
- `WHY_US` — the 4-point "Why Choose Aarvi Industries" grid
- `CAPABILITIES` — the 5-step manufacturing process
- `STATS` — the animated counters on the homepage (**currently placeholder figures** — see *Known limitations*)

To change colors or fonts, edit the CSS custom properties at the very top of the `<style>` block (`--navy-900`, `--orange-600`, `--f-display`, `--f-body`, etc.) — everything on the site references these variables, so a single edit updates it everywhere.

If you're not comfortable editing the file directly, just describe the change and hand the file back — it can be edited and returned the same way it was built.

---

## Contact form (Formspree)

The enquiry form on the Contact page submits via [Formspree](https://formspree.io) (form ID `mdeonlpw`), which forwards submissions directly to `herry@aarviindustries.com`. No server of your own is involved.

- If you ever need to point it at a different Formspree form, change the `action="https://formspree.io/f/..."` URL on the `<form id="quote-form">` element.
- Formspree sends a one-time confirmation link to the receiving inbox when a form is created — until that's clicked, real submissions will be rejected even though the form looks like it's working.
- On success, the form shows an inline "Request sent successfully" message — no page reload, no redirect to Formspree.

---

## Deployment (recommended: GitHub + Netlify)

This is the easiest path to keep the site easy to update going forward.

1. **Buy a domain** — any registrar (Namecheap, GoDaddy, BigRock, Hostinger, etc.)
2. **Push this repo to GitHub** — keeps full version history of every change
3. **Connect the repo to Netlify** (free) — "Add new site → Import from GitHub"; Netlify auto-builds and gives you a live URL with free SSL
4. **Point your domain at Netlify** — add the DNS records Netlify shows you in your registrar's dashboard
5. **Test live** — check the site on mobile and desktop, submit a real test enquiry, confirm the padlock/HTTPS is active

From then on, updating the live site is just: edit → commit → push. Netlify redeploys automatically within about a minute.

---

## Browser support & responsiveness

Built and tested to work smoothly from small phones (~320px) up through large desktop monitors, with dedicated breakpoints at 480px, 640px, 760px, 900px and 980px. Uses standard modern CSS (Grid, custom properties, `clamp()`) and vanilla JavaScript — no polyfills included, so very old browsers (IE11 and earlier) are not supported.

---

## Known limitations

- **No backend or database.** This is a static file — nothing it displays is fetched from or saved to a server, aside from the Contact form's one-way delivery through Formspree.
- **Stats are placeholders.** The homepage counters (`35+` years, `1,800+` dies, etc.) were set as illustrative figures during development — replace them in the `STATS` array with verified numbers before relying on them publicly.
- **Privacy Policy & Terms are a good-faith starting point, not legal advice.** Both pages say so explicitly at the bottom — have them reviewed by a qualified professional before treating them as your official policy.
- **Google Fonts are loaded from Google's CDN.** This is normal for most modern sites, but means the page isn't 100% dependency-free at runtime (everything else is).
