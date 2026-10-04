# 🏏 Cricket Hotseat Sprint

A fast, one-tap cricket arcade game you play **hotseat-style** — pass the phone around and see who can run the furthest before getting out.

Built as a single, self-contained `index.html` file. No build step, no dependencies, no internet required.

---

## 🎮 What is it?

You control a cricket ball sprinting across the pitch. Wickets, bats and bottles fly at you — **jump over them** to keep your run alive. Every metre counts as a run, and clearing an obstacle gives you a bonus. Hit one and you're **out**.

It's a *hotseat* game: set how many players are playing (2–6), and each person takes one turn. When everyone has batted, the scoreboard shows who won. 🏆

## 🕹️ How to play

1. Open `index.html` in any modern browser (or use the live link below).
2. Choose the **number of players** (2–6) with the slider.
3. Press **START MATCH**.
4. **Jump** to dodge obstacles:
   - 📱 **Tap** anywhere on the screen, or
   - 🖱️ **Click**, or
   - ⌨️ Press **Space**, **↑** or **W**
5. When you hit an obstacle you're out — hand the device to the next player and press **READY PLAYER N**.
6. After the last player, press **VIEW SCOREBOARD** to see the final standings.

**Scoring:** 1 metre = 1 run, plus a **+5 bonus** for each obstacle you clear. Highest score wins.

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

- 🎯 One-tap / one-key controls — instantly playable on phone or desktop
- 👥 Hotseat multiplayer for 2–6 players with a final scoreboard
- 🏏 Cricket-themed obstacles: stumps, bats and bottles
- 🌤️ Animated sky, drifting clouds, pitch stripes and dust particles
- 📈 Speed ramps up the longer you survive
- 📱 Fully responsive — works on any screen size
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
