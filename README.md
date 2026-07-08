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
- **Smart extras** — daily poem/greeting, per-day nutrition & calorie estimate, emoji lookup for the sticker creator — powered by Claude when hosted there, or by free public APIs when self-hosted (see below)
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

## 🌐 Smart features when self-hosted

When the app detects it is NOT running in a Claude-hosted environment, it automatically switches to free public APIs:

| Feature | Provider | Key needed? |
|---|---|---|
| ✨ Generate sticker (text → emoji + category) | [emoji.family](https://www.emoji.family/developers) (primary), [emoji-api.com](https://emoji-api.com) (optional fallback) | No key for emoji.family; emoji-api.com key optional |
| 🥗 Nutrition estimate | [calorieapi.com](https://calorieapi.com) (preferred), falling back to [USDA FoodData Central](https://fdc.nal.usda.gov/api-guide) | Calorie API key ships pre-filled (replaceable in **Export → Online AI**); USDA works with `DEMO_KEY` |
| ☀️ Daily greeting | [beanpoems.com](https://www.beanpoems.com/api/) — random poem of the day | No |

Keys are entered in-app (Export dialog → "Online AI") and stored only in the user's browser. If a service is unreachable, the feature falls back gracefully (default greeting, friendly error).

Note: USDA figures are per-100 g servings of the closest matching food — a rough estimate, not the Claude-grade contextual one.

## ⚠️ Limitations

- **Storage is per-browser** (localStorage). No accounts, no sync. Users are nudged in-app to download JSON backups; restore works on any device.
- Data cap: localStorage (~5 MB). Uploaded sticker images are downscaled to 96px, avatars to 128px, to stay small.
- Nutrition/emoji APIs require internet; everything else works fully offline.

## 🔒 Privacy

All data stays on the user's device. The only network calls are the optional smart features, which send just the search text or the day's food names (never notes, dates tied to identity, or images).
