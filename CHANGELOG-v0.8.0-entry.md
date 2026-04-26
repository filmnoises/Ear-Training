# Changelog

## v0.8.0 — 2026-04-25

### Added — Level 4: 7th chords

New training level for ear-training on 7th chords. Architecture mirrors Level 2 (triads): two-axis answer UI with explicit Submit, blocked/arpeggiated playback modes, "Seventh Focus" settings panel, and an on-demand reference grid.

**Chord qualities (4):** Major 7, Minor 7, Dominant 7, Half-diminished (m7♭5). Diminished 7 (dim7) is intentionally omitted from the user-facing pool but the data structure supports adding it later as an advanced toggle.

**Inversions (4):** Root, 1st, 2nd, 3rd. Stored in a separate `SEVENTH_INVERSIONS` constant rather than reusing the triad `INVERSIONS` constant, so 7th-chord changes cannot affect Levels 2 or 3.

**Voicings (2):** Tight (closed position) and Open (drop-2 — the second-from-top voice drops down an octave, producing a chord that spans roughly a 10th, the standard jazz "spread" sound). User-selectable from the Seventh Focus panel.

**Defaults (easier onramp):**
- Quality pool: Major 7 + Dominant 7 only (the most pedagogically meaningful starter pair — the "home" sound vs the "going somewhere" sound)
- Inversion pool: Root + 1st inversion only
- Mode: Arpeggiated (the 7th lands as a discrete event, easier to hear than blocked)
- Voicing: Tight
- Direction: Ascending

User can broaden the pool from the Seventh Focus settings as their ear builds.

**Root range:** MIDI 48–58 (C3 to A♯3). Slightly narrower than Level 2's 48–60 because open voicings can extend the chord up by an octave; this keeps the top note within the piano sample range even for the highest tight 3rd-inversion chords.

**Reference panel:** 4×4 grid (qualities × inversions). Buttons display short labels like "Maj7 / Root" with screen-reader aria-labels reading "Play Major 7 / Root inversion reference" for clarity. Reference uses the currently-selected voicing.

### Architecture notes

- New constants: `SEVENTH_QUALITIES`, `SEVENTH_INVERSIONS`, `SEVENTH_VOICINGS`
- New helper: `buildSeventhMidi(rootMidi, qualityKey, inversionKey, voicingType)` — returns MIDI array sorted low-to-high
- New state namespace: `state.l4` (mirrors `state.l2` shape with added `voicing` field)
- New JS engine: `l4_*` functions paralleling `l2_*` patterns
- Header sub-text now includes voicing label: e.g. `Level 4 · arpeggiated · ascending · tight`

### Accessibility

- Full keyboard parity with Level 2: Space (play/new), R (replay), S (skip), Enter (submit)
- All quality/inversion/voicing buttons have descriptive aria-labels
- Voicing chooser uses `role="radio"` with `aria-checked` (radio behavior, not toggle)
- Color-plus-symbol feedback (✓/✕) on answer buttons
- All new controls respect `prefers-reduced-motion`

### Files touched

- `ear-trainer.html` (regenerated)
- `CHANGELOG.md` (this entry)

---

## v0.7.2 — 2026-04-25

Patch: Tritone shows as "Tritone (Aug4/Dim5)" in the Level 3 target picker only. All other locations unchanged.
