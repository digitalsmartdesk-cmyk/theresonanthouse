# Resonant House website

Static one-page site. Source of truth: `index.html` (plain HTML, inline CSS, small vanilla JS). No framework, no build step, no dependencies — keep it that way unless asked.

- Read `HANDOFF.md` first (structure, design tokens, open placeholder items).
- The original Claude Design export (`design-source/`) was removed from the repo; the page is hosted straight from the repo root.
- Preview: `python3 -m http.server 8000`.
- Check responsive layout at 1280px, 820px, 520px and 375px widths after any layout change (breakpoints: 860 / 820 / 560 / 520).
- Use only the design tokens in `HANDOFF.md` (ivory `#FAF6EE`, ink `#0D161D`, gold `#B08C58`, navy `#0A1825`, Cormorant Garamond + Inter). Do not introduce new colors or fonts.
- Do not modify, recolor or re-crop the logo PNGs; optimized derivatives go next to them with a new filename.
- Preserve existing copy exactly (British spelling, measured tone). Flag any copy change as a suggestion instead of making it.
- Resolve the `⚠ PLACEHOLDER` items in `HANDOFF.md` only with real values from the owner — never invent URLs, titles or emails.
- Keep accessibility intact: real `<a>`/`<button>`, labelled inputs, visible focus ring, `aria-hidden` on decorative SVG.
