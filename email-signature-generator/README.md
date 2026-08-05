# Email Signature Generator

A local, single-file signature builder. No install, no server. Uploaded
photos/logos are embedded directly into the generated HTML as base64. The
phone/email/website/address icons and the LinkedIn/X/Bluesky badges are
hotlinked from HubSpot's own icon CDN (and Bluesky's brand asset URL) by
choice, so those depend on those hosts staying reachable — everything else
(profile photo, logo, any custom social icon you upload) has no such
dependency.

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
- Anything that must sit side-by-side (social icons) is laid out as table
  cells, not `<div>`/inline-block — Word's renderer doesn't reliably keep
  inline-block elements from stacking.
- Icon "background" colors are plain `background-color` on a table cell,
  not `linear-gradient`.
- The call-to-action button is a bulletproof table-button, not a styled
  `<span>`/`<a>` with border-radius as its only shape.

## Customizing

- Accent color, font, and whether contact/social icons sit on a colored
  circle (square if unchecked, for contact icons) are all exposed in the
  **Style** section.
- Social links support LinkedIn, X, Bluesky, Instagram, Facebook, Threads,
  GitHub, or a custom platform. LinkedIn/X/Bluesky use HubSpot's/Bluesky's
  real icon; any row can override its icon with a custom URL or upload,
  which also covers Instagram/Facebook/Threads/GitHub/custom (otherwise a
  generated letter badge).
- Profile photo and company logo each take a hosted URL or a local upload.

## Known limitations

- The phone/email/website/address icons and default LinkedIn/X/Bluesky
  badges are hotlinked, not embedded — if HubSpot's CDN or Bluesky's asset
  URL ever goes away, those specific icons would break. Override any of
  them with a custom icon URL/upload if that's ever a concern.
- Always do a final check by pasting into Outlook and sending yourself a
  test email — this tool eliminates the well-known CSS incompatibilities,
  but no browser preview is a perfect stand-in for Outlook's own renderer.
