# Changelog

All notable changes to Carrot Snatcher are recorded here, newest first.
The format follows [Keep a Changelog](https://keepachangelog.com/); this project
has no formal releases yet, so entries are grouped by the date they landed.

## 2026-07-24

### Fixed
- Audio no longer goes silent after an idle spell. Safari/WebKit parks an idle
  audio context in the non-standard `interrupted` state (not just `suspended`),
  which the old resume check missed — so starting a new round after lingering on
  the leaderboard came up with no music or sound effects. The context is now
  revived whenever it isn't `running`, plus on tab refocus and the next
  interaction. ([#4](https://github.com/krismartin/carrot-snatcher/pull/4))

## 2026-07-22

### Added
- Clean-sweep celebration: clear every carrot in the maze for a **+50 bonus**, a
  party-popper pop (synthesized in Web Audio), and a burst of confetti. The clock
  keeps running so you can still chase golden carrots, and a clean sweep gets its
  own end-screen title. ([#2](https://github.com/krismartin/carrot-snatcher/pull/2))

### Changed
- Mobile controls: the on-screen dpad is gone — steer the bunny by **swiping
  anywhere on the maze**. A short flick is enough, diagonal swipes resolve to the
  dominant axis, and page scroll is locked during a round so a margin swipe never
  moves the window. Desktop keyboard play (arrows + WASD) is
  unchanged. ([#1](https://github.com/krismartin/carrot-snatcher/pull/1))
