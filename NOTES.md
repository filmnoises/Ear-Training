# Notes

Working notes, observations, half-formed ideas. This is an **inbox**, not a
plan. When something here gets real, move it to TODO.md. Periodically delete
things that no longer seem worth doing.

Format: date, a line or two, move on. Don't polish.

---

## 2026-04-20 (afternoon)

**Session sentence:** Added root-note selector and adjustable tempo slider
to the Reference panel. Split out "sing-first" as its own future feature.

**Big lesson:** Caught a "two ideas in one TODO item" — the original item
mixed "slower default" with "sing-first quiz mode." These are very
different things (one is a tweak, one is a new mode). Splitting them
preserved both ideas at their proper sizes. This is worth watching for
in every future TODO item: if I can spot a "maybe also..." or "and
possibly..." inside an item, that's the seam to split along.

**Small refactor worth noting:** Merged `playQuestion` and the inner
playback bits of `playIntervalOnDemand` into a single `playSequence(q)`
that takes a `gap` parameter. Quiz passes 0.6, Reference passes the
slider value. Two callers, one playback path. Less duplication, easier
to change tomorrow.

**A11y choice:** The root chooser uses role="radio" rather than toggle
buttons, because the user picks ONE root. Toggle buttons (aria-pressed)
would imply you can have several active. Same visual style, different
semantics. Worth remembering: aria-pressed = "this can be on/off
independently"; aria-checked + radio = "exactly one of a group is on."

**Stopped:** Shipped v0.5.0. App now feels much more usable as a singer's
practice tool — fixed root + slow tempo together is exactly the workflow
my voice teacher friend would want.

**Next session:** Either start sing-first mode (logical follow-on to
today's work) OR set up git (overdue). Probably git first — the project
is now 5 versions deep and getting valuable enough that not having it
backed up is a real risk.

---

## 2026-04-20 (morning)

**Session sentence:** Moving direction controls up near the mode tabs,
and establishing accessibility as a baseline priority going forward.

**Big decision:** Committed to accessibility as a from-the-start priority,
not a retrofit. Claude will carry this in memory.

**Honest assessment:** v0.3.0 had significant a11y gaps. v0.4.0 fixes
them. Lesson: should have done this from v0.1.0.

**Observation:** Good a11y often IS good code structure — proper toolbar
with aria-pressed buttons is cleaner than divs with custom state.

**Stopped:** Shipped v0.4.0.

**Next session:** Build root selector + tempo slider for Reference panel.

---

## 2026-04-19

**Session sentence:** Learning about best practices and setting up project
organization.

**Observation:** The pool-bug fix was a good example of derived state
getting stale when upstream state changes. Watch for this pattern.

**Idea:** Triad answer UI will need two axes — quality + inversion.

**Question:** Should mode switch reset score or keep running? Currently
keeps. Flag for later.

**Stopped:** Set up CHANGELOG, README, TODO, NOTES, TESTING.

**Next session:** Move direction controls up.
