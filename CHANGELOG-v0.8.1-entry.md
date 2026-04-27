# Changelog — v0.8.1 entry

## v0.8.1 — 2026-04-26

Patch release: usability and reliability. Triggered by real-user feedback that the app played silently on iPhone with no indication of why, and that testers had to manually open the User Manual in a separate browser tab.

### Added

- **User Manual link in the header.** Small "User Manual ↗" link at top-right opens the GitHub-hosted PDF in a new tab. Styled in the muted JetBrains Mono UI label style — present but not competing with the level tabs. The "↗" is the standard convention for "opens externally" and is hidden from screen readers (the aria-label clarifies it's a new tab).
- **Prominent audio-not-ready banner.** When the Web Audio context is suspended (the default state on every page load until a user gesture), a warm-accent-colored banner appears at the top of the app with the message "Tap any button to enable sound" plus an explicit iPhone silent-switch hint: "iPhone users: also check that the silent switch on the side of your phone is OFF (orange showing means muted — flip it the other way)." Banner has a dismiss button for users who don't need it.
- **Sample loading failure detection.** If the Salamander piano samples haven't loaded after 15 seconds, the audio banner switches to a red-bordered error state explaining that the samples couldn't load and suggesting a network/reload check. Previously, a CDN failure would leave the user with a perpetual "Loading…" message and no recourse.

### Changed

- **AudioContext auto-resume on user interaction.** A capture-phase `pointerdown` listener at the document level calls `Tone.start()` and explicitly resumes the AudioContext if suspended. This is belt-and-suspenders alongside the existing per-button `Tone.start()` calls — covers cases where iOS suspends the context after the user backgrounds the app and returns. Includes a fast-path early return so it's a near-zero-cost no-op when audio is already running.
- **AudioContext state listener.** When the context state changes (suspended → running, or vice versa), the banner updates automatically.

### Architecture notes

- New `audioState` object tracks three independent conditions: `samplesLoaded`, `contextRunning`, `loadFailed`, plus a `bannerDismissed` flag.
- New `updateAudioBanner()` function is the single source of truth for what the banner shows; called whenever any audio state changes.
- New `ensureAudioRunning()` is the canonical "make audio work now" function — safe to call repeatedly from any user gesture handler.
- Header restructured: `<h1>` and the new `.manual-link` now live inside a `.header-main` flex container; the version sub-text remains below.

### Accessibility

- Audio banner uses `role="alert"` and `aria-live="assertive"` because the user *needs* to act on it for the app to function.
- Dismiss button has `aria-label="Dismiss audio notice"`.
- Manual link has `aria-label="Open User Manual in a new tab (PDF)"` so screen-reader users know both the destination and the new-tab behavior in advance.
- Manual link `↗` glyph is wrapped in `aria-hidden="true"` to avoid announcement of the symbol name.
- All new colors meet WCAG AA contrast against the dark background (the warm accent is the existing `--accent-hot` already used elsewhere in the app).

### Files touched

- `ear-trainer.html` (regenerated)
- `CHANGELOG.md` (this entry — merge into top of your local file)
