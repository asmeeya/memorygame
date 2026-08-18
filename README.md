# 3D Memory Game — Flask + Three.js

A browser-based memory (card-matching) game rendered in 3D using **Three.js**, served by a lightweight **Flask** backend, and styled entirely with **Bootstrap 5** (no custom CSS).

![Tech](https://img.shields.io/badge/Flask-000000?logo=flask&logoColor=white)
![Tech](https://img.shields.io/badge/Three.js-black?logo=three.js&logoColor=white)
![Tech](https://img.shields.io/badge/Bootstrap-7952B3?logo=bootstrap&logoColor=white)

## Features

- 🃏 4×4 grid of 3D cards (8 matching pairs)
- 🎮 Click-to-flip interaction using raycasting
- 🔄 Smooth flip animations (no external animation library)
- 📊 Live move counter and match counter
- 🏆 Win banner on game completion
- ♻️ Restart button to reshuffle and replay
- 🎨 Fully responsive UI built with Bootstrap components only

## Tech Stack

| Layer      | Technology         |
|------------|---------------------|
| Backend    | Flask (Python)       |
| Frontend   | HTML, Bootstrap 5    |
| 3D Engine  | Three.js (r128, CDN) |
| Styling    | Bootstrap utility classes only — no internal `<style>` |

## Project Structure

```
project-root/
├── session2/
│   └── app.py              # Flask application entry point
└── templates/
    └── index.html          # Game UI + Three.js game logic
```

> Flask's default `render_template()` looks for templates in a `templates/` folder relative to the app's root path. If `app.py` and `templates/` are not siblings, set `template_folder` explicitly when creating the Flask app.

## Prerequisites

- Python 3.8+
- `pip` (Python package manager)

## Installation

1. Clone or download the project files into the structure shown above.
2. Install Flask:

   ```bash
   pip install flask
   ```

## Running the App

From the directory containing `session2/`:

```bash
cd session2
python app.py
```

The app will start in debug mode. Open your browser and navigate to:

```
http://localhost:5000
```

## How to Play

1. The board loads with 16 face-down cards, each showing a `?` icon.
2. Click any card to flip it and reveal a symbol.
3. Click a second card:
   - ✅ **Match** — both cards stay face-up and are marked as matched.
   - ❌ **No match** — both cards flip back face-down after a short delay.
4. Your **move count** increases with every pair of flips attempted.
5. Match all 8 pairs to win. A banner displays your final move count.
6. Click **Restart** at any time to reshuffle the deck and start a new game.

## Implementation Notes

- **Card textures** are generated dynamically on an HTML `<canvas>` element (for both the card back and each symbol face) and applied as Three.js `CanvasTexture` materials — no external image assets required.
- **Card flipping** is achieved by rotating each card mesh 180° on its Z-axis; a simple `requestAnimationFrame` tween handles the animation without any external animation/tweening library.
- **Click detection** uses Three.js `Raycaster` to determine which card mesh was clicked based on normalized mouse coordinates.
- **Game state** (flipped cards, matched pairs, move/match counts) is managed with plain JavaScript variables inside the inline `<script>` block — no external state management library.
- The scene uses a `PerspectiveCamera` angled above the grid, with ambient and directional lighting for card shading.

## Customization Ideas

- Adjust `GRID_COLS` / `GRID_ROWS` and the `SYMBOLS` array to change board size and difficulty.
- Swap `CanvasTexture` symbols for image textures (e.g., `THREE.TextureLoader`) to use custom artwork.
- Add a timer alongside the move counter.
- Persist best scores using Flask sessions or a small database.

## License

This project is provided as a demo/learning example and free to use or modify.
