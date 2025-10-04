# 🎯 Math Drop Challenge!

An interactive maths game where problems drop from the top of the screen.  
Solve them quickly, keep your lives, and climb the leaderboard!

---

## 📂 Project Structure

- **index.html**  
  Single-file app containing:
  - **HTML** → Screens (Home, Game HUD, Game Over, Leaderboard modal)
  - **CSS** → Layout, gradients, animations, responsive grid
  - **JavaScript** → Game logic (problems, scoring, timers, lives, sound, difficulty, leaderboard)

- **README.md**  
  This file.

No build tools required.

---

## 🕹️ How to Play

1. Open `index.html` in your browser.
2. Pick a **topic** (Addition / Times Tables / Subtraction) and a **level**.
3. Pick a **difficulty** (Easy / Medium / Hard).
4. Answer each problem before it reaches the bottom **or** the timer expires.
5. You have a limited number of **lives** ❤️ (depends on difficulty).
6. A round ends after **10 questions** or when you run out of lives.
7. Scores are recorded locally; high scores and leaderboard entries are saved per mode.

---

## 🎚️ Difficulty Levels

Select on the Home screen (also shown as a pill in the top bar during play). Your choice is remembered.

- 🟢 **Easy** — 5 lives, 15s per question, slower fall
- 🟡 **Medium** — 3 lives, 10s per question, normal fall *(default)*
- 🔴 **Hard** — 2 lives, 7s per question, faster fall

> Difficulty also scales the fall speed; exact values are in the code via `DIFF_SETTINGS`.

---

## 🏆 Leaderboard (Local)

A built-in, **local** leaderboard (using `localStorage`) stores the **Top 10** for each combination of:
- **Topic** (Addition / Times Tables / Subtraction)
- **Level** (e.g., Addition ≤30, 7× table)
- **Difficulty** (Easy / Medium / Hard)

### How it works
- At **Game Over**, if your result qualifies for the Top 10 (by **score desc**, then **faster total round time**), you’ll be prompted to enter a **name/initials**.
- Click **“Save to Leaderboard”** to record it.
- Open the **Leaderboard** from Home or the in-game HUD to browse results (filters at the top).

### Data that is saved
Each leaderboard entry stores:
- `name` (up to 20 chars)
- `score` (out of 10)
- `timeMs` (total time for the round; tie-breaker)
- `date` (unix ms)

> Your last used player name is remembered locally to speed up future saves.

---

## 🖥️ Code Overview

### Screens
- **Home** — Topic cards, levels, difficulty, Leaderboard button  
- **Game** — HUD (score, best score, difficulty pill, lives), timer bar, falling tile with answer input  
- **Game Over** — Final score, best score, optional save area for leaderboard, quick actions  
- **Leaderboard Modal** — Filters + Top 10 table

### Game Mechanics
- **Problem generation**
  - *Addition*: sum ≤ chosen cap (e.g., 30)  
  - *Times Tables*: `[level] × 1..12`  
  - *Subtraction*: no negative results
- **Movement**: frame-rate independent (uses delta time)
- **Timer**: per-question countdown (visual shrinking bar)
- **Lives**: lose one for wrong or missed questions
- **High score**: per mode/level (separate from the leaderboard)

### Accessibility
- Live regions for score and question counter
- Hearts labelled via ARIA with remaining lives
- Inputs labelled for screen readers

---

## ⚙️ Customisation

Open `index.html` and tweak the following sections:

### Difficulty settings
```js
const DIFF_SETTINGS = {
  easy:   { lives: 5, timer: 15000, speedMul: 0.75, label: 'Easy' },
  medium: { lives: 3, timer: 10000, speedMul: 1.00, label: 'Medium' },
  hard:   { lives: 2, timer:  7000, speedMul: 1.50, label: 'Hard' }
};
