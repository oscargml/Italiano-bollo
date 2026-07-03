# Bollo B2

A free, single-file web app for studying toward the **PLIDA B2** Italian
certification exam. Duolingo-style interactive practice, but scoped to what
the real exam actually tests: grammar, listening, reading, writing, and
speaking, plus a gamified progress dashboard.

## What it is

- **Grammatica** — 14 B2-level grammar topics (congiuntivo, periodo
  ipotetico, discorso indiretto, pronomi combinati, passivo, gerundio, usi
  del si, connettivi, congiunzioni concessive/finali, etc.), each with an
  explanation, a conjugation/usage table, example sentences, and a 5-question
  scored quiz.
- **Ascolto** — 5 listening exercises. Audio is generated on the fly with the
  browser's built-in `SpeechSynthesis` API (Italian voice), so there are no
  audio files to host. Falls back to a toggleable transcript.
- **Lettura** — 5 original reading passages (article, formal letter,
  argumentative text, blog post, official announcement) with comprehension
  questions.
- **Uso della lingua** — 4 cloze / transformation drills matching the exam's
  "elementi di competenza linguistica" format.
- **Scrittura** — 4 writing prompts (formal email, informal letter,
  argumentative text, complaint email) with a live word counter, a
  self-assessment rubric, and a model answer to compare against.
- **Parlato** — 4 speaking prompts with a timed prep/speak flow. If the
  browser supports `SpeechRecognition`, what the user says is transcribed
  live; otherwise it degrades gracefully to a plain timer.
- **Guida** — a long-form written guide to the exam structure, a 4-phase
  study plan, and common B2 mistakes (also the primary long-form content for
  AdSense crawler eligibility).
- **Progresso** — XP, a daily streak counter/calendar, per-skill completion
  breakdown, and a "timbro" (stamp) collection, all stored in the browser's
  `localStorage`. No backend, no accounts — progress is per-device.

All lesson/exercise content is original, written to match the *format* and
typical *topics* of the PLIDA B2 exam. No official PLIDA past-paper material
is reproduced anywhere (that content is copyrighted by the Società Dante
Alighieri).

## Tech stack

- Single `index.html` file — vanilla HTML/CSS/JS, no build step, no
  framework, no dependencies.
- Fonts loaded from Google Fonts CDN (Fraunces, Inter, IBM Plex Mono).
- `SpeechSynthesis` (listening) and `SpeechRecognition` (speaking) are native
  browser Web APIs — no external API calls, no cost.
- Progress persistence via `localStorage` only.

## File layout

```
index.html          the entire site
favicon.svg          generated favicon
apple-touch-icon.png  generated touch icon
og-image.png          generated 1200x630 social share image
logo.png               generated square logo
sitemap.xml            single canonical URL
robots.txt              points at sitemap.xml
vercel.json             static routing + cache headers for Vercel
```

## Local development

No build step. Just serve the folder:

```bash
python -m http.server 8000
# open http://localhost:8000
```

## Deploying

Drag-and-drop the folder onto Netlify, or push to a repo connected to Vercel.
`vercel.json` is already set up for static hosting with `cleanUrls` and
sensible cache headers on the generated image assets.

## Monetization & SEO — what's wired, what you still need to do

**Wired with your real AdSense client (`ca-pub-8643026289824701`):**
- The AdSense loader script in `<head>`
- Three in-page ad units (`<ins class="adsbygoogle">`): after the exam
  structure overview on the home page, mid-article in the Guida section, and
  near the page footer

**Still placeholder — you need to fill these in:**
- `REPLACE_WITH_SLOT_ID_1` / `_2` / `_3` — the three AdSense unit slot IDs.
  Create them in your AdSense dashboard (Ads → By ad unit), or just enable
  **Auto Ads** site-wide and delete the three manual `<ins>` blocks — Auto Ads
  only needs the loader script that's already in place.
- `G-XXXXXXXXXX` (three occurrences) — your real Google Analytics Measurement
  ID, if you want analytics. Delete the whole `gtag` block if you don't.
- `REPLACE_WITH_GSC_TOKEN` — your Google Search Console verification meta
  content, once you add the property.
- `REPLACE_WITH_USERNAME` — your Buy Me a Coffee username, in the footer
  donation link (or delete the link if you don't want a donation ask).
- The canonical/OG URLs are set to `https://www.bollob2.com/` as a
  placeholder domain — swap to your real domain everywhere (`<link
  rel="canonical">`, `og:url`, `og:image`, `twitter:image`, `sitemap.xml`).

**Already in place:**
- Full meta tag set: title, description, keywords, robots, canonical
- Open Graph + Twitter Card, pointing at the generated `og-image.png`
- JSON-LD `WebApplication` schema
- JSON-LD `FAQPage` schema, matching the visible FAQ in the Guida section
  word-for-word (required for rich-result eligibility)
- `sitemap.xml` with a single real canonical URL (no `#fragment` noise) and
  `robots.txt` pointing at it
- Generated favicon, apple-touch-icon, and a real 1200×630 PNG `og-image.png`
  (social scrapers want a raster image, not the SVG favicon)

## Content model (for future edits)

All lesson content lives in plain JS data arrays near the top of the
`<script>` block: `grammarTopics`, `listeningExercises`, `readingPassages`,
`usoExercises`, `writingPrompts`, `speakingPrompts`. Adding a new grammar
topic, listening script, or writing prompt is just appending an object to the
relevant array in the same shape as its neighbors — the render functions
(`renderGrammarGrid`, `openGrammarLesson`, etc.) pick up new entries
automatically.
