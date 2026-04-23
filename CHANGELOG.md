# Changelog

All notable changes to the Ear Trainer (formerly Interval Trainer) are
documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- Add diminished and augmented triads to Level 2 quality pool
- Sing-first practice mode (hear root, sing interval/triad, verify)
- Seventh chords (Level 3)
- Rhythm training
- Sight-reading trainer (VexFlow)

---

## [0.6.1] — 2026-04-23

### Changed
- **Level 2 settings renamed and regrouped as "Triad Focus."**
  The settings section now has a clear top-level heading ("Triad Focus")
  with a short description of what it does. Subheadings updated from
  "Quality pool" → "Chord quality" and "Inversion pool" → "Chord inversion."
- **Quiz answer labels updated to match:** "Quality" → "Chord Quality"
  and "Inversion" → "Chord Inversion" on the Level 2 answer rows.
  Consistency between settings and quiz labels throughout.
- **Triad Focus panel repositioned** between the score and the Reference
  panel (previously was at the bottom of the page). Accessible from a
  natural reading position after answering a question.
- **All font sizes bumped up one point** for readability. H1 header,
  tab labels, button text, answer buttons, feedback, panel headings,
  chips — everything is slightly larger. Helps anyone with mild visual
  fatigue or small-screen viewing.

### Fixed
- **Keyboard hint badge contrast on primary buttons.** The small "Space"
  and "Enter" badges on the brass-colored Play and Submit buttons were
  nearly unreadable (low-contrast dim text on bright background). They
  now use a near-black color on brass backgrounds. The R and S badges
  on transparent-background buttons are unchanged (still readable there).

### Technical notes
- Added `--ink-on-brass` CSS variable for high-contrast text on
  brass-colored surfaces. Used via `.btn-primary .kbd` and
  `.btn-submit .kbd` selectors.
- No logic changes in this release; purely cosmetic/UX polish.

---

## [0.6.0] — 2026-04-23

### Added
- **Level 2: Triads** — new training level for major and minor triads
  with all three inversions.
  - Blocked mode: three notes simultaneously.
  - Arpeggiated mode: notes in sequence, with direction toolbar.
  - Two-axis answer UI (Quality row + Inversion row) with explicit
    Submit button and Clear Picks affordance.
  - Partial-credit feedback distinguishes "quality right, inversion wrong"
    from "both wrong."
  - Keyboard shortcut: Enter submits.
  - Level 2 Reference panel with per-combination buttons.
- **Level 1 / Level 2 tab structure** at top of app.
- **Separate scores per level.**

### Changed
- **Renamed project from "Interval Trainer" to "Ear Trainer."**
  File renamed from `interval-trainer.html` to `ear-trainer.html`.
- Refactored state into `state.l1` and `state.l2` sub-objects.

---

## [0.5.0] — 2026-04-20

### Added
- Reference panel: root note selector (Random/Fixed with chromatic chooser).
- Reference panel: adjustable melodic spacing slider.

### Changed
- Refactored `playQuestion`/`playIntervalOnDemand` to share
  `playSequence(q)` with a `gap` parameter.

---

## [0.4.0] — 2026-04-20

### Changed
- Direction controls moved below mode tabs as an ARIA toolbar.

### Added — accessibility baseline
- Semantic HTML, ARIA tab/toolbar/live-region patterns, keyboard
  shortcuts, focus indicators, ✓/✕ symbols, skip-to-main-content link,
  prefers-reduced-motion support, contrast bumps.

---

## [0.3.0] — 2026-04-19

### Added
- Reference panel.

### Fixed
- Stale-question bug when pool/direction/mode changed mid-question.

---

## [0.2.0] — 2026-04-19

### Added
- Harmonic mode, auto-advance on correct, Repeat Last button.

---

## [0.1.0] — 2026-04-19

### Added
- Initial working version: melodic interval trainer with sampled piano.
