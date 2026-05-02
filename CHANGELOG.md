# Changelog

All notable changes to the Ear Trainer (formerly Interval Trainer) are
documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
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

## [0.9.1] — 2026-05-02

Patch release: documentation and housekeeping. No app code changes.

### Changed — User Manual

- Manual updated to reflect the v0.9.0 UX redesign:
  - Quick-start now opens with the Reference panel as step 3, before
    pressing Play. Mirrors the in-app onboarding hint.
  - Each level section gains a "Layout" subsection describing the
    MODE and DIRECTION labels, the Reference-above-quiz ordering, and
    the renamed stage headings ("Guess The Interval" / "Guess The
    Triad" / "Practice").
  - Settings panel descriptions use the new names ("Interval Quiz
    Choices," "Triad Quiz Choices") instead of "Interval Pool" and
    "Triad Focus."
  - Reference panel description updated for the new Fixed-default-at-C4
    behavior.
  - Play button described as green throughout (was "brass-colored").
- New consolidated **Keyboard shortcuts** section between Level 3 and
  Tips. The four per-level shortcut blocks at the bottom of each level
  section now point to this consolidated section instead of repeating
  the same lists. Reflects the in-app consolidation from v0.9.0.
- Accessibility section updated: shortcut references no longer say
  "see the level sections above"; the in-app reminder paragraph now
  describes the single global disclosure instead of four per-level
  ones.
- Level 4 disclaimer expanded slightly: notes that Level 4 follows the
  same v0.9.0 layout pattern as Levels 1 and 2 even though its full
  documentation (including 7th-chord theory primer) is still pending
  for a future release.
- Top comment in USER-MANUAL.html now carries a versioned/dated header
  line, matching the convention used in ear-trainer.html.
- "Last updated April 2026" stamp in the topbar bumped to May 2026.

### Changed — Repo housekeeping (committed in earlier housekeeping
commit, captured here for completeness)

- Retired stale documentation to a local archive (kept on the author's
  machine in `1. OLD DNU/`, no longer tracked by git):
  `NOTES.md`, `TODO.md`, `TESTING.md`, `USER-MANUAL.md`,
  `Ear Training User Notes.docx`, `USER-MANUALv1.pdf`, and the old
  experiment file `seventh-chord-test-harness.html`.
- Walked back the v0.8.4 commitment to keep `USER-MANUAL.md` in the
  repo for "historical reference." The retired copy is preserved in
  the local archive; the canonical documentation is now exclusively
  `USER-MANUAL.html` going forward.
- `Releases/` folder added to `.gitignore` so the author's local
  versioned-archive of release builds doesn't accidentally end up in
  the repo on a future `git add` command.

### Fixed — release tooling

- `release.sh` final "Done" print no longer crashes with `unbound
  variable: GRN?` when running under `set -u`. Wrapped the variable
  references in braces (`${GRN}` instead of `$GRN`) so bash correctly
  identifies the variable name boundary against the multi-byte ✓
  glyph that follows. Cosmetic-only bug — never affected the actual
  release operations, which complete before the failing line runs.
- Marked `release.sh` executable (`chmod +x`) so the executable bit
  is recorded in git and survives clones to other machines.

### Files touched

- `USER-MANUAL.html` (regenerated)
- `CHANGELOG.md` (this entry)
- `release.sh` (one-line bug fix)

### Notes

This is the first patch release using the new `release.sh` workflow
end-to-end on a release that began with a clean working tree (rather
than the messy state v0.9.0 was tagged from). Should be the smoothest
release-script run yet.

---

## [0.9.0] — 2026-05-01

Minor release: UX redesign aimed at first-run discovery. Earlier real-
user testing (April 2026) showed that several non-musician testers
didn't understand they were the one making the guesses, and didn't
discover the Reference panel because it sat below the fold under the
quiz. The original v0.9.0 plan was a modal first-run onboarding overlay;
this release takes a lighter approach instead — making the page itself
self-explanatory by labeling controls, repositioning the Reference
panel, and pointing at it with a small inline caption.

### Changed — layout reorder (per level)

- **Mode row gets an explicit "MODE" label.** Previously the mode tabs
  (Melodic/Harmonic, Blocked/Arpeggiated, etc.) sat alone at the top of
  each level panel with no caption. Sighted first-run users were reading
  them as decorative header chrome instead of as live controls. The
  uppercase JetBrains Mono "MODE" label sits to their left now.
- **Direction row gets an explicit "INTERVAL DIRECTION" (L1) or
  "ARPEGGIO DIRECTION" (L2/L4) label.** Same problem, same fix. L3 has
  no direction control.
- **Reference panel moved ABOVE the quiz/stage.** Was the single biggest
  finding from testing — non-musicians never scrolled down to find it.
  Now it's right above the Play button on L1, L2, L4. L3 has no
  Reference panel (the Target picker serves a different role).
- **"Quiz Choices" panels moved to the bottom of each level.** Settings
  for narrowing the quiz pool aren't first-run material; they belong
  out of the way until you want them.
- **New inline caption above each Reference panel:** "↓ New here? Open
  the Reference section first to hear and learn the sounds." Italic
  body type with a green ↓ marker; speaks directly to the user testing
  finding.

### Changed — labels and naming

- **Stage headings become explicit verbs:**
  - L1: "Question" → "Guess The Interval"
  - L2: "Question" → "Guess The Triad"
  - L3: "Sing-First Practice" → "Practice"
  - L4: "Question" → "Guess The 7th Chord"
- **Quiz Choices panels rename for plain-English clarity:**
  - L1: "Interval pool" → "Interval Quiz Choices"
  - L2: "Triad Focus" → "Triad Quiz Choices"
  - L4: "Seventh Focus" → "7th Chord Quiz Choices"
  - L3 keeps its existing structure (Target + Practice settings, a
    different shape entirely — Target is required, not a filter).
- **"Mixed" stays "Mixed."** Considered renaming it to "Random," but
  that would collide with the Random/Fixed root setting on the
  Reference panel.

### Changed — Reference defaults

- **Reference root default flipped from Random to Fixed.** Users
  exploring the Reference grid for the first time benefit from a stable
  reference pitch (C4) — random root makes intervals harder to compare
  side-by-side. The chooser also now shows from page load (the `hidden`
  attribute is gone), so the C4 selection is immediately visible.
- **Fixed/Random button order swapped: Fixed on the left, Random on the
  right.** Matches the new default and reads left-to-right as
  "this is what's on; here's the alternative."

### Changed — keyboard shortcuts disclosure consolidated

- **The four per-level "Keyboard shortcuts" disclosures from v0.8.2
  collapse into ONE global disclosure** that lives between the header
  and the level tabs. Its contents update via `updateGlobalShortcuts()`
  whenever the level changes. The screen-reader focus-mode warning now
  appears once instead of four times — same warning, same wording, just
  no longer duplicated.
- New `SHORTCUT_SETS` object keys the per-level shortcut tables; the
  updater rebuilds the `<dl>` from whichever set matches `state.currentLevel`.

### Changed — Play button

- **Play button now green** (var(--good)) instead of brass
  (var(--accent)). The brass was the same color used for selection
  highlights on answer buttons; some testers were misreading the Play
  button as "already selected" rather than "press me." Green reads
  cleanly as a primary go-action.
- Hover color matches the existing Submit button hover (`#b0d598`) —
  green primary actions across the app behave consistently now.
- Slightly larger: `font-size: 17px`, `padding: 14px 22px`. Bigger hit
  area and more visual weight for the primary CTA.

### Notes

- All accessibility features from v0.8.2 are preserved: ARIA roles and
  labels still match the new structure (label IDs are referenced via
  `aria-labelledby` on the mode tablists and direction toolbars), the
  skip link still moves focus, mode-hint spans are still announced,
  reduced-motion handling is unchanged, the `<details>`-based panel
  collapse pattern is unchanged.
- New CSS components: `.control-row-with-label`, `.control-label-large`,
  `.ref-onboarding-hint`. The existing `details.shortcuts-help` styling
  from v0.8.2 is reused unchanged for the global disclosure.
- JS changes are surgical: `state.l{1,2,4}.refRootMode` defaults flip
  to `'fixed'`; new `SHORTCUT_SETS` table and `updateGlobalShortcuts()`
  function; one new line in the level-tab onclick handler and one at
  init. Engine logic, audio handling, render functions, and event
  wiring are all unchanged.

### Files touched

- `ear-trainer.html` (regenerated)
- `CHANGELOG.md` (this entry; obsolete v0.9.0 overlay bullet removed
  from `[Unreleased]`)

### Deferred to next session (deliberate scope split)

- `USER-MANUAL.html` updates — quick-start step ordering, per-level
  layout descriptions, settings panel names, Play button color, stage
  heading names, and the "shortcuts now live in one place" note.
  Split out so this release ships small and reviewable rather than
  blowing the tool budget like last time.

### Tooling

- New `release.sh` shell script — first release using the streamlined
  workflow. See the script's header comment and the accompanying
  tutorial for details.

---

## [0.8.4] — 2026-04-28

Patch release: User Manual is now a styled HTML page hosted on the
same domain as the app. Replaces the GitHub-rendered markdown link
from v0.8.3 because the GitHub view wraps the manual in repository
chrome (file browser, repo nav, commit history sidebar) that is
confusing for non-technical users.

### Added
- **`USER-MANUAL.html`** — standalone documentation page styled in a
  light docs aesthetic: cream background, Fraunces serif body type,
  warm muted accent color for headings, ~65–75 character measure
  for comfortable reading. Includes a table of contents, anchored
  section IDs for deep linking, a "← Back to app" link, and a print
  stylesheet that strips chrome and uses pure black on white.
- The HTML manual is now the canonical documentation. The markdown
  source (`USER-MANUAL.md`) remains in the repo for historical
  reference but is no longer the source of truth — when content
  needs updating, edit `USER-MANUAL.html` directly.

### Changed
- **Manual link target.** From the GitHub repository file viewer
  back to a relative path (`USER-MANUAL.html`) hosted on the same
  domain as the app. Same-domain serving means: no GitHub chrome,
  no third-party site, no PDF viewer, no domain switch.
- The relative URL works regardless of the hosting domain — useful
  if the project ever moves off `filmnoises.github.io`.

### Notes
- This is the third change to the manual link in three days
  (PDF → GitHub markdown → standalone HTML). The pace was
  exploratory; this version is the intended end state. Future
  manual edits will simply update `USER-MANUAL.html`.
- The "Level 4 not yet documented" notice in the manual is
  preserved. Full Level 4 / 7th-chord theory documentation remains
  queued in the Unreleased section.

### Files touched

- `ear-trainer.html` (regenerated)
- `USER-MANUAL.html` (new file — replaces the PDF as the canonical manual)
- `CHANGELOG.md` (this entry)

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
