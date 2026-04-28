# Changelog

All notable changes to the Ear Trainer (formerly Interval Trainer) are
documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- First-run onboarding overlay (v0.9.0) — explain "this is a guessing
  game; press Play, then click your guess; new to intervals? try the
  Reference panel first." Real-user feedback (April 2026) showed
  multiple non-musician testers didn't understand they were the one
  making the guesses, and didn't discover the Reference panel below
  the fold.
- Extended chords (Levels 5+): 9th, 11th, 13th — deserve their own
  design conversation around voicing range and pedagogical sequencing.
- Save settings to localStorage so they persist across sessions.
- Continued mobile-friendly layout review.
- Reference manual (separate from getting-started guide).
- Full User Manual catch-up: Level 4 (7th chords) section, 7th-chord
  music theory primer, v0.7.2 Tritone label note, v0.8.1 audio banner
  documentation. Was deferred from v0.8.2 to its own dedicated session
  to do the theory writeups carefully.

---

## [0.8.3] — 2026-04-28

Patch release: workflow cleanup. The User Manual link in the app
header now points to GitHub's rendered markdown view of
`USER-MANUAL.md` instead of the PDF. The PDF is no longer the
canonical reference — markdown is the single source of truth,
which removes the PDF re-export step from every release that
touches the manual.

### Changed
- **Manual link target.** From
  `https://filmnoises.github.io/Ear-Training/USER-MANUAL.pdf` to
  `https://github.com/filmnoises/Ear-Training/blob/main/USER-MANUAL.md`.
  GitHub renders markdown attractively in the browser; users land
  on the rendered manual without needing a separate PDF viewer.
  Mobile users in particular benefit (PDFs are clunky on phones).
- **Aria-label.** "Open User Manual in a new tab (PDF)" → "Open
  User Manual in a new tab" (no longer a PDF).

### Notes
- The `USER-MANUAL.pdf` file in the repo is now unreferenced from
  the app. It can be deleted in a future cleanup (or left in place
  for users who have bookmarked the old URL — old PDF stays
  accessible at the existing path).
- Going forward, manual edits are a single-file change: edit
  `USER-MANUAL.md`, push, and the linked rendered view updates
  automatically.

### Files touched

- `ear-trainer.html` (regenerated)
- `CHANGELOG.md` (this entry)

---

## [0.8.2] — 2026-04-28

Patch release: accessibility and ADHD-friendliness pass. Triggered
by feedback from a sight-impaired tester (single-letter shortcuts
collide with screen reader navigation keys) plus a design review
flagging that the page below the stage area piles up with reference
grids and settings, which is hard for users with ADHD.

### Added
- **In-app "Keyboard shortcuts" disclosure on every level panel.**
  Collapsed by default; opens to show the per-level shortcuts plus a
  brief screen-reader focus-mode warning. Users who hit the conflict
  the moment they try a shortcut now get the warning in context, not
  only buried in the PDF manual.
- **Screen reader focus-mode guidance in the User Manual.** Per-screen-
  reader instructions for NVDA, JAWS, VoiceOver, and Narrator on how
  to enable focus / forms / pass-through mode.

### Changed
- **Reference, Settings, and Focus panels are collapsed by default.**
  Wrapped in native `<details>` elements with custom `<summary>`
  styling that matches the existing panel typography. Native
  `<details>` handles keyboard, focus, and screen reader state
  ("collapsed" / "expanded") automatically — no JavaScript toggle
  needed. Page now arrives quiet, with only the question, answer
  choices, and score visible. Users who want their Reference grid or
  pool toggles open can simply click the disclosure once per session
  (state does not persist — that's a localStorage feature in the
  Unreleased section).
- **Level 3's settings split into two panels: Target (open) and
  Practice settings (collapsed).** Target picker is required to start
  practicing, so it stays open by default. Voice range, wait timer,
  and continuous toggle move into the collapsed Practice settings.
- **Skip link now actually moves focus.** Added `tabindex="-1"` to
  `<main>` so activating the skip link moves focus there in addition
  to scrolling. Previously, the link scrolled the viewport but left
  focus on the link itself, so screen reader users heard nothing
  change after activating it.
- **Mode hint spans now announced to screen readers.** Removed
  `aria-hidden="true"` from the four `.mode-hint` spans (e.g., "two
  notes · at the same time"). Sighted users were getting useful
  context that screen reader users weren't.
- **Feedback strings always lead with an unambiguous status word.**
  L1 already led with "Correct" / "Incorrect"; L2 and L4 now also
  lead with "Incorrect" instead of "Not quite" (the warm partial-
  credit text remains, just demoted to the second clause). L3 self-
  rating feedback now leads with "Got it —" or "Missed —" before the
  warm continuation message. Ensures the first word a screen reader
  announces tells the user the result.
- **Audio banner aria-live downgraded** from `assertive` to `polite`.
  The banner is visually prominent enough on its own; assertive was
  interrupting screen readers mid-sentence whenever the banner
  appeared, which is louder than warranted now that the affordance
  is stable and well-tested.
- **Reduced-motion handling strengthened.** The existing wildcard
  block (`*` selector with `transition-duration: 0.01ms`) was already
  good for transitions. Added explicit rules for `box-shadow` glow
  effects (which the wildcard misses), plus belt-and-suspenders for
  `animation-iteration-count` and `scroll-behavior`. Comment in the
  CSS explains the philosophy: flatten transitions and animations
  while preserving state visibility (the stage indicator still turns
  green; it just doesn't pulse or glow).

### Notes
- Two new CSS components: `details.panel-collapsible` (wraps the
  Reference / Settings / Focus panels with matching typography and
  custom +/- indicator) and `details.shortcuts-help` (the quieter
  per-level keyboard shortcut disclosure at the top of each panel).
- No new state. The collapsed/expanded state of each panel resets on
  reload — persisting it via localStorage is queued for the
  Unreleased section.
- Followed the user's suggested pattern of letting native `<details>`
  do all the work — no JavaScript, no aria-expanded toggling, just
  semantic HTML doing what it's designed to do.

### Files touched

- `ear-trainer.html` (regenerated)
- `CHANGELOG.md` (this entry)
- `USER-MANUAL.md` (screen-reader section added; version label
  changed to date-based; Level 4 catch-up deferred to a dedicated
  session)

---

## [0.8.1] — 2026-04-26

Patch release: usability and reliability. Triggered by real-user
feedback that the app played silently on iPhone with no indication
of why, and that testers had to manually open the User Manual in a
separate browser tab.

### Added
- **User Manual link in the header.** Small "User Manual ↗" link at
  top-right opens the GitHub-hosted PDF in a new tab. Styled in the
  muted JetBrains Mono UI label style — present but not competing
  with the level tabs. The "↗" is the standard convention for
  "opens externally" and is hidden from screen readers (the
  aria-label clarifies it's a new tab).
- **Prominent audio-not-ready banner.** When the Web Audio context is
  suspended (the default state on every page load until a user
  gesture), a warm-accent-colored banner appears at the top of the
  app with the message "Tap any button to enable sound" plus an
  explicit iPhone silent-switch hint. Banner has a dismiss button
  for users who don't need it.
- **Sample loading failure detection.** If the Salamander piano
  samples haven't loaded after 15 seconds, the audio banner switches
  to a red-bordered error state explaining that the samples couldn't
  load and suggesting a network/reload check. Previously, a CDN
  failure would leave the user with a perpetual "Loading…" message
  and no recourse.

### Changed
- **AudioContext auto-resume on user interaction.** A capture-phase
  `pointerdown` listener at the document level calls `Tone.start()`
  and explicitly resumes the AudioContext if suspended. Belt-and-
  suspenders alongside the existing per-button `Tone.start()` calls
  — covers cases where iOS suspends the context after the user
  backgrounds the app and returns. Includes a fast-path early
  return so it's a near-zero-cost no-op when audio is already running.
- **AudioContext state listener.** When the context state changes
  (suspended → running, or vice versa), the banner updates
  automatically.

### Notes
- New `audioState` object tracks three independent conditions:
  `samplesLoaded`, `contextRunning`, `loadFailed`, plus a
  `bannerDismissed` flag.
- New `updateAudioBanner()` is the single source of truth for what
  the banner shows; called whenever any audio state changes.
- New `ensureAudioRunning()` is the canonical "make audio work now"
  function — safe to call repeatedly from any user gesture handler.
- Header restructured: `<h1>` and the new `.manual-link` now live
  inside a `.header-main` flex container; the version sub-text
  remains below.

---

## [0.8.0] — 2026-04-25

Minor release: adds Level 4 (7th chords).

### Added — Level 4: 7th chords
- **Chord qualities (4):** Major 7, Minor 7, Dominant 7, Half-
  diminished (m7♭5). Diminished 7 (dim7) is intentionally omitted
  from the user-facing pool but the data structure supports adding
  it later as an advanced toggle.
- **Inversions (4):** Root, 1st, 2nd, 3rd. Stored in a separate
  `SEVENTH_INVERSIONS` constant rather than reusing the triad
  `INVERSIONS` constant, so 7th-chord changes cannot affect Levels
  2 or 3.
- **Voicings (2):** Tight (closed position) and Open (drop-2 — the
  second-from-top voice drops down an octave, producing a chord
  that spans roughly a 10th, the standard jazz "spread" sound).
  User-selectable from the Seventh Focus panel.
- **Reference panel:** 4×4 grid (qualities × inversions). Buttons
  display short labels like "Maj7 / Root" with screen-reader
  aria-labels reading "Play Major 7 / Root inversion reference"
  for clarity. Reference uses the currently-selected voicing.

### Defaults — easier onramp
- Quality pool: Major 7 + Dominant 7 only (the most pedagogically
  meaningful starter pair — the "home" sound vs the "going
  somewhere" sound).
- Inversion pool: Root + 1st inversion only.
- Mode: Arpeggiated (the 7th lands as a discrete event, easier to
  hear than blocked).
- Voicing: Tight.
- Direction: Ascending.
- User can broaden the pool from the Seventh Focus settings as
  their ear builds.

### Notes
- New constants: `SEVENTH_QUALITIES`, `SEVENTH_INVERSIONS`,
  `SEVENTH_VOICINGS`.
- New helper: `buildSeventhMidi(rootMidi, qualityKey, inversionKey,
  voicingType)` — returns MIDI array sorted low-to-high.
- New state namespace: `state.l4` (mirrors `state.l2` shape with
  added `voicing` field).
- New JS engine: `l4_*` functions paralleling `l2_*` patterns.
- Header sub-text now includes voicing label, e.g. `Level 4 ·
  arpeggiated · ascending · tight`.
- Root range MIDI 48–58 (C3 to A♯3), slightly narrower than Level
  2's 48–60 because open voicings can extend the chord up by an
  octave; this keeps the top note within the piano sample range
  even for the highest tight 3rd-inversion chords.
- Full keyboard parity with Level 2: Space (play/new), R (replay),
  S (skip), Enter (submit).
- Voicing chooser uses `role="radio"` with `aria-checked` (radio
  behavior, not toggle).

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
