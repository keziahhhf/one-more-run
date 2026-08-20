# ONE MORE RUN — Project Story

## 💡 Inspiration

The best arcade games share one trait: the moment you die, your hand is already reaching for the restart button before your brain has finished processing "game over." Think *Downwell*, *Subway Surfers*, *Geometry Dash*, *Crossy Road* — games with almost no menu friction between failure and another attempt, where the loss itself feels like fuel instead of punishment.

We wanted to chase that exact feeling inside a browser tab, with zero installs, zero backend, and zero loading time — just a single HTML file you can open and be playing in under a second. The neon/cyberpunk direction came from wanting every frame to feel *alive*: glow, particles, and motion doing the emotional work that a bigger production would hand off to 3D models and a sound designer.

The name **ONE MORE RUN** is the design brief, not just the title. Every system in the game — the instant restart, the risk/reward tension, the perfect-dodge dopamine hit — exists to shorten the gap between *dying* and *trying again*.

## 🛠️ What it does

One More Run is a neon endless runner where a glowing energy orb auto-runs forward through a procedurally generated obstacle course. The player steers left/right (keyboard or touch) to:

- **Dodge** obstacles spawned from nine distinct procedural pattern types (zigzags, narrow gaps, moving gates, risky-reward corridors, alternating gates, speed sections, and more), with difficulty ramping smoothly over the run.
- **Collect** coins that build combo and currency.
- **Chain combos** from coins and near-misses, raising a live score multiplier with escalating visual feedback.
- **Land Perfect Dodges** — skimming an obstacle at the last possible instant triggers slow-motion, a screen flash, camera shake, a particle burst, and a large score bonus. This became the signature mechanic we built the whole feel of the game around.
- **Gamble in Risk Mode** — once a meter fills, the player can trigger a faster, higher-multiplier, higher-danger state where a single mistake ends the run, forcing a constant choice between *safe score* and *huge risky score*.
- **Progress meta systems** between runs: a Garage of purely cosmetic unlocks (colors, trails, glow styles, death effects) purchased with earned coins, and 12 tracked achievements — all persisted with `localStorage`, no account required.

## 🧱 How we built it

The entire game is **one self-contained HTML file** — inline CSS and vanilla JavaScript, rendered with the Canvas 2D API, with a thin DOM layer on top for menus, HUD, and score screens. No frameworks, no bundler, no build step, no external dependencies beyond the browser itself.

Key architecture decisions:

- **A single `requestAnimationFrame` loop** drives simulation and rendering together, targeting 60 FPS, with delta-time based movement so speed stays consistent regardless of frame rate.
- **Procedural pattern generation**: rather than placing individual obstacles, the spawner emits whole *patterns* (a zigzag, a coin corridor, a risky-reward split path) ahead of the player, each hand-tuned so every generated pattern is guaranteed passable — no impossible RNG deaths.
- **A single `multiplier` value** is the nerve center of the scoring system — combo tier, Risk Mode, and coin value all read and write to it, so the many feel-good systems stay coherent instead of stacking into confusing math.
- **Synthesized audio**: every sound effect (coin pickup, combo tick, perfect dodge, risk activation, death, high score) is generated on the fly with the Web Audio API using oscillators and gain envelopes — there are no audio files to fetch, and if `AudioContext` is blocked or unavailable the game simply plays silently rather than breaking.
- **Perspective-faked 3D**: obstacles and coins carry a "distance ahead" value that's mapped to screen Y-position and scale each frame, giving a pseudo-3D runway effect entirely in 2D canvas space, with cheap parallax stars and neon rail lines layered behind it.
- **Persistence** via `localStorage` for best score, best combo, total runs, cosmetic unlocks, and achievement state — enough meta-progression to reward repeat play without needing any server.

## 🧗 Challenges we ran into

- **Making "near miss" feel fair, not random.** Perfect Dodge needed a collision window generous enough to feel earned and skill-based, not luck-based — this took several passes of tuning the hitbox-vs-near-miss thresholds so it rewards precision without punishing normal dodging.
- **Balancing Risk Mode as a real decision, not a strict upgrade.** Early versions made Risk Mode purely beneficial, which killed the tension. The final version raises both the reward *and* the danger simultaneously (faster obstacles, tighter margins) so it stays a genuine bet.
- **Never generating an impossible pattern.** With nine procedural pattern types and increasing difficulty, guaranteeing every generated segment always leaves a passable lane required constraining the pattern generator's randomness rather than letting lanes block fully at random.
- **Keeping a single HTML file performant.** With everything — game logic, rendering, UI, audio synthesis — in one file and one render loop, avoiding unnecessary DOM writes every frame (only updating text/opacity when values actually change) was essential to hitting 60 FPS smoothly, especially on mobile.
- **Mobile input without fighting the browser.** Getting drag/swipe steering to feel as responsive as arrow keys, while also preventing the page from scrolling or bouncing during play, took careful `touch-action` and event-handling work across iOS and Android quirks.

## 📚 What we learned

- How much *game feel* comes from layering several small, cheap effects (screen shake, particle bursts, brief slow-motion, UI scale pulses) rather than any single big system — the sum is far more satisfying than any one part.
- That procedural generation is as much about *constraint design* as randomness — the fun comes from bounded unpredictability, not raw chaos.
- How far the Web Audio API can carry a project's audio needs without a single sound file, and how important graceful audio degradation is for a zero-dependency browser game.
- That an addictive loop is really a *loop of tiny promises* — one more coin, one more combo tick, one more dodge — each one cheap enough for the player to always feel like the next attempt is worth it.

## ➡️ What's next for ONE MORE RUN

- Daily seeded runs with a shareable leaderboard
- New biome-based visual themes and additional procedural pattern archetypes
- Gamepad/controller support
- Optional cloud save for cross-device progression
