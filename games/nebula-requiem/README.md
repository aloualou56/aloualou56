# Nebula Requiem

A roguelike bullet-hell space shooter in a single HTML file. Open `index.html` in a modern browser to play; there is no build step.

The only network requests are the Tailwind CSS play CDN and Google Fonts. Every ship, nebula, particle, sound effect and music track is generated at runtime with Canvas 2D and the Web Audio API. If either CDN is unreachable the game still runs on its own CSS and fallback fonts.

## Controls

| Action | Keyboard / mouse | Gamepad | Touch |
| --- | --- | --- | --- |
| Move | WASD / arrows | Left stick / D-pad | Drag left half |
| Aim | Mouse (auto-aims when idle) | Right stick | Drag right half |
| Fire | Auto-fire (toggle in Settings), or hold click / J | RT | Auto |
| Phase dash | Space / Shift / right-click | A | Dash button |
| Nova bomb | E / K | B | Nova button |
| Overdrive | Q / L (when flux is full) | X | Flux button |
| Pause | Esc / P | Start | II button |

## What's in a run

- **Sectors:** four waves, then a guardian. Each fallen guardian adds a sector mutator; after the fourth, the loop restarts as Ascension with tougher hostiles.
- **Guardians:** Helix Cantor (rose curves, double helices, Cantor-set walls), Lissajous Leviathan (a follow-the-leader serpent on a Lissajous path), Fractal Seraph (Koch snowflakes, phyllotaxis spirals, rotating lances) and Entropy Engine (a 4-D tesseract projection, Lorenz-attractor bullet swarms).
- **Grafts:** 24 in-run perks across four rarities, drafted on level-up, with rerolls.
- **Hangar:** stardust from each run buys 11 permanent refits and two extra hulls. Progress is saved to `localStorage`.

## Engine notes

The script is organised into numbered sections (see the map in the file header):

- Fixed 120 Hz simulation with an accumulator and spiral-of-death guard, plus hit-stop and slow-motion time scaling.
- One opaque canvas: domain-warped fBm nebula, three parallax star layers, a demoscene plasma field, a 2-D lighting grid, a mass-spring "spacetime lattice", then entities.
- Post-processing in pure Canvas 2D: downsample-chain bloom and radial chromatic aberration via channel splitting.
- Pooled particles (sparks, embers, smoke, polygon shards, shockwaves, lightning, afterimages), and pooled bullets with composable behaviours.
- A declarative collision matrix over a spatial hash, using swept-circle, capsule, arc and annulus tests.
- An adaptive quality monitor that steps render resolution and effects down when frame time stays above 21 ms.
