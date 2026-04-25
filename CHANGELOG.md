# Changelog

All notable changes to the Ear Trainer (formerly Interval Trainer) are
documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- Seventh chords (Level 4?)
- Drop-2 voicings
- Rhythm training
- Sight-reading trainer (VexFlow library)
- Per-interval / per-quality score tracking
- Save settings to localStorage so they persist across sessions
- Real-user testing with sight-impaired screen reader users
- Mobile-friendly layout review
- Reference manual (separate from getting-started guide)

---

## [0.7.1] — 2026-04-24

### Added
- **User manual**: a getting-started guide for first-time users.
  Covers all three levels with light music theory context for users
  new to formal theory (intervals, triads, inversions explained with
  evocative musical examples). Available as:
  - `USER-MANUAL.md` — Markdown source, the editable working version
  - `USER-MANUAL.pdf` — polished PDF for distribution to testers,
    11 pages, generated via reportlab with serif typography matching
    the app's calm/literary aesthetic
- Manual includes sections on: quick start, three-levels overview,
  music theory primer, per-level practice loops with settings
  explained, tips for effective practice, full keyboard shortcut
  reference, and an explicit accessibility features section.

### Notes
- No app code changes in this release. The HTML file is unchanged
  from v0.7.0.
- The Markdown source is the canonical version. PDF should be
  regenerated when the manual changes (build script: build_manual_pdf.py
  if kept in the project for reference).

---

## [0.7.0] — 2026-04-24

### Added
- **Diminished and augmented triads** in Level 2 (off by default).
- **Level 3: Sing-First practice mode** — pick a target, hear root,
  sing the interval/triad, then verify. Voice-range selector
  (Bass/Tenor/Alto/Soprano), adjustable wait timer (1–15s),
  continuous practice toggle, "Got It / Missed It" self-rating.
  Both intervals and triads supported.
- Third level tab and keyboard shortcuts for Level 3 (Space, T, G, M).

### Changed
- Stage indicator light gains a green "waiting" state for L3 countdown.

---

## [0.6.1] — 2026-04-23

### Changed
- Level 2 settings renamed/regrouped as "Triad Focus" with consistent
  "Chord quality" / "Chord inversion" labels in both settings and quiz.
- Triad Focus repositioned between score and Reference panel.
- All font sizes bumped up one point.

### Fixed
- Keyboard hint badge contrast on primary (brass) buttons.

---

## [0.6.0] — 2026-04-23

### Added
- **Level 2: Triads** — blocked/arpeggiated, major/minor, three
  inversions, two-axis answer UI with explicit Submit, partial credit.
- Level 1 / Level 2 tab structure.
- Separate scores per level.

### Changed
- Renamed project from "Interval Trainer" to "Ear Trainer."
- Refactored state into `state.l1` and `state.l2` sub-objects.

---

## [0.5.0] — 2026-04-20

### Added
- Reference panel: root note selector and adjustable spacing slider.

### Changed
- Refactored to share `playSequence(q)` with a `gap` parameter.

---

## [0.4.0] — 2026-04-20

### Changed
- Direction controls moved below mode tabs as an ARIA toolbar.

### Added — accessibility baseline
- Semantic HTML, ARIA patterns, keyboard shortcuts, focus indicators,
  ✓/✕ symbols, skip link, prefers-reduced-motion, contrast bumps.

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
