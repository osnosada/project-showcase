# Minesweeper Rogue (扫雷地牢)

A Roguelike minesweeper game that blends traditional minesweeper reasoning with dungeon-crawling progression, inspired by *Soul Knight*'s room structure and classic minesweeper mechanics.

## Core Mechanics

| Mechanic | Description |
|----------|-------------|
| **IQ Damage System** | Getting hit reduces IQ instead of HP; IQ reaches 0 = game over — a humorous Roguelike twist |
| **Chain Explosions** | Stepping on a mine triggers cascading chain reactions across adjacent tiles |
| **Goal-Oriented** | Navigate from start to exit to clear a level — no need to sweep the entire board |

## Game Systems

### Talent System (Passive — chosen at start of each run)
- **Chess Master** — Movement pattern changes to chess Knight, allowing L-shaped moves
- **Lucky Star** — First dangerous step avoids the mine; the mine disappears from the board
- **Detector** — Reveal numbers in a 3×3 area around the mouse cursor

### Skill System (Active — acquired during gameplay)
| Skill | Effect |
|-------|--------|
| Brain Tonic (脑白金) | Restore 20 IQ points |
| Blast Suit (防爆服) | Next mine explosion deals 0 IQ damage |

### Menu & Settings
- Level selection screen
- Volume control and fullscreen toggle
- In-game tutorial with basic instructions

## Tech Stack

| Category | Technology |
|----------|-----------|
| Language | Python 3.8+ |
| Game Framework | Pygame 2.5+ |
| Architecture | Modular (core / entities / ui / utils) |
| AI Assistance | Developed with AI coding tools |

## Project Structure

```
minesweeper_rogue/
├── main.py              # Game entry point & menu
├── src/
│   ├── core/            # Game controller, grid logic, level manager
│   ├── entities/        # Player, items, mines
│   ├── ui/              # Renderer, HUD
│   └── utils/           # Audio, settings, tutorial, constants, helpers, fonts
├── assets/              # Fonts, images, sounds
└── data/                # Level configs, balance, saves
```

## Controls

| Key | Action |
|-----|--------|
| WASD / Arrow Keys | Move character |
| Mouse Left Click | Click-to-move / select area for Detector |
| Space | Use selected skill |
| 1–5 | Select skill slot |
| ESC | Pause / Resume |

## My Role

**Sole Developer** — Designed and implemented the entire game, including:
- Core minesweeper mechanic with IQ damage system and chain explosions
- Roguelike room-based level progression
- Talent system (3 passive talents) and skill system (2 active skills)
- Menu system with level selection, settings, and tutorial
- All game logic, rendering, and UI

## Development Notes

- Developed over Feb–May 2026 as a personal project with AI-assisted coding
- The game is a functional demo — core gameplay loop (talent selection → room exploration → skill usage → level completion) is fully playable
- Some features in the original roadmap (more talents/skills, Boss battles, shop, achievements, save system, full art assets) are not yet implemented

## How to Run

```bash
pip install -r requirements.txt
python main.py
```

Or on Windows: `start.bat`
