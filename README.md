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


