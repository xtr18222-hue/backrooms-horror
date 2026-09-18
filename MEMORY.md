# MEMORY.md — The Backrooms 3D Horror

> Read this first when resuming this project.

## What this is

A fully browser-playable 3D Backrooms horror game. Pure HTML5 + CSS3 + vanilla
JavaScript, rendered with Three.js (CDN, r160). Zero build step, zero external
assets — all textures are drawn procedurally on canvas, all audio is synthesized
live via the Web Audio API.

- **Repo:** https://github.com/xtr18222-hue/backrooms-horror (public, MIT)
- **Local path:** `C:\Users\xtr18\Desktop\backrooms-horror`
- **Single file:** everything lives in `index.html` (~1,600 lines).

## How to play / test

Open `index.html` in a modern desktop browser. No server needed (Three.js comes
from a CDN with an automatic jsdelivr fallback, so first load needs internet).

Controls: mouse look (pointer lock), WASD, Shift sprint, Ctrl crouch,
F flashlight, Q throw Almond Water (stuns the Smiler), P/Esc pause, M mute.

## Game design (verified working)

- 3 levels: **Level 0 The Lobby** (mono-yellow), **Level 1 Habitable Zone**
  (concrete grey), **Level 2 Piped Dreams** (dark red). Each has its own
  palette, fog density, maze size, smiler count and speed.
- Maze: recursive-backtracker + extra loop openings + rooms + pillars.
  Regenerated every run. BFS is used for both distance fields and smiler
  pathfinding.
- **Smiler AI states:** `lurk` (stares from the dark, does not approach) ->
  `hunt` (pathfinds to player when the player is in darkness, low on sanity,
  or very close) -> `stunned` (hit by a thrown Almond Water pulse) ->
  `flee` (driven back by sustained light). A stunned/fleeing smiler despawns.
- **Sanity:** drains in the dark, restores in light. Below ~55% -> whispers +
  hiss; below ~50% -> heartbeat; below ~40% -> screen distortion/sway; below
  ~24% -> false smiler hallucinations spawn in the fog ahead and vanish when
  looked at directly. Sanity at 0 for 4s+ = madness death.
- **Win/lose:** collect N Almond Waters on a level to unlock the exit door
  (turns green on the minimap); reach it to advance. All 3 levels = escape.
  Smiler touch = caught death. Sanity 0 for 4s = madness death.

## Testing (how it was verified)

No usable browser automation in this environment (the built-in Chromium fails
to launch; system Chrome runs headless but produces no output — likely
sandboxed). The game was therefore verified headlessly with **Node + a stubbed
DOM/Three.js**, by extracting the main `<script>` and driving the real game
loop for 1000+ frames:

- boot: 0 errors
- menu -> playing
- movement + collision + head-bob
- throw (Q): spare count decrements, pulse stuns smiler
- forced smiler kill -> `dead` state + death overlay shown
- retry -> respawned, back to `playing`
- sanity forced to 0 -> madness death
- exit reached -> level transition
- 0 runtime errors throughout

Also verified against the **real** three.min.js from the CDN: the file parses,
and every `THREE.*` API and instance method the game calls exists in r160.

Known untested path: the actual WebGL rendering (needs a real GPU browser).

## Repo state

- `main` branch, initial commit `76b3d5a`, pushed to GitHub.
- Git identity was set **per-repo** (global identity was empty):
  `xtr18222-hue` / `xtr18222-hue@users.noreply.github.com`.
- `gh` CLI is authenticated as `xtr18222-hue` (scopes: repo, workflow, gist).

## Next features (not yet built)

Sound effects are a natural next step, plus power-ups and a high score — these
were offered but not requested. Suggested order:

1. High score / run timer persistence (localStorage).
2. More smiler variety (different speeds, a ranged "Hound" type).
3. Level 3+ endless mode with a difficulty ramp.
4. Mobile touch controls (the canvas already has touch handlers).
5. Chunked/streaming maze for much larger levels.

## Conventions

- Deliverables are working artifacts, not stubs.
- Keep unrelated features out of scoped requests.
- Update this file as the project evolves; never put secrets here.
