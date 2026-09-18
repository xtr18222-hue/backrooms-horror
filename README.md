# The Backrooms — 3D Horror

A fully browser-playable 3D Backrooms horror game, built with **pure HTML5, CSS3 and vanilla JavaScript**, rendered with **Three.js** (loaded from CDN — no build step, no npm install).

> *"If you're not careful and you noclip out of reality in the wrong areas, you'll end up in the Backrooms..."*

## Play

Just open `index.html` in any modern desktop browser (Chrome, Firefox, Edge). No server required.

Three.js is fetched at runtime from a CDN (with an automatic fallback). An internet connection is needed on first load.

## What's in it

- **3 procedurally-generated levels** — Level 0: The Lobby (mono-yellow), Level 1: Habitable Zone (concrete grey), Level 2: Piped Dreams (dark red), each with its own palette, fog density, maze size and difficulty.
- **Endless maze each run** — recursive-backtracker generation plus extra loop openings, rooms and pillars; no two runs are identical.
- **The Smiler** — a grinning entity that stalks you through the dark. It lurks and stares while you're in the light, and hunts when you're not. It hunts harder as your sanity cracks.
- **Sanity system** — standing in darkness drains it; light restores it. At low sanity you hear whispers and your heartbeat, the world distorts, and **false smilers** (hallucinations) appear in the fog — look directly at one and it vanishes.
- **Flashlight + battery** — the light keeps you safe and keeps the Smiler at bay, but the battery drains. Find batteries.
- **Almond Water** — collect enough on each level to open the exit; extras can be thrown (Q) as a pulse that **stuns the Smiler** for a few seconds.
- **Synthesized audio** — the entire soundscape (fluorescent mains hum, drone, whispers, footsteps, heartbeat, jumpscare stinger) is generated live via the Web Audio API. **Zero audio files.**
- **Zero image files** — every texture (yellow wallpaper, carpet, ceiling panels, glow sprites) is procedurally drawn on canvas.
- **Minimap** with objectives, smiler blips and exit marker; vignette, head-bob, crouch/sprint with stamina, and pointer-lock mouselook.

## Controls

| Input | Action |
|---|---|
| Mouse | Look (pointer lock) |
| W A S D | Move |
| Shift | Sprint (uses stamina) |
| Ctrl | Crouch |
| F | Flashlight toggle |
| Q | Throw Almond Water (stuns the Smiler) |
| P / Esc | Pause |
| M | Mute audio |

## Objective

Find the required number of **Almond Water** bottles on each level — the exit door unlocks once you have them all. Reach the exit to descend deeper. Survive all three levels to escape. Don't let the Smiler catch you, and don't let your sanity hit zero for too long.

## Tech

- Single `index.html` — everything is in one file.
- Three.js r160 via CDN (`unpkg`, auto-fallback to `jsdelivr`).
- No build tools, no bundler, no package manager, no external assets.

## Project layout

```
backrooms-horror/
├── index.html      # the entire game (~1,500 lines)
├── README.md
├── LICENSE         # MIT
└── .gitignore
```

## License

MIT — see [LICENSE](LICENSE).
