# Project Context

This is the canonical project context for the Godot 4.x project (GDScript only).

## Architecture & Folder Structure

The project code and scenes reside in the `project/` directory (`res://`).
The standard folders are structured as follows:
- `res://systems/` - Reusable Lego-brick scripts (project-agnostic).
- `res://autoload/` - Global managers (small, specialized, < 50 lines).
- `res://resources/` - Custom Resource types and `.tres` data files.
- `res://shared/` - Cross-feature assets (sprites, audio, fonts).
- `res://<feature>/` - Feature folders (e.g. `res://player/player.tscn`, `res://player/player.gd`).

## Map Parsing & Simulation System

A system to load, parse, and simulate grid-based movement and triggers.

### Custom Resources
- **`TriggerData`** (`res://resources/trigger_data.gd`): Stores trigger name, start coordinate, and end coordinate. Includes `contains_cell(cell)` boundary checking.
- **`MapData`** (`res://resources/map_data.gd`): Stores grid dimensions, 1D grid representation (1 for non-walkable blocks, 0 for walkable cells), player start position, and list of `TriggerData`. Includes bounds and cell lookup helpers.

### Reusable Systems
- **`MapParser`** (`res://systems/map_parser.gd`): Reads map `.txt` files containing grid data and config file paths, parses custom-format `.json` files (containing player start and trigger coordinates), and returns populated `MapData`.
- **`MapSimulation`** (`res://systems/map_simulation.gd`): Manages player movement inside the grid, prevents moving onto `1` cells, and emits signals for player movement and trigger activation.
