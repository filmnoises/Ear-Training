# Ear Trainer

A browser-based ear training app. Currently includes:
- **Level 1 · Intervals** — melodic and harmonic interval recognition
- **Level 2 · Triads** — major/minor triad recognition with inversions,
  blocked and arpeggiated playback

Built as a learning project. Single HTML file, no build step, no install.

## Running it

Open `ear-trainer.html` in any modern browser. Piano samples load from
a CDN on first launch (a few seconds). No server needed after caching.

## Project files

- `ear-trainer.html` — the app. Single file; HTML, CSS, and JS together.
- `CHANGELOG.md` — version history. Newest changes at the top.
- `NOTES.md` — working notes, ideas, things to come back to. Inbox, not plan.
- `TODO.md` — what's next, organized into Now / Next / Later.
- `TESTING.md` — manual checks to run after any change.
- `README.md` — this file.
- `Releases/` — archived versioned copies for testers.

## Project history

Originally named "Interval Trainer" when it covered only Level 1.
Renamed to "Ear Trainer" at v0.6.0 when Level 2 (Triads) was added,
reflecting the broader scope. The file `interval-trainer.html` became
`ear-trainer.html`. Prior versioned releases in `Releases/` retain
their original names.

## Tech

- [Tone.js](https://tonejs.github.io/) for audio — Sampler with Salamander
  Grand Piano samples from the Tone.js CDN.
- Vanilla HTML/CSS/JS. No framework, no build step.
- Typography: Fraunces (display) + JetBrains Mono (data), Google Fonts.
- Accessibility: WCAG AA contrast, semantic HTML, ARIA tab/toolbar/live
  patterns, full keyboard navigation, visible focus indicators,
  symbols-alongside-color feedback, prefers-reduced-motion support.
