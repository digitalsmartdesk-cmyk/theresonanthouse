# Resonant House — Claude Code handoff

Single-page marketing site for **Resonant House**, a strategic communications & PR practice
(books/publishing PR, op-eds, speaking placement, cultural work, reputation response).
Designed in Claude Design (project "Resonant House website design"); this package turns it into a
buildable repo.

## What's in the zip

| Path | What it is |
|---|---|
| `index.html` | **Start here.** Production-ready static page: plain HTML + inline CSS, ~15 lines of vanilla JS, no build step. Visually identical to the design. |
| `uploads/Resonant House Luxury Logo.png` | The logo used in the hero (1536×1024 PNG, 1.5 MB). |
| `uploads/a_clean_professional_brand_identity_logo_lockup_b.png` | Alternate logo lockup. **Not used on the page.** |
| `CLAUDE.md` | Working rules for Claude Code in this repo. |

Run locally: `python3 -m http.server 8000` → http://localhost:8000

## Differences between the design source and `index.html`

Everything visible is unchanged. Only these were done to make it standalone:
1. Removed the design-editor wrapper (`<x-dc>`, `<helmet>`, `support.js`).
2. Converted the custom `style-hover` / `style-focus` attributes into real `:hover` / `:focus` CSS rules (`.rh-sN` classes, `!important` because the base styles are inline).
3. Added `lang="en"`, a `<title>`, and a `<meta name="description">` (the source had none).
4. Kept the scroll-reveal (`IntersectionObserver` on `.fi`) and mailto form handler as plain JS.

## Page structure (section ids)

1. `#hero` — logo, italic promise line ("We help strong voices reach the readers, editors and stages they deserve."), CTA to `#contact`. Sticky nav above it (wordmark + "Start a Conversation").
2. `#services` — "Five ways we build a voice's reach." 5 articles in a 3-col grid (2-col ≤860px, 1-col ≤520px).
3. `#approach` — "Four things you can rely on." 2-col split, numbered 01–04 (stacks ≤820px).
4. `#current-work` — dark navy section: **The AI Trilogy** (three books, Book One December 2026).
5. `#press-kit` — "Press Materials" download card + descriptive copy.
6. `#contact` — "Start a conversation." + form (name, email, goal).
7. `<footer>` — wordmark, tagline "Where voices become influence.", anchor nav, email.

## Design tokens

| Token | Value | Use |
|---|---|---|
| Ivory | `#FAF6EE` | page background, text on dark |
| Ink | `#0D161D` | body text, buttons, borders (text at 0.55–0.72 alpha for secondary) |
| Gold | `#B08C58` | rules, eyebrow labels, numerals, focus ring |
| Navy | `#0A1825` | Current Work section background |
| Near-black | `#0E0E0D` | footer background |
| Display font | Cormorant Garamond 300/400/500 + italic 300/400 | headings, wordmark, pull quotes |
| UI/body font | Inter 300/400/500 | body, labels, buttons |
| Section padding | `clamp(80px,11vh,120px)` vertical, `clamp(20px,6vw,80px)` horizontal | all sections |
| Max content width | 1140px | |
| Eyebrow labels | 10px, `letter-spacing:.24em`, uppercase, preceded by a 36px gold rule | |
| Motif | Concentric gold quarter-arcs (inline SVG, low opacity) in hero (top-right), Current Work (bottom-left), footer (top-right) — echoes the logo | |
| Gold dividers | `linear-gradient(to right, transparent, #B08C58 20%, #B08C58 80%, transparent)`, 1px | between sections |
| Motion | `.fi` fade-up (0.9s, `cubic-bezier(0.22,1,0.36,1)`), triggered once at 10% visibility; hero uses 0.3s / 0.55s delays | |

## Open items — real content/config still needed

These are marked `⚠ PLACEHOLDER` in the HTML comments:

1. **Book website link** (`#current-work`): the "Visit the book website →" link is `href="#"`. Needs the real URL.
2. **Press kit** (`#press-kit`):
   - Heading reads literally `[Book One Title] — Press Kit` — needs the real title.
   - A visible italic note ("Placeholder — update the book title above and the download link below…") is rendered to visitors — **delete before launch**.
   - "Download Press Kit" is `href="#"` — needs the real file/URL (host the PDF/zip in the repo, e.g. `press/`, or a link).
   - Its `aria-label` says "(placeholder link)" — remove that suffix when the link is real.
3. **Email**: the site uses `theresonanthouse@gmail.com` as a stand-in. The contact section shows "Domain email coming soon." beneath it — swap to the domain address when ready and remove that line. The address appears in two `mailto:` links (contact section, footer) and once in the form handler's JS.
4. **Contact form** has no backend: submit just opens the visitor's mail client with a prefilled `mailto:`. Fine for launch; consider Formspree/Netlify Forms/a serverless function if they want real submissions. `novalidate` is set and there is no inline validation or success state.

## Suggested improvements (not done — confirm with owner first)

- **Logo file size**: hero PNG is 1.5 MB at 1536×1024 but displays at ≤340px wide. Export a ~700px-wide optimized PNG/WebP (and `srcset` for 2×); also add `width`/`height` attributes to avoid layout shift. Don't alter or recolor the logo itself.
- **Fonts**: currently loaded from Google Fonts. Self-hosting is an option for privacy/performance.
- **Tagline inconsistency**: nav says "Strategic Communications & PR", footer and logo alt say "…& Public Relations". Pick one.
- **Meta/social**: add `og:title`, `og:description`, `og:image`, favicon (derive from the logo's mark), canonical URL once the domain exists.
- **Accessibility**: the design already uses landmarks, labelled inputs, `focus-visible` ring, `aria-hidden` on decorative SVG. Still to check: low-alpha text contrast (e.g. `rgba(250,246,238,0.28)` footer small print, `rgba(13,22,29,0.38)` "Domain email coming soon", 9px labels) against WCAG AA, and `prefers-reduced-motion` (the `.fi` fade-up has no reduced-motion fallback; `.fi` starts at `opacity:0`, so without JS the content is hidden — add a `<noscript>` rule or default to visible).
- **Deployment**: pure static — Netlify, Vercel, Cloudflare Pages, GitHub Pages all work with the repo root as the publish directory.

## Content notes (don't change without owner sign-off)

Copy is deliberately precise: PR claims are modest and sourceable ("We make no claim we cannot source"; "You approve everything before it goes out"). Preserve tone and wording; British spelling ("labour") is intentional. The AI Trilogy is a client engagement — Resonant House leads media strategy, op-eds and speaking for Book One (December 2026).
