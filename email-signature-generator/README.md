# Email Signature Generator

A local, single-file signature builder. No install, no server, no external
dependencies — everything (icons, uploaded logo) is embedded directly into
the generated HTML so the output never breaks due to a missing hosted image.

## Use

Open `index.html` in a browser. Fill in the form on the left; the preview
on the right updates live.

- **Copy signature** — copies the rendered signature (rich HTML) so you can
  paste it directly into Outlook's signature editor (Settings → Mail →
  Compose and reply → Signatures).
- **Copy HTML source** — copies the raw HTML, for email clients that accept
  pasted source or for embedding elsewhere.
- **Download .html** — saves a standalone signature file you can open in a
  browser and copy from there, which some Outlook builds handle more
  reliably than a direct app-to-Outlook paste.

Your inputs are saved to the browser's local storage automatically, so
they're still there next time you open the file.

## Why this exists

HubSpot's free signature generator produces good-looking output in its own
preview, but its HTML leans on CSS Outlook doesn't support — `border-radius`
circles and `linear-gradient` icon backgrounds — so signatures built there
can reflow once pasted into Outlook's signature box (Outlook renders
signatures with Word's HTML engine, not a browser engine).

This tool avoids those properties entirely:

- Layout is nested `<table>`s with explicit pixel widths, not flexbox/CSS
  grid.
- Dividers are 1px solid-color table cells (`bgcolor`), not CSS borders.
- Icons are plain raster PNGs (canvas-drawn, then embedded as base64),
  never SVG or CSS-drawn shapes — Word's engine doesn't render SVG at all.
- The call-to-action button is a bulletproof table-button, not a styled
  `<span>`/`<a>` with border-radius as its only shape.

## Customizing

- Accent color, font, and whether contact/social icons sit on a colored
  circle are all exposed in the **Style** section.
- Social links support LinkedIn, X, Bluesky, Instagram, Facebook, Threads,
  GitHub, or a custom platform (with your own badge letters or an uploaded
  icon image).
- Logo is uploaded from disk and embedded as base64 — no hosting required.

## Known limitations

- Icons are simple generated glyphs (drawn on canvas), not official brand
  logos — this sidesteps hosting/trademark concerns. Use the "custom icon"
  upload on a social row if you want an exact brand mark instead.
- Always do a final check by pasting into Outlook and sending yourself a
  test email — this tool eliminates the well-known CSS incompatibilities,
  but no browser preview is a perfect stand-in for Outlook's own renderer.
