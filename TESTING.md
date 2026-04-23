# Testing

Manual checks to run after any code change. Smoke tests, not exhaustive.
If something breaks that's not listed here, add it.

## Smoke test — run after every change

### Loading
- [x] Open the HTML file in a browser. "Loading piano samples…" banner appears.
- [x] Banner disappears within a few seconds. Level 1 Play button enables.
- [x] Switch to Level 2 tab — Play button there also enabled.
- [x] Both feedback lines read "Ready. Press Play."

### Level 1 · Melodic mode
- [ ] Press Play. Two piano notes play in sequence, about 0.6s apart.
- [ ] Answer buttons appear for each enabled interval.
- [ ] Click correct answer → green feedback, ✓ on correct button.
- [ ] Auto-advance to next question after ~1.2s.
- [ ] Click wrong answer → red feedback, ✕ on wrong + ✓ on correct.
- [ ] No auto-advance on wrong.
- [ ] Repeat Last replays the just-answered question.
- [ ] Skip generates a new question without answering.

### Level 1 · Harmonic mode
- [ ] Click Harmonic tab within Level 1. Header shows "Level 1 · harmonic".
- [ ] Direction chips dimmed/disabled.
- [ ] Reference tempo slider dimmed/disabled.
- [ ] Play → two notes simultaneously.

### Level 1 · Reference panel
- [ ] Each of the 12 reference buttons plays its interval.
- [ ] Random root / Fixed root toggle works.
- [ ] Tempo slider affects melodic playback spacing.

### Level 2 · Blocked mode
- [ ] Click Level 2 tab. Header shows "Level 2 · blocked".
- [ ] Feedback reads "Ready. Press Play."
- [ ] Press Play → three notes play simultaneously.
- [ ] Direction bar is dimmed/disabled (blocked mode).
- [ ] Quality row shows Major and Minor buttons.
- [ ] Inversion row shows Root / 1st / 2nd buttons.
- [ ] Submit button is disabled until both axes picked.
- [ ] Click a quality → it highlights (brass-colored "selected" state).
- [ ] Click an inversion → it highlights too.
- [ ] Submit button enables once both are picked.
- [ ] Clear Picks button enables when any pick is made.
- [ ] Clear Picks clears both selections and disables Submit.
- [ ] Submit a correct answer → green feedback, auto-advance.
- [ ] Submit a wrong answer (both wrong) → "Not quite" message.
- [ ] Submit with only one wrong → partial-credit message
      ("Quality right, inversion wrong" or vice versa).
- [ ] Enter key submits (when Submit is enabled).

### Level 2 · Arpeggiated mode
- [ ] Click Arpeggiated. Header shows "Level 2 · arpeggiated · [direction]".
- [ ] Direction bar re-enables.
- [ ] Reference tempo slider re-enables.
- [ ] Press Play → three notes play in sequence.
- [ ] Switch direction to Descending → next question plays notes
      from high to low.
- [ ] Switch to Mixed → questions randomize direction.

### Level 2 · Reference panel
- [ ] Every quality × inversion combination has a button.
- [ ] Each button plays that specific triad.
- [ ] Random/Fixed root toggle works.
- [ ] Tempo slider affects arpeggiated playback (blocked mode ignores it).

### Level 2 · Settings changes mid-question
- [ ] Start a triad question.
- [ ] Before answering, disable all qualities except Minor.
- [ ] Press Play again. New question MUST be a minor triad.
- [ ] Same for disabling inversions — next question respects the pool.
- [ ] Switching mode (blocked ↔ arpeggiated) invalidates current question.

### Score tracking
- [ ] Level 1 correct/wrong updates Level 1 score only.
- [ ] Level 2 correct/wrong updates Level 2 score only.
- [ ] Switching levels does not reset or alter either score.

## Accessibility checks

### Keyboard navigation
- [ ] Tab reaches every interactive element on both levels.
- [ ] Brass focus outline visible everywhere.
- [ ] Arrow keys navigate within tab groups (level tabs, mode tabs).
- [ ] Space = Play; R = Repeat; S = Skip (routes to active level).
- [ ] Enter submits Level 2 answer when Submit is enabled.
- [ ] Tempo sliders respond to arrow keys when focused.

### Screen reader
- [ ] Level tabs announce as "Level 1: Intervals tab, selected, 1 of 2".
- [ ] Mode tabs (within each level) also announce properly.
- [ ] Feedback live region announces correct/wrong.
- [ ] Answer buttons have descriptive aria-labels.
- [ ] Pool chips announce pressed/unpressed state.
- [ ] Partial-credit feedback in Level 2 reads naturally.

### TODO
- [ ] Real testing with sight-impaired users on their preferred
      screen readers.
