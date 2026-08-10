# 🐰🥕 Carrot Snatcher

A browser-based arcade maze game. Play a bunny loose in a hedge maze and race a 60-second clock to snatch as many carrots as you can - with a pitchfork-wielding farmer on your tail, if you pick hard mode.

Built as a single, dependency-free HTML file - plain JavaScript, Canvas, and the Web Audio API. No framework, no build step.

## The origin story

This game was designed by my 7-year-old daughter. Over dinner one evening, she described exactly how she wanted it to play - a bunny finding its way through a maze to collect carrots against a timer, with a special glowing bonus carrot in the middle - and then drew the whole thing out:

![The original game sketch, drawn by my daughter](assets/sketch.jpg)

Her sketch already had every core mechanic in it: the **timer** ("5 minits", boxed at the top), a **winding maze with looping paths**, **carrots scattered along the routes** as little orange dashes, **bunnies** placed in the maze, **arrows** showing how you move - and, right in the centre, the **big bonus carrot drawn with sparkle lines** to show that it glows and is worth chasing. This project is just that sketch, brought to the screen. 🥕

And like any good product owner, the moment the first version was up and running, the change requests started rolling in - fast 🚀 _"Can I pick different bunnies?"_ _"Can it have music?"_ _"How do I change my bunny after the game finishes?"_ Most of the features here exist because she asked for them on the spot. 🐰

## Gameplay

- **Objective:** collect as many carrots as possible before the timer runs out.
- **Fresh maze every round:** each game generates a new maze (recursive-backtracker carving with extra walls removed for Pac-Man-style loops), so no two runs are the same.
- **The golden carrot:** a larger, glowing bonus carrot worth **double points**. It spawns far from you, favours dead-ends, and relocates every few seconds if you don't reach it in time - a risk-reward chase for a higher score.
- **The farmer (hard mode only):** he starts the round dozing on the far side of the maze (💤), then sets off after you, taking the shortest path through the hedges and speeding up as the clock runs down. He is always slower than a bunny and takes the odd wrong turn, so he can be outrun - but let him reach you and he pinches **5 of your carrots**, points and all. You keep your place in the maze and hop straight on; he stomps back to the far side and gets a couple of seconds' rest before resuming the chase. The end screen tells you how many times he got you and how much of your haul he took.
- **Clean-sweep bonus:** snatch *every* carrot in the maze and you earn a **+50 bonus** with a party-popper pop and a burst of confetti. The clock keeps running, so you can still chase golden carrots afterward - and a clean sweep gets its own celebration on the end screen.
- **Two numbers that matter:** _carrots collected_ (the raw count) and _score_ (points). A normal carrot is 1 point; a golden one is 2, so your score can run ahead of your carrot count. The leaderboard ranks by score.

## Difficulty

Choose your challenge on the start screen, before picking a bunny:

- **🐰 Easy** - just you and the carrots. Exactly the game as it was before the farmer arrived: no chase, no pressure.
- **🧑‍🌾 Hard** - the farmer hunts you through the maze.

Easy is the default, and your choice carries between rounds. Scores set on hard mode are flagged with a 🔥 on the leaderboard, so the two modes stay comparable.

## Controls

- **Desktop:** Arrow keys or `WASD`.
- **Mobile:** swipe anywhere on the maze to hop that way. A short flick is enough, and diagonal swipes pick whichever direction you moved most.

## Characters

Pick from six coloured bunnies before you start - Snowball, Hazel, Smokey, Honey, Blossom, and Midnight. Your choice is shown next to your name on the leaderboard, and you can switch bunnies between rounds.

## Leaderboard

After each round you can add your score to the leaderboard, with your chosen bunny shown next to your name and the board ranked by score. Runs played on hard mode carry a 🔥 next to the name.

Note the current limitation: the leaderboard is **local to your session only**. Scores are held while the page is open but reset on reload, and they are **not shared between players or devices** yet. Persistent, shared scoring is the next thing on the roadmap (see below).

## Project structure

```
.
├── index.html        # the entire game (markup, styles, and JS)
└── assets/
    └── sketch.jpg    # the original sketch
```

## Running locally

No build step and no server required - just open the file:

```
open index.html
```

## Deploying

Deploys to [Netlify](https://www.netlify.com/) as a static site. Connect the repo (or drag the folder into Netlify Drop) - no build command required.

## Roadmap

- **Persistent, shared leaderboard.** Replace the session-only board with server-side storage via a small Netlify Function backed by [Netlify Blobs](https://docs.netlify.com/blobs/overview/), so scores persist and every player sees the same board.

## Tech notes

- **Rendering:** HTML Canvas. The bunny, the farmer, and the maze are drawn as vector shapes, so bunnies can be tinted any colour.
- **Movement:** tile-locked and frame-rate independent - the bunny steps toward the next tile centre and is clamped so it can never overshoot, which keeps wall collisions and carrot pickups accurate even on lower-framerate devices. The farmer uses the same stepping, but his turns are chosen by the chase AI rather than the player.
- **Chase AI:** a breadth-first flood fill from the bunny's tile gives every tile its step distance; at each tile centre the farmer walks toward whichever open neighbour is closest, never doubling back unless it is the only way out, and taking a random turn ~18% of the time so he is beatable. The distance field is recomputed only when the bunny changes tile.
- **Audio:** a procedurally generated background loop plus sound effects, all synthesised at runtime with the Web Audio API (no audio files). Toggle with the speaker button.

---

Made for fun ❤️
