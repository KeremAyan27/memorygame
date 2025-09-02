# Memory Match – Animal Cards

A lightweight memory game built with vanilla JavaScript. Cards are generated dynamically; each card’s **front** is an animal-specific SVG, while the **back** uses a shared SVG. The game includes scoring, persistent history, and subtle effects.

## Features

* Dynamic deck creation from a configurable `animals` array
* Flip animation and match logic (`.flipped`, `.has-match`)
* Scoring: starts at 0, +20 for a correct pair, −5 for a wrong pair
* Scoreboard with Current, Best, and Last 3 scores (persisted via `localStorage`)
* Confetti feedback on each match and on game completion
* No build step; runs in any modern browser

## Tech Stack

* HTML5, CSS3
* Vanilla JavaScript

## Quick Start

1. Download or clone the project.
2. Ensure the confetti library is loaded before `app.js`:

   ```html
   <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
   <script src="app.js" defer></script>
   ```
3. Open `index.html` in a browser (or serve with a simple static server).

## Game Rules & Scoring

* Flip two cards per turn.
* If they match, they stay open and you earn **+20**.
* If they do not match, they flip back after a short delay and you lose **−5**.
* The game ends when all pairs are matched.
* On each match a short confetti burst is shown; on win a timed confetti celebration runs.

## Scoreboard & Persistence

* Current score updates live.
* Best and Last 3 scores are read from `localStorage` key `memgame_history`.
* On win, the current score is appended to history; Best is derived from the history.

## Configuration

All configuration is in `app.js`:

* **Animals list**
  Define which animals to include (these are doubled and shuffled to form the deck):

  ```js
  const animals = ["dog","rabbit","monkey","lion","bear","pig","panda","fox","owl","cat"];
  ```
* **SVGs**

  * `BACK_SVG_COMMON`: shared back SVG for all cards.
  * `FRONT_SVGS`: per-animal front SVGs.
    Paste full `<svg>...</svg>` content into the marked template areas.
* **Flip timing**
  `FLIP_BACK_DELAY` controls the delay before mismatched cards flip back.
* **Styling**
  Scoreboard theming via CSS variables in `style.css`:

  ```css
  :root{
    --sb-bg: rgba(255,255,255,0.08);
    --sb-border: rgba(255,255,255,0.18);
    --sb-text: #fff;
    --sb-muted: #cdd3df;
    --sb-accent: #8ef0ff;
  }
  ```

## Implementation Notes

* The board is rendered by JavaScript into `<section class="game__cards"></section>`.
* Matching logic uses a click delegate on the board container and a lock to prevent rapid re-clicks during animations.
* Matched cards receive `.has-match` (kept open and unclickable).
* To prevent SVG ID collisions across duplicated cards, `uniquifySVGIds` adds a unique suffix to `id`, `url(#...)`, and `href="#..."` references per instance.

## Project Structure

```
index.html      # markup; includes scoreboard and game container
style.css       # board, card, and scoreboard styles
app.js          # deck generation, flip logic, scoring, persistence, confetti
```

## Accessibility

* Scoreboard section uses `aria-live="polite"` to announce score changes without disrupting gameplay.

## License

MIT.
