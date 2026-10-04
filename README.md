# 🏏 Cricket Hotseat Sprint

A fast, **timing-based cricket batting arcade game** you play *hotseat-style* — pass the phone around and see who can score the most runs.

Built as a single, self-contained `index.html` file. No build step, no dependencies, no internet required.

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
👉 Live demo: _add your GitHub Pages / hosting link here_

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
