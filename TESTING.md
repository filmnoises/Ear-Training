# Testing

Manual checks to run after any code change. Smoke tests, not exhaustive.
If something breaks that's not listed here, add it.

## Smoke test — run after every change

### Loading
- [ ] Open the HTML file in a browser. "Loading piano samples…" banner appears.
- [ ] Banner disappears within a few seconds. Play button becomes enabled.
- [ ] Feedback line reads "Ready. Press Play."

### Melodic mode — basic
- [ ] Press Play. Two piano notes play in sequence, about 0.6s apart.
- [ ] Answer buttons appear for each enabled interval.
- [ ] Click correct answer → green feedback, ✓ on correct button.
- [ ] Auto-advance to next question after ~1.2s.
- [ ] Click wrong answer → red feedback, ✕ on wrong + ✓ on correct.
- [ ] No auto-advance on wrong — waits for user.
- [ ] "Repeat Last" replays the just-answered question.
- [ ] "Skip →" generates a new question without answering.

### Harmonic mode
- [ ] Click Harmonic tab. Header subtitle changes to "harmonic".
- [ ] Hint text changes to "two notes · at the same time".
- [ ] Direction chips appear dimmed / disabled.
- [ ] Reference tempo slider appears dimmed / disabled.
- [ ] Press Play → two notes play simultaneously.

### Settings changes mid-question (v0.3.0 regression)
- [ ] Start a question (press Play).
- [ ] Before answering, turn off all intervals except Tritone.
- [ ] Press Play again. The new question MUST be a tritone.
- [ ] Direction change mid-question → next Play respects it.
- [ ] Mode switch mid-question → next Play uses new mode.

### Reference panel — basic (v0.3.0)
- [ ] Each of the 12 reference buttons plays its interval when clicked.
- [ ] Brass-colored flash on the clicked button.
- [ ] Playing a reference interval does NOT affect the current quiz question.

### Reference panel — root selector (v0.5.0)
- [ ] On load, "Random" is selected, root chooser is hidden.
- [ ] Click "Fixed" → chromatic chooser (C through B) appears.
- [ ] Click any root note → that note becomes selected (visually pressed).
- [ ] Click any reference interval → root is the chosen note.
- [ ] Switch back to "Random" → chooser hides; reference uses random root.
- [ ] Edge case: with Fixed root = B (high), play Octave → it should play
      cleanly (octave-shift logic should keep it in keyboard range).
- [ ] Edge case: with Fixed root = C (low) and direction = Descending,
      play Octave → also plays cleanly.

### Reference panel — tempo slider (v0.5.0)
- [ ] Default value reads "1.5 s".
- [ ] Drag slider — number updates as you drag.
- [ ] Min value 0.4 s; max value 4.0 s.
- [ ] Click reference interval at 0.4 s → notes are quick (~snappy quiz pace).
- [ ] Click reference interval at 4.0 s → long pause between notes.
- [ ] Switch to harmonic mode → slider is disabled (visually + functionally).
- [ ] Switch back to melodic → slider re-enables, value preserved.

### Score tracking
- [ ] Correct answers increment Correct and Total, grow Streak.
- [ ] Wrong answers increment Total, reset Streak to 0.
- [ ] Score persists across mode switches.

## Accessibility checks — run after any UI change

### Keyboard navigation
- [ ] Tab through the page. Every interactive element shows brass focus outline.
- [ ] Tab order is logical: skip link → tabs → direction → Play / Repeat /
      Skip → answers → root mode buttons → root chooser (when visible) →
      tempo slider → reference buttons → pool chips.
- [ ] Space activates Play (when not focused on slider/input).
- [ ] R activates Repeat Last; S activates Skip.
- [ ] Number keys 1–9 pick the Nth visible answer.
- [ ] Arrow keys (Left/Right) move between mode tabs.
- [ ] Tempo slider responds to arrow keys when focused.
- [ ] Skip-to-main-content link appears at top-left when Tab-focused.

### Screen reader
- [ ] Mode tabs announce as "Melodic tab, selected, 1 of 2".
- [ ] Direction toolbar is announced as a toolbar with its label.
- [ ] Interval pool chips announce their pressed state.
- [ ] Answer buttons read as "Answer 3: Major 3rd, 4 semitones".
- [ ] Feedback changes are announced (live region).
- [ ] Reference buttons say "Play Perfect 5th reference" etc.
- [ ] Root chooser announces as a radio group; each note labeled.
- [ ] Tempo slider announces current value when focused.

### Color & motion
- [ ] With OS-level reduced-motion, transitions are near-instant.
- [ ] ✓ / ✕ symbols visible alongside green/red coloring.
- [ ] Text readable against dark backgrounds at normal viewing distance.

### TODO
- [ ] Eventually: real testing with sight-impaired users on their
      preferred screen readers.
