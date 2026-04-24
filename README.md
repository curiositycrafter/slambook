# The Slam Book

A personal, interactive slam book built as a single HTML file. Friends fill out a curated set of questions about you — first impressions, memories, opinions, secret thoughts — and their answers are saved to Firebase Firestore (with a localStorage fallback).

## Features

- **Custom pen cursor** with animated ink trails, splats, and dots
- **Personalised question set** — each visitor gets a randomly shuffled mix of questions drawn from a larger bank, so no two entries are identical
- **Three question modes**
  - *Normal* — general questions about you, memories, opinions
  - *Classified* (secret) — dark-card questions shown without the respondent's name attached
  - *Confidential* — a final, fully off-the-record freeform field
- **Three input types** — long-form text, multiple-choice buttons, and 1–10 slider scales
- **Progress bar** that tracks how far through the questions the visitor is
- **Animated page transitions** — ink-wipe effect between every screen
- **Firebase Firestore** storage with automatic localStorage fallback when offline or unconfigured
- **Saving toast** notification while the entry is being written to the database
- **Responsive layout** that works on mobile and desktop

## Tech Stack

| Layer | Detail |
|---|---|
| Markup & styles | Plain HTML + CSS (no build step) |
| Logic | Vanilla JavaScript (ES modules for Firebase) |
| Fonts | Google Fonts — Reenie Beanie, Fraunces, DM Mono |
| Database | Firebase Firestore v10 (CDN) |
| Fallback storage | `localStorage` |

## How It Works

1. **Cover page** — decorative landing screen; click *→ open it* to enter.
2. **Name page** — visitor enters their name (minimum 2 characters).
3. **Questions** — 11 questions are shown one at a time:
   - 8 randomly picked normal questions
   - 2 randomly picked secret/classified questions (inserted in the middle)
   - 1 fixed "last page" closing question
   - 1 fixed confidential freeform field (always last)
4. **Done page** — a "SEALED" stamp confirms the entry was saved.

## Project Structure

```
slambook/
└── index.html   # entire app — HTML, CSS, and JS in one file
```

## Customisation

Everything lives in `index.html`, making changes straightforward:

- **Questions** — edit the `qBank` array (~line 603). Each entry takes `id`, `tag`, `type` (`"text"` | `"choice"` | `"scale"`), `q` (question text), `hint`, and optional `choices` / `min` / `max` fields. Set `secret: true` for classified questions or `confidential: true` for the off-the-record slot.
- **Question count** — change the `.slice(0, 8)` and `.slice(0, 2)` calls in `buildQuestions()` (~line 649).
- **Colour palette** — update the CSS custom properties in `:root` (~line 11).
- **Nudge messages** — edit `shortNudges` and `emptyNudges` (~line 581) for the validation prompts shown when an answer is too short or empty.
- **Done-page jokes** — edit the `jokes` array (~line 795).
