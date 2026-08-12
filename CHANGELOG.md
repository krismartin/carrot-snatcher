# Changelog

All notable changes to Carrot Snatcher are recorded here, newest first.
The format follows [Keep a Changelog](https://keepachangelog.com/); this project
has no formal releases yet, so entries are grouped by the date they landed.

## 2026-08-10

### Added
- Difficulty modes, chosen on the start screen: **Easy** is the game exactly as
  it was before the farmer existed, and **Hard** turns him loose. Easy is the
  default and the choice carries between rounds; picking a mode also shows or
  hides the farmer's rules on the start screen. Hard-mode runs are flagged with
  a 🔥 on the leaderboard so the two modes stay comparable.
- The farmer: a pitchfork-carrying, straw-hatted rival who hunts the bunny
  through the hedges. He dozes for the first few seconds of a round, then paths
  toward you along the shortest route (breadth-first over the maze) with an
  occasional wrong turn, and picks up pace as the clock runs down — but he is
  always slower than a bunny, so he can be outrun. Let him catch you and he
  pockets **5 of your carrots** (score included) and stomps off to the far side
  of the maze; you keep your place in the hedges and hop straight on, with a
  couple of safe seconds while he trudges back. The end screen reports how many
  times he got you and how much of your haul he made off with.

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
