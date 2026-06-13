# PDI Snag Tracker — Flat H-802

Mobile-first web app to track 91 pre-delivery inspection findings from the GW Home Inspection report.

## Quick Deploy to GitHub Pages

```bash
# 1. Create a repo
gh repo create pdi-snag-tracker --public --clone
cd pdi-snag-tracker

# 2. Copy all files from this zip into the repo root
#    (index.html, manifest.json, images/)

# 3. Push
git add .
git commit -m "PDI Snag Tracker"
git push

# 4. Enable GitHub Pages
#    Go to Settings > Pages > Source: Deploy from branch > main > / (root)
#    Your site will be live at https://<username>.github.io/pdi-snag-tracker/
```

## Features

- **Dashboard** — progress ring, status/severity breakdown, top rooms
- **List** — search, filter by status/severity/component
- **Rooms** — 11 room cards with per-room progress
- **Detail view** — inspection photo, editable status/severity/remedy/dates
- **Photo capture** — add your own photos (camera or upload) per snag
- **Notes log** — timestamped append-only notes
- **Export** — copy-paste summary for WhatsApp/email
- **Offline** — runs entirely in the browser, no server needed

## Storage

- Snag data → `localStorage`
- User photos → `IndexedDB` (handles larger binary data)
- No server, no login, no network required after initial load

## File Structure

```
├── index.html          # The entire app (single file)
├── manifest.json       # PWA manifest
├── README.md
└── images/
    ├── snag-01.jpg     # Inspection photos (91 files, ~1.3MB total)
    ├── snag-02.jpg
    └── ...
```
