# Minesweeper Rogue (扫雷地牢)

A Roguelike minesweeper game that blends traditional minesweeper reasoning with dungeon-crawling progression, inspired by *Soul Knight*'s room structure and classic minesweeper mechanics.

## Core Innovation

| Mechanic | Description |
|----------|-------------|
| **Release-to-Explode** | Players can step on mines safely — they only detonate when the player steps off, enabling strategic probing |
| **Goal-Oriented** | No need to clear the entire board — just navigate from start to exit |
| **IQ Damage System** | Getting hit reduces IQ instead of killing the player; IQ reaches 0 = game over |
| **Chain Explosions** | Mine blasts (1–2 tile radius) trigger cascading chain reactions |
| **Knockback** | Explosions push the player in the opposite direction |

## Game Systems

### Talent System (Passive)
- **Lucky Star** — First move or next step avoids mines; may alter layout
- **Chess Master** — Movement changes to chess-piece patterns (King / Knight / Bishop / Rook)
- **Flash** — Move 2 tiles at once; can dash out of blast range

### Skill System (Active)
| Skill | Rarity | Effect |
|-------|--------|--------|
| Steel Plate | Common | Cover a tile — walkable but hidden |
| Box | Rare | Like Steel Plate but pushable |
| Clone | Epic | Place a phantom on a tile; recall to trigger its effect |
| Detector | Common | Reveal numbers in a 3×3 area |
| Remote Flag | Common | Place/remove flags at range |
| Brain Tonic | Common | Restore 20 IQ |
| Blast Suit | Rare | Next explosion deals 0 IQ damage |

### Room & Level System
- Room layouts from 3×3 to 5×5 (inspired by *Soul Knight*)
- 5 room types: Start, Exit, Normal, Shop, Boss
- Procedurally generated mine layouts with safe zones at start/exit
- Mini-map navigation

### Boss System
- 3 distinct Boss types with phase-based attack patterns
- Attack speed increases as Boss HP drops (3 phases)

### Supporting Systems
- **Save System** — 3 save slots
- **Settings** — Volume, difficulty, key bindings, fullscreen toggle
- **Tutorial** — 11-step interactive tutorial
- **Statistics** — Rooms cleared, mines triggered, IQ lost, steps taken
- **Achievements** — 12 unlockable achievements
- **Shop** — Purchase items between rooms
- **Procedural Audio** — All sound effects generated programmatically (no external audio files needed)

## Tech Stack

| Category | Technology |
|----------|-----------|
| Language | Python 3.8+ |
| Game Framework | Pygame 2.5+ |
| Architecture | Modular MVC (core / entities / ui / utils) |
| Audio | Programmatic synthesis (no external files) |
| Build | PyInstaller (Windows executable) |
| AI Assistance | Developed with AI coding tools |

## Project Structure

```
minesweeper_rogue/
├── main.py              # Game entry point & menu
├── editor.py            # Level editor
├── debug.py             # Debug tools
├── src/
│   ├── core/            # Game controller, grid logic, level manager
│   ├── entities/        # Player, items, mines
│   ├── ui/              # Renderer, HUD
│   └── utils/           # Audio, save, settings, tutorial, achievements,
│                        # shop, boss, stats, particles, animation, fonts
├── assets/              # Fonts, images, sounds
├── data/                # Level configs, balance, saves
└── build/               # PyInstaller output
```

## Controls

| Key | Action |
|-----|--------|
| WASD / Arrow Keys | Move character |
| Left Click | Click-to-move on valid tile |
| Right Click | Place / remove flag |
| F | Flag current tile |
| E | Place clone |
| R | Recall clone |
| Space | Use selected skill |
| 1–5 | Select skill slot |
| ESC | Pause / Resume |

## My Role

**Sole Developer** — Designed and implemented the entire game, including:
- Core "release-to-explode" minesweeper mechanic and chain explosion system
- Roguelike room-based level structure with procedural generation
- Talent & skill system with rarity tiers and cooldowns
- Boss battle system with multi-phase attack patterns
- Procedural audio synthesis engine
- Save, settings, tutorial, achievement, shop, and statistics subsystems
- Particle effects, screen shake, damage numbers, and UI animations

## Development Notes

- Developed over Feb–May 2026 as a personal project with AI-assisted coding
- The game is in v0.1 Alpha — core systems are functional but some features listed in the roadmap (more themes, background music, level editor, full art assets) are not yet implemented
- Known bugs exist; the project serves as a learning exercise in game design and Python development

## How to Run

```bash
pip install -r requirements.txt
python main.py
```

Or on Windows: `start.bat`
