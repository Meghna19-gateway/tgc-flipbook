GATEWAY CHRONICLES — SINGLE-FILE FLIPBOOK TEMPLATE
===================================================

WHAT'S HERE
  flipbook.html   ← the whole flipbook in ONE file (page-flip engine + UI +
                    page-turn sound are all built in; nothing else to load).
  pages/          ← the page images the flipbook displays.

HOW TO VIEW
  Double-click flipbook.html (opens in your browser). That's it.
  Or upload the whole folder to any web host for a shareable link.

HOW TO UPDATE THE PAGES  (no rebuild, no re-rendering)
  1. Export your new/edited pages as images.
  2. Name them in order:  page-001, page-002, page-003, ...
     - Zero-padded "page-001.jpg" or plain "page-1.jpg" both work.
     - Formats: .jpg  .jpeg  .png  .webp
  3. Drop them into the  pages/  folder (replace or add).
  4. Refresh flipbook.html. The new pages appear automatically.

  • Pages must be sequential starting at 1. The flipbook loads page-001,
    page-002, ... and stops at the first missing number.
  • Keep every page the same width:height ratio for a clean spread
    (the book sizing is taken from page-001).
  • First image = the cover (shown alone); the rest open as 2-page spreads.

OPTIONAL SETTINGS
  Open flipbook.html in a text editor and find the CONFIG block near the
  bottom to change the title, the pages folder name, or turn the default
  sound on/off. Everything else is automatic.

CONTROLS
  ← →  turn pages   ·   drag a page corner   ·   click page edge
  toolbar: first / prev / next / last · zoom · sound · thumbnails · fullscreen
