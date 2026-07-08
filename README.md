# My Daily Log 📔

A playful, mobile-first visual life tracker: log food, drinks, exercise, and daily habits by placing **stickers on a calendar** instead of typing.

![status](https://img.shields.io/badge/status-MVP-brightgreen) ![license](https://img.shields.io/badge/license-TBD-lightgrey)

## ✨ Features

- **Month / Week / Day views** — scrapbook-style sticker piles, "+N" overflow badges, today highlight
- **Drag & drop logging** — mouse drag on desktop, **long-press drag** or tap-to-add on mobile
- **Day peek popover** — click any day to see, remove, or annotate its stickers
- **Meal lanes** — food/drinks auto-sort into Breakfast / Lunch / Snack / Dinner (editable)
- **30+ default stickers** in 5 categories, all editable/hideable
- **Custom sticker creator** — pick an emoji, upload an image, or use a text name-tag; optional **AI generate** from a description
- **AI extras** — daily cheerful greeting, per-day nutrition & calorie estimate *(only in Claude-hosted environments — see Limitations)*
- **Day notes** — freeform "note to self" per day (✏️ marker on the calendar)
- **Sounds & delight** — pop/squish sound effects (mutable), drop animation, confetti at 3+ stickers/day
- **Data safety** — CSV export (all or date range, includes day notes), full **JSON backup/restore**, automatic backup reminders
- **Tweakable theme** — accent color, week start day, sticker size

## 🚀 Deploy

`index.html` is fully self-contained (fonts, scripts, and assets inlined). No build step, no server logic.

**GitHub Pages:**
1. Push this folder to a repo
2. Settings → Pages → Deploy from branch → root
3. Open `https://<user>.github.io/<repo>/`

Any static host (Netlify, Vercel, S3) works the same way.

## 📦 Contents

| File | Purpose |
|---|---|
| `index.html` | The app — single self-contained file, deploy as-is |
| `PRD.md` | Product requirements document |
| `ROADMAP.md` | Product roadmap |
| `src/My Daily Log v2.dc.html` | Design-component source (edit in the original design environment, then re-bundle) |

## ⚠️ Limitations

- **Storage is per-browser** (localStorage). No accounts, no sync. Users are nudged in-app to download JSON backups; restore works on any device.
- **AI features degrade gracefully outside Claude-hosted environments**: sticker auto-generate and nutrition estimates show a friendly error; the daily greeting falls back to a default line. Everything else works fully offline.
- Data cap: localStorage (~5 MB). Uploaded sticker images are downscaled to 96px, avatars to 128px, to stay small.

## 🔒 Privacy

All data stays on the user's device. Nothing is sent anywhere except the optional AI calls (sticker text / day's food names only).
