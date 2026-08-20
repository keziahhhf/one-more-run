<div align="center">

# ⚡ ONE MORE RUN

### A neon cyberpunk endless‑runner built for one purpose: making you say *"okay, one more run."*

[![Play Now](https://img.shields.io/badge/▶_PLAY-index.html-ff2d95?style=for-the-badge)](./index.html)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Canvas](https://img.shields.io/badge/Canvas_API-0ff0fc?style=for-the-badge)
![No Backend](https://img.shields.io/badge/Backend-None_needed-a855f7?style=for-the-badge)

**RUN → DODGE → COLLECT → COMBO → RISK → DIE → HIGH SCORE → INSTANT RESTART**

</div>

---

## 🎮 What is this?

**One More Run** is a single-file, zero-dependency, browser-based neon arcade endless runner. Your glowing energy orb auto-runs forward through a procedurally generated obstacle course. You steer left and right to dodge, chain coins and near-misses into massive combos, and gamble your run on **Risk Mode** — a high-speed, high-reward state that can double your score or end your run in an instant.

No install. No backend. No loading screen. Open `index.html` and you're playing in under a second.

## 🕹️ Controls

| Platform | Input |
|---|---|
| Desktop | `←` `→` Arrow keys or `A` `D` |
| Mobile / Tablet | Drag or swipe left/right |
| Risk Mode | Tap the risk meter (or `Space`) once it's full |

## ✨ Signature Mechanics

- **🔥 Combo System** — coins, dodges, and near-misses chain into a rising score multiplier, with glow, particle bursts, floating text, and UI scaling to match the intensity.
- **✨ Perfect Dodge** — skim an obstacle at the last possible instant and get rewarded with brief slow-motion, a screen flash, camera shake, a particle burst, and a big score bonus. It's the mechanic the whole game is built around.
- **⚡ Risk Mode** — burn built-up energy to go faster, multiply your score, and double coin value — while obstacles get more dangerous and one hit ends the run. Constant tension between *safe score* and *huge risky score*.
- **🧩 Procedural Generation** — nine distinct obstacle pattern types (zigzags, narrow gaps, moving gates, risky-reward corridors, alternating gates, speed sections...) are stitched together endlessly, with difficulty that ramps smoothly and never generates an impossible pattern.
- **🎨 Garage** — spend earned coins on purely cosmetic unlocks: orb colors, particle trails, glow styles, and death effects. Zero pay-to-win, all style.
- **🏆 12 Achievements** — tracked and saved locally, from *First Run* to *Risk Master*.

## 🛠️ Built With

`HTML5` · `CSS3` · `JavaScript (ES6, no frameworks)` · `Canvas 2D API` · `Web Audio API` · `localStorage`

No build step, no bundler, no npm install. It's one HTML file with inline `<style>` and `<script>`.

## 🚀 Run It

```bash
# Clone it
git clone https://github.com/<your-username>/one-more-run.git
cd one-more-run

# Just open it — no server required
open index.html      # macOS
start index.html      # Windows
xdg-open index.html   # Linux
```

Or use any static file server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

Or **[play it directly](./index.html)** by downloading and double-clicking.

## 📁 Project Structure

```
one-more-run/
├── index.html          # The entire game — markup, styles, and logic
├── README.md           # You're reading it
├── PROJECT_STORY.md     # Devpost / hackathon write-up
└── LICENSE
```

## 🧠 How It Works (short version)

- A single `requestAnimationFrame` loop drives simulation and rendering together, targeting 60 FPS.
- The world is 3-laned; obstacles and coins are generated as **patterns** (single blockers, zigzags, moving gates, risky-reward corridors, etc.) spawned ahead of the player and swept away once passed — nothing accumulates indefinitely, keeping memory and draw calls flat.
- Depth is faked with a simple perspective function that maps a "distance ahead" value to screen Y position and scale, so obstacles grow as they approach.
- Combo, Risk Mode, and Perfect Dodge state all feed into one `multiplier` value that the scoring loop reads every frame — one number, many systems.
- All audio is synthesized on the fly with the Web Audio API (oscillators + gain envelopes) — there are no audio files to load, and if `AudioContext` is unavailable the game just plays silently instead of breaking.
- Progress (best score, coins, cosmetic unlocks, achievements) persists via `localStorage` — no account, no server, no backend.

## 🗺️ Roadmap Ideas

- [ ] Daily seeded runs / leaderboard
- [ ] Additional obstacle archetypes and biome-based visual themes
- [ ] Controller support
- [ ] Optional cloud save

## 📄 License

MIT — see [LICENSE](./LICENSE).

---

<div align="center">

**Made for the BTT Web Game Jam · Summer 2026**

*How far can you go?*

</div>
