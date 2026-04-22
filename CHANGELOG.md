# Changelog

All notable changes to the Interval Trainer are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- Decide whether quiz auto-advance delay should be user-adjustable
- Sing-first practice mode: user hears root, sings the target interval,
  then plays the actual interval to self-check (its own mode/tab)
- Triads and inversions module
- Drop-2 voicings module
- Sight-reading trainer (using VexFlow)

---

## [0.5.0] — 2026-04-20

### Added
- **Reference panel: root note selector.** New "Random / Fixed" toggle
  above the interval grid. When Fixed is selected, a chromatic chooser
  (C through B) appears. The chosen root applies to all reference button
  clicks until changed. Default behavior unchanged (Random).
- **Reference panel: adjustable melodic spacing.** New slider sets the
  delay between the two notes in melodic Reference playback, from 0.4s
  to 4s. Default 1.5s — slow enough to sing the interval before the
  second note plays. Quiz still uses fixed 0.6s for snappier testing.
  Slider is automatically disabled in harmonic mode (spacing has no
  meaning when notes play together).

### Changed
- Refactored `playQuestion` and `playIntervalOnDemand` to share a single
  underlying `playSequence` that takes a `gap` parameter. Quiz passes
  0.6, Reference passes the slider value. One playback path, two callers.
- Reference root chooser uses `role="radio"` semantics (only one root
  active at a time) rather than toggle-button semantics, while reusing
  the chip styling. Screen readers announce it as a radio group.

---

## [0.4.0] — 2026-04-20

### Changed
- **Direction controls moved up** directly below the mode tabs as a
  proper ARIA toolbar. Previously buried at the bottom of settings.

### Added — accessibility baseline
- Semantic HTML throughout: real `<button>` elements, `<main>` and
  `<section>` landmarks.
- Proper ARIA tab pattern (Melodic/Harmonic) with arrow-key navigation.
- `aria-pressed` on toggle buttons; `aria-live` on feedback region.
- Keyboard shortcuts: Space / R / S / 1-9. Visible on the buttons.
- Visible focus indicators (`:focus-visible` brass outline).
- ✓ / ✕ symbols alongside color on right/wrong feedback.
- Skip-to-main-content link (visible on focus).
- `prefers-reduced-motion` support.
- Bumped `--ink-dim` and accent colors for WCAG AA contrast.

---

## [0.3.0] — 2026-04-19

### Added
- Reference panel: click any of 12 intervals to hear it on a random root.
- Brass-colored flash on reference buttons.

### Fixed
- Stale-question bug: pool/direction/mode changes now invalidate any
  pending question via new `invalidateCurrent()` helper.

---

## [0.2.0] — 2026-04-19

### Added
- Harmonic mode (notes played simultaneously).
- Auto-advance on correct answers (1.2s).
- Repeat Last button.
- Mode-aware header subtitle and hint.

### Changed
- Split `state.current` from `state.lastQuestion` to support Repeat Last
  after auto-advance.

---

## [0.1.0] — 2026-04-19

### Added
- Initial working version: melodic interval trainer.
- Sampled piano via Tone.js + Salamander Grand Piano.
- Configurable interval pool and direction.
- Score tracking (correct / total / streak).
- Dark studio-gear aesthetic.
