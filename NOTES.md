# Notes

Working notes, observations, half-formed ideas. This is an **inbox**, not a
plan. When something here gets real, move it to TODO.md. Periodically delete
things that no longer seem worth doing.

Format: date, a line or two, move on. Don't polish.

---

## 2026-04-23

# In the bottom "pool" choice area, put a header and call it "triad focus" so if someone wants to work on a specific area, they can focus on it. 
# rename "quality pool" to "chord quality" 
# rename "inversion pool" to "chord inversion" 
# move the triad focus box above the question but below the level one / level two box to see if that feels better. 
# make all of the fonts everywhere 1 point larger
# in the Question Play box, change the font color of "space" to something with a lot more contrast. It does not read easily with the yellowish background. 


**Session sentence:** Build Level 2 (triads) and rename the app to
"Ear Trainer" to reflect the broader scope.

**Big build:** First real multi-level app. Added Level 1 / Level 2 tab
structure at the top, existing interval trainer tucked inside Level 1
unchanged. Level 2 has blocked and arpeggiated playback modes, major
and minor triads (dim/aug deferred), all three inversions with user-
toggleable pool, two-axis answer UI with explicit Submit, partial-
credit feedback.

**State architecture win:** Split `state` into `state.l1` and `state.l2`.
Each level's data lives in its own sub-object. All L1 functions
prefixed `l1_`, all L2 functions `l2_`. This made the code dramatically
easier to reason about — no accidental crossover, clear ownership.
Worth remembering the pattern: when an app grows to multiple top-level
sections, namespace the state to match.

**Design choice worth noting:** Level 2 uses an EXPLICIT SUBMIT button
rather than auto-submit, per Rick's call. This turned out to be
pedagogically correct — users can experiment with picks before
committing. Also supports the "Clear Picks" affordance and partial-
credit feedback, both of which wouldn't make sense without submit.

**Design choice worth noting #2:** The Reference panel for Level 2
shows every quality × inversion combination as its own button (so 2×3
= 6 buttons right now, will grow to 4×3 = 12 when dim/aug added).
Grid naturally scales. Users can hear any specific voicing on demand.

**Partial-credit feedback:** When a Level 2 answer has one axis right
and one wrong, we specifically say "Quality right, inversion wrong" or
"Inversion right, quality wrong." This is much more informative than
just "wrong" and helps the user understand where their ear is and
isn't working yet.

**Triad voicing math:** Buildng the MIDI pitches was a nice small
piece of music-theory-as-code. Root position [P0, P1, P2] from the
quality intervals, then:
  - 1st inv: [P1, P2, P0+12]  (third on bottom, root up an octave)
  - 2nd inv: [P2, P0+12, P1+12]  (fifth on bottom, root+third up)
Documented in `buildTriadMidi()` with comments.

**Rename:** Went from "Interval Trainer" to "Ear Trainer" since the
scope now clearly exceeds intervals. Also renamed the file from
`interval-trainer.html` to `ear-trainer.html`. Past versioned
releases keep their old names (they *were* Interval Trainer).

**Open question for next session:** How does arpeggiated mode actually
feel for hearing scale-tone progression? Rick specifically hoped this
would teach scale-degree listening. Worth testing with real practice
before declaring it works.

**Stopped:** Shipped v0.6.0. Substantial release — two new levels of
architecture, three new playback modes (blocked, arpeggiated up,
arpeggiated down), full Level 2 UI with two-axis answers.

**Next session:** Add dim/aug triads, or tackle sing-first mode, or
set up GitHub for cloud backup. Probably dim/aug first — small addition
that completes the basic triad set. OR pause and test Level 2 with
music educators to see if the design choices hold up.

---

## 2026-04-22

**Session sentence:** Set up git for the project.

**Completed:** Git installed and configured, repo initialized, first
commit made with v0.5.0 baseline. Second commit for renaming the
versioned release file. Learned the basic add/commit/log cycle.
Fell into vim once, learned how to escape.

**Stopped:** Set up git, made first couple of commits. Good learning
day despite the vim sidetrack.

**Next session:** Build Level 2 / triad module.

---

## 2026-04-20 (afternoon)

**Session sentence:** Added root-note selector and adjustable tempo
slider to the Reference panel.

**Lesson:** Caught a "two ideas in one TODO item" — original item
mixed "slower default" with "sing-first quiz mode." Split them.
Pattern worth watching for in every future TODO.

**Stopped:** Shipped v0.5.0.

---

## 2026-04-20 (morning)

**Session sentence:** Move direction up; establish a11y as baseline.

**Big decision:** A11y is a from-the-start priority, not a retrofit.

**Stopped:** Shipped v0.4.0.

---

## 2026-04-19

**Session sentence:** Set up project organization.

**Stopped:** Set up CHANGELOG, README, TODO, NOTES, TESTING.
