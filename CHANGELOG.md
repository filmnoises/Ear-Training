# Changelog

All notable changes to the Ear Trainer (formerly Interval Trainer) are
documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- 7th chords (Level 4) — natural extension of Level 2 with one more
  inversion, four to five common qualities (maj7, min7, dom7, m7b5,
  optionally dim7)
- Then a deliberate pause for tester feedback before Part 2 (extensions:
  9th/11th/13th) and Part 3 (drop-2 voicings) — both deserve their own
  design conversations
- Save settings to localStorage so they persist across sessions
- Real-user testing with sight-impaired screen reader users
- Mobile-friendly layout review
- Reference manual (separate from getting-started guide)

---

## [0.7.2] — 2026-04-25

### Changed
- **Tritone label expanded in the Level 3 target picker** to read
  "Tritone (Aug4/Dim5)" instead of "TT". Helps singers connect the
  alternate names (augmented 4th, diminished 5th) they may know to
  the tritone label as they prepare to produce that pitch. The
  expanded label appears only in the Level 3 target picker; all
  other appearances of the tritone (Level 1 answer buttons, Level 1
  pool, Level 1 Reference panel) keep their concise labels.

### Notes
- Single surgical change in `l3_renderIntervalTargetPicker()` — added
  a special-case label for `iv.semitones === 6`, plus a tiny CSS rule
  (`.chip.l3-tritone { white-space: nowrap; }`) to prevent the longer
  label from breaking awkwardly mid-text.
- User manual is technically slightly out of date now (it describes
  Tritone consistently as "Tritone"). Worth updating when the manual
  next gets a refresh, but not urgent.

---

## [0.7.1] — 2026-04-24

### Added
- User manual (`USER-MANUAL.md` and `USER-MANUAL.pdf`) — getting-started
  guide for first-time users with light music theory context.

---

## [0.7.0] — 2026-04-24

### Added
- Diminished and augmented triads in Level 2 (off by default).
- Level 3: Sing-First practice mode with voice-range selector,
  adjustable wait timer, and Got It/Missed It self-rating.
- Third level tab and keyboard shortcuts (Space, T, G, M).

### Changed
- Stage indicator light gains a green "waiting" state for L3 countdown.

---

## [0.6.1] — 2026-04-23

### Changed
- Level 2 settings renamed/regrouped as "Triad Focus" with consistent
  "Chord quality" / "Chord inversion" labels.
- Triad Focus repositioned between score and Reference panel.
- All font sizes bumped up one point.

### Fixed
- Keyboard hint badge contrast on primary (brass) buttons.

---

## [0.6.0] — 2026-04-23

### Added
- Level 2: Triads (blocked/arpeggiated, major/minor, three inversions,
  two-axis answer UI with explicit Submit, partial credit feedback).
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
