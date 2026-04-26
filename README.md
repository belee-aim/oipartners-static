# oipartners.io — Wayback Machine restoration

Restored on 2026-04-25 from web.archive.org snapshots. This is a **static HTML** rebuild — there is no PHP / Laravel / database; original site was a dynamic Laravel app on cPanel.

## How to view

Either open `index.html` directly in a browser (file://) or run a static server:

```
cd oipartners
python3 -m http.server 8000
# then browse http://localhost:8000
```

All internal links are depth-aware relative paths, so both `file://` and an HTTP server work.

## What was restored (32 files, ~2.1 MB)

15 HTML pages — `index.html`, `blog.html`, `blog-page-2.html`, `contact-us.html`, `group.html`, `division/{luxury-brands,outdoor-brands,wholesale}.html`, `page/{customer-care,sustainability,work-with-us}.html`, `post/{6,9,11,23}.html`.

3 CSS — `css/{style,plugins,custom}.css`. 3 JS — `js/{jquery,plugins,functions}.js`. 9 images under `storage/{items,blogs,settings}/`. `robots.txt`.

## Snapshot dates used

Each page was pulled from its **most recent** successful Wayback capture (range Sep 2024 – Mar 2026). Assets are from the 2025-03-14 crawl. Where Wayback's CSS rewrites had embedded archived URLs, they were stripped back to the originals.

## Language coverage

The site was a Laravel app with a Mongolian / English language switcher backed by a session cookie (`/lang/mn`, `/lang/en`). Wayback **only ever captured the Mongolian-default version** — those switcher endpoints are dynamic redirects and were never archived, so a separate English-only build is not recoverable. Note: the captured pages are still partly bilingual because the original markup interleaves English marketing copy with Mongolian navigation labels — this is how the live site looked too. The switcher links in the rebuild have been disabled (turned into `href="#"`).

## Known limitations

**Theme assets never crawled.** The original CSS references decorative assets that Wayback never captured (e.g., `images/expand.png`, `webfonts/inspiro-icons.{ttf,woff}`, `images/overlay-pattern/*`, `images/triangle-divider-*`, `images/dropdown-arrow.png`). The icon font in particular means custom theme icons fall back to default glyphs. Pages render correctly otherwise.

**Storage images partially recovered.** Wayback captured 10 files under `/storage/`. After deep-search across Wayback's CDX, Wayback's `available` API per-file, archive.today (returned "No results" for the entire domain), and Google Cache (deprecated), 38 referenced images were never archived. Two of those have been substituted from public sources via Wayback:

- `storage/divisions/June2023/Mongolia_blank.svg` — recovered from Wikimedia Commons (the original site referenced this Wikipedia file as `2560px-Mongolia_blank.svg copy2.jpg`; the wholesale page now points at the recovered SVG)
- `storage/brands/July2023/nCZIR0gfvMpwRg43xBLP.jpg` — Vibram logo recovered from vibram.com via Wayback

The other 36 images (brand logos for Moncler, Bally, Garmont, Clorts, Kailas, Humtto, Trex Pro; sustainability/blog hero photos; division illustrations; customer-care illustrations) are not on any archive. A CSS placeholder (light grey + image icon) renders for these so the layout doesn't break.

**Backslash-pathed images.** `division/wholesale.html` references five images with literal Windows-style backslashes in the URL (`/storage/strengths\May2023\…`) — a Laravel bug in the original site. These were broken on the live site too.

**Disabled in static.** The contact form's `action` endpoint, the `/lang/mn` ↔ `/lang/en` switcher, and the blog's pagination beyond page 2 are server-side. The switcher and missing pagination links have been replaced with `href="#"`. The contact form's HTML is preserved but submitting it will do nothing.

**Pagination patched.** The blog `?page=1` link has been remapped to `blog.html`, and `?page=2` to `blog-page-2.html`. There were no further blog pages archived.

## Files

- `index.html` — homepage
- `blog.html`, `blog-page-2.html` — blog listing pages
- `post/{6,9,11,23}.html` — individual blog posts
- `division/{luxury-brands,outdoor-brands,wholesale}.html` — division pages
- `page/{customer-care,sustainability,work-with-us}.html` — info pages
- `group.html`, `contact-us.html` — about / contact
- `css/`, `js/`, `storage/` — assets
- `robots.txt`
