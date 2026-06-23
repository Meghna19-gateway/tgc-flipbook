# Handover — The Gateway Chronicles Digital Flipbook

A self-contained, Heyzine-style page-flip flipbook built from the anniversary PDF.
This document explains how to **publish it**, **update it**, and **rebuild it** from
another machine.

---

## 0. Current status

- The finished flipbook lives in this folder (`flipbook-site/` in the handover ZIP,
  or `TGC-flipbook-FINAL/` in the original project).
- It is **already a local git repository with one commit** — ready to push.
- It is **not yet published**. Remaining work = create a GitHub repo, push, enable Pages.

---

## 1. What's in this folder

| File / folder | Purpose |
|---|---|
| `index.html` | The flipbook (entry page for GitHub Pages). Self-contained: engine, page-turn sound, and logo are all embedded. |
| `flipbook.html` | Identical copy — the "template" name used during development. |
| `pages/` | The page images (`page-001.jpg` … `page-037.jpg`). **This is the content.** |
| `.nojekyll` | Tells GitHub Pages to serve files as-is (no Jekyll processing). |
| `README.md` / `README.txt` | Short usage notes. |
| `.git/` | The committed repository (so you can push without re-committing). |

---

## 2. PUBLISH to GitHub Pages  (main task)

**You need:** a GitHub account, and either Git or GitHub Desktop installed.

### Option A — Git command line
1. Copy this whole folder to the new machine.
2. Create a **public** repo at <https://github.com/new> (e.g. `gateway-chronicles`).
   Do **not** add a README/license there.
3. In a terminal, inside this folder:
   ```bash
   git remote add origin https://github.com/<username>/<repo>.git
   git push -u origin main
   ```
   - Authentication: GitHub no longer accepts your account password here. Use a
     **Personal Access Token** as the password
     (<https://github.com/settings/tokens> → "Generate new token (classic)" → tick
     `repo`), or use GitHub Desktop (Option B).
4. In the repo on GitHub: **Settings → Pages → Source: "Deploy from a branch" →
   Branch: `main` / `/(root)` → Save.**
5. After ~1 minute the public link is:
   ```
   https://<username>.github.io/<repo>/
   ```

### Option B — GitHub Desktop (no command line)
1. Install GitHub Desktop and sign in.
2. **File → Add local repository →** select this folder.
3. Click **Publish repository** (uncheck "Keep this code private" for free Pages).
4. Then enable Pages as in step 4 above.

> Free GitHub Pages requires a **public** repo, so the page images become publicly
> viewable and search-indexable. If this should stay internal, host it on a company
> server/intranet instead (just serve `index.html` + `pages/`).

---

## 3. UPDATE the pages later

1. Replace / add images in `pages/`, named sequentially: `page-001.jpg`,
   `page-002.jpg`, …  (formats: `.jpg .jpeg .png .webp`; same width:height ratio).
2. Commit and push:
   ```bash
   git add -A
   git commit -m "Update pages"
   git push
   ```
3. GitHub Pages redeploys automatically in ~1 minute. No HTML editing needed —
   the flipbook auto-detects the page count and adjusts pagination/centering.

---

## 4. REBUILD from a new PDF  (optional — only if regenerating from scratch)

Tools are in the `rebuild-tools/` folder of the handover ZIP.

**You need:** Python 3 and these packages:
```bash
pip install pymupdf fpdf2 pillow
```

1. **Render the PDF to page images** (150 DPI JPEGs):
   ```python
   import fitz
   doc = fitz.open("your.pdf")
   mat = fitz.Matrix(2.0, 2.0)
   for i, page in enumerate(doc):
       page.get_pixmap(matrix=mat, alpha=False).save(f"pages/page-{i+1:03d}.jpg", jpg_quality=82)
   ```
   Put the output in a folder `TGC-flipbook/pages/`.
2. Ensure these sit beside `build_template.py`:
   - `TGC-flipbook/lib/page-flip.browser.js`  (the flip engine — included)
   - `TGC-flipbook/pages/…`                    (rendered above)
   - `Gateway Group_Transparent White_Logo.png` (included)
3. Build the final single-file flipbook (with center spine shadow + logo):
   ```bash
   python build_template.py final
   ```
   This writes `TGC-flipbook-FINAL/flipbook.html` + copies the pages.
4. Copy `flipbook.html` → `index.html` and publish as in section 2.

Build flags: `python build_template.py` (no shadow) · `... v2` / `... final`
(center spine shadow).

---

## 5. Quick facts

- **Fully offline / self-contained:** `index.html` embeds the flip engine, the
  page-turn sound, and the logo. Only the `pages/` images are external (so they're
  swappable without touching the HTML).
- **Features:** centered cover → 2-page spreads → no trailing blank on even counts,
  page-turn sound (toggle), zoom, thumbnails, fullscreen, keyboard arrows,
  bottom-left Gateway logo, subtle center spine shadow.
- **Hosting note:** any static host works (GitHub Pages, Netlify, an internal web
  server). Just serve `index.html` with the `pages/` folder alongside it.
