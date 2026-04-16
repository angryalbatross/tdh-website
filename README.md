# Third Day Horticulture — tdhort.com

Hugo-powered lead-generation website for Third Day Horticulture in Tyler, Texas. Specializes in container gardens, commercial planters, and seasonal planter rotations.

## Build

```bash
hugo server
# production
hugo --minify
```

## Sitemap

- `/` Home
- `/services/` Services (overview)
  - `/services/commercial/`
  - `/services/residential/`
  - `/services/seasonal-rotations/`
- `/about/` About
- `/gallery/` Gallery (`/projects/` redirects here)
- `/contact/` Contact

## Project structure

- `content/` — Page front-matter (routes, meta titles/descriptions)
- `data/projects/*.yaml` — Gallery items (title, subtitle, category, img/preview)
- `layouts/` — Section templates (home, services, about, contact, gallery)
- `layouts/partials/header.html` + `footer.html` — Site-wide layout shell, overrides the minimal theme
- `static/css/tdh.css` — Custom design system (overrides theme + bootstrap)
- `static/img/portfolio/` — All photography used on the site (reused from the original `projects` data)

## Reused assets

All imagery comes from the existing `static/img/portfolio/` directory — no new stock images introduced. Key roles:

- `IMG_7687.JPG` — hero, banners, commercial
- `IMG_7979.jpeg` — commercial services
- `EABS8299.JPG` — residential services
- `IMG_0062.JPG` — seasonal rotations
- `IMG_7692.jpeg` — About / founder
- `IMG_7734.JPG`, `IMG_7685.JPG`, `IMG_0012.JPG` — seasonal cards
- Remaining `portfolio/*.JPG|jpeg` — gallery

## Missing / recommended assets

Worth sourcing on the client's next shoot:

1. Headshot of Alison Burgett (Founder) for the About page split
2. Wide horizontal hero-oriented photographs (current library is mostly vertical hospital shots)
3. Country club entry planter photography (currently implied, not pictured)
4. Winter / holiday container installs (referenced in Seasonal Rotations)
5. "Before / after" residential examples

## Metadata / SEO

- Per-page `metaTitle`, `metaDescription`, `ogImage` via front matter
- LocalBusiness JSON-LD rendered on the home page (`layouts/partials/header.html`)
- Canonical, Open Graph, Twitter, and geo meta on every page
- `robots.txt` + Hugo-generated `sitemap.xml`
- `aliases` on `/gallery/` redirect old `/projects/` URL; also handled in `_redirects` for Netlify
