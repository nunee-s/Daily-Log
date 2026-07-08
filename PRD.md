# PRD — My Daily Log

| | |
|---|---|
| **Status** | MVP shipped |
| **Owner** | TBD |
| **Last updated** | 2026-07-08 |

## 1. Problem

Habit and food trackers demand typing, menus, and numbers. Most people abandon them within weeks. Logging should take **under 3 seconds** and feel rewarding, not like data entry.

## 2. Solution

A visual daily journal where users **place cute stickers on a calendar** to record what they ate, drank, did, and felt. Zero typing required; notes and quantities are optional. Cheerful feedback (sounds, animation, confetti, a daily greeting) makes logging itself the reward.

## 3. Audience

- Primary: individuals tracking daily habits casually (food, exercise, health, mood), mobile-first
- Secondary: friends & family sharing the habit informally
- Gender-neutral tone and palette by design

## 4. Goals & success metrics

| Goal | Metric | Target |
|---|---|---|
| Effortless logging | Time from open → sticker placed | < 3 s |
| Habit formation | Days/week with ≥1 sticker | ≥ 5 |
| Retention of delight | Confetti moments (3+ stickers/day) | ≥ 3/week |
| Data safety | Users with ≥1 backup within 30 days | ≥ 60 % |

## 5. Functional requirements

### 5.1 Calendar (P0)
- Month / Week / Day views; today highlighted; prev/next + Today navigation
- Month cells show sticker piles (overlapping, scrapbook style) with `+N` overflow
- Click a day → **peek popover** (stickers, remove ✕, day note, open day)
- Double-click → Day view; Day view has back button to previous view
- Day view groups food/drinks into Breakfast / Lunch / Snack / Dinner lanes (auto-guessed by log time, editable per entry)

### 5.2 Logging (P0)
- Desktop: HTML5 drag & drop from palette to any day
- Mobile: tap-to-add to selected day AND long-press (350 ms) drag with floating ghost + haptic
- Multiple copies of the same sticker per day; quantity stepper and free-text note per entry
- Remove: detail modal, peek ✕, or right-click in month view

### 5.3 Stickers (P0)
- 30+ defaults across Food / Drinks / Exercise / Health / Other
- All stickers editable (name, emoji, image, category); defaults hideable
- Custom creator: emoji OR uploaded image (auto-cropped 96px) OR text name-tag
- AI generate (P1): description → emoji + name + category

### 5.4 Notes (P0)
- Per-day "note to self" (≤500 chars) editable from peek popover and Day view; ✏️ indicator on month cells

### 5.5 Data (P0)
- Persistence: localStorage, versioned key (`sll-data-v1`)
- CSV export: columns `date, category, sticker_name, quantity, note`; all data or date range; day notes exported as `day_note` rows; UTF-8 BOM; clipboard fallback if download is blocked
- JSON backup (full state incl. custom stickers, notes, avatar) + restore with confirmation
- Backup nudge: shown at ≥10 entries and ≥14 days since last backup; snooze 7 days

### 5.6 AI features (P1 — Claude-hosted environments only, graceful fallback elsewhere)
- Daily greeting line (cached per day)
- Sticker auto-generation from text
- Per-day nutrition estimate (kcal, protein, carbs, fat + summary), cached per day-signature

### 5.7 Personalization (P1)
- Avatar logo (photo upload, 128px, stored locally; 👤 default)
- Tweaks: accent color, week start (Sun/Mon), month sticker size
- Sound effects (pop on place, squish on delete, ta-da + confetti at 3rd sticker of a day) with persistent mute

## 6. Design principles

- **2026 visual language**: Cloud Dancer near-white base, ambient layered gradients, liquid-glass panels, elevated warm neutrals, clay primary / teal support
- **Handwritten warmth**: Caveat for labels and hints; Baloo 2 brand; Quicksand body
- **Die-cut stickers**: white-outline circles, slight rotations, pile overlap
- **Accessibility**: muted text ≥ ~4.5:1 contrast; touch targets ≥ 44px; non-color cues (✏️, badges)

## 7. Non-goals (MVP)

- Accounts, cloud sync, multi-device merge
- Social feeds / sharing images
- Reminders & push notifications
- Native apps

## 8. Risks

| Risk | Mitigation |
|---|---|
| localStorage cleared → data loss | Backup/restore + automatic nudge |
| AI unavailable in some hosts | All AI paths fail silently to manual flows |
| Emoji rendering varies by OS | Emoji are user-visible content only; no layout dependence |
| ~5 MB storage cap | Images downscaled aggressively |
