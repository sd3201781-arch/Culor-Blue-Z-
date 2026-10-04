# 🏏 Cricket Hotseat Sprint

[![▶ Play now](https://img.shields.io/badge/%E2%96%B6%20Play%20now-live-brightgreen?style=for-the-badge)](https://sd3201781-arch.github.io/Culor-Blue-Z-/)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-live-2ea44f?style=for-the-badge&logo=github)](https://sd3201781-arch.github.io/Culor-Blue-Z-/)
[![Players](https://img.shields.io/badge/players-2%E2%80%936-orange?style=for-the-badge)](https://sd3201781-arch.github.io/Culor-Blue-Z-/)
[![License](https://img.shields.io/badge/license-Unlicense-blue?style=for-the-badge)](LICENSE)

A fast, **timing-based cricket batting arcade game** you play *hotseat-style* — pass the phone around and see who can score the most runs.

Built as a single, self-contained `index.html` file. No build step, no dependencies, no internet required.

---

## ▶️ Play it live

### 👉 **[sd3201781-arch.github.io/Culor-Blue-Z-](https://sd3201781-arch.github.io/Culor-Blue-Z-/)**

No install, no sign-up — just open the link in any browser, on phone, tablet or desktop, and play.

**Cricket Hotseat Sprint** is a **2–6 player, pass-and-play, timing-based cricket batting arcade game**. You tap/press to swing as the ball reaches the green zone on the timing bar — nail it for a six, mistime it and you're bowled. Each player gets 6 balls and 3 wickets; the highest total wins.

> Hosted free with **GitHub Pages**, served straight from the `main` branch of this repo.

---

## 🎮 What is it?

You're the batter. A bowler runs in and delivers the ball — **time your shot** as the ball reaches the green zone on the timing bar:

- 🎯 **Perfect timing** → **SIX!** (6 runs)
- ✅ **Great timing** → **FOUR!** (4 runs)
- 👍 **Good timing** → 2 runs
- 🙂 **Okay timing** → 1 run
- 😬 **Mistimed** → dot ball
- ❌ **Way off** → **BOWLED!** (you lose a wicket)

Each player gets **6 balls** and **3 wickets**. When everyone has batted, the scoreboard shows who won. 🏆

## 🕹️ How to play

1. Open `index.html` in any modern browser (or use the live link below).
2. Choose the **number of players** (2–6) with the slider.
3. Press **START MATCH**, then **START INNINGS**.
4. **Swing** when the ball reaches the green zone:
   - 👆 **Tap** anywhere on the screen, or
   - 🖱️ **Click**, or
   - ⌨️ Press **Space**, **↑**, **W** or **Enter**
5. When your innings ends, hand the device to the next player and press **NEXT: PLAYER N**.
6. After the last player, press **FINAL SCOREBOARD** to see the final standings.

**Scoring:** 6 / 4 / 2 / 1 runs per shot depending on timing. Highest total wins.

## 🚀 How to run it

**Option A — just open it**
Download `index.html` and double-click it. That's it.

**Option B — serve it locally** (optional)
```bash
# from the project folder
python3 -m http.server 8000
# then visit http://localhost:8000
```

**Option C — play online**
👉 Live demo: **[https://sd3201781-arch.github.io/Culor-Blue-Z-/](https://sd3201781-arch.github.io/Culor-Blue-Z-/)** (GitHub Pages, auto-deployed from `main`)

## ✨ Features

- 🎯 **Timing-based batting** — a clear timing bar with six/four/run zones
- 🥇 **Hotseat multiplayer** for 2–6 players with a final scoreboard
- 🏟️ **Animated stadium** — gradient sky, drifting clouds, a bobbing crowd, mown pitch stripes
- 🏏 **Animated bowler & batsman** — run-up, bat swing, ball trail, dust particles, screen shake
- 🔊 **Sound effects** via the Web Audio API (no audio files needed)
- 📈 **Rising difficulty** — the ball gets faster each delivery
- 📱 **Fully responsive** — works on any screen size, touch or keyboard
- 📦 **Zero dependencies** — one HTML file, works offline

## 🛠️ Tech

Plain **HTML + CSS + JavaScript** with the HTML5 `<canvas>` 2D API. No frameworks, no libraries, no build tools.

## 📁 Project structure

```
.
├── index.html   # the entire game
├── README.md    # this file
└── LICENSE      # The Unlicense (public domain)
```

## 📜 License

Released under **The Unlicense** — see [LICENSE](LICENSE). Free to use, modify and share.
