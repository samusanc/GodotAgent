# Project Context

This is the canonical project context for the Godot 4.x project (GDScript only).

## Architecture & Folder Structure

The project code and scenes reside in the `project/` directory (`res://`).
The standard folders are structured as follows:
- `res://systems/` - Reusable Lego-brick scripts (project-agnostic).
- `res://autoload/` - Global managers (small, specialized, < 50 lines).
- `res://resources/` - Custom Resource types and `.tres` data files.
- `res://shared/` - Cross-feature assets:
  - `res://shared/sprites/` - Gameplay images and textures.
  - `res://shared/audio/` - Sound effects and background music.
  - `res://shared/fonts/` - UI text fonts.
- `res://level/` - Level features, setups, and level scenes.
- `res://player/` - Player logic, assets, and scenes.

## Map Parsing & Simulation System

A system to load, parse, and simulate grid-based movement and triggers.

### Configuration Format (JSON)
The map configurations are stored as formal JSON under `res://map-config.json` (or similar name matching the reference in the map file).
Example schema:
```json
{
  "player_start": [0, 0],
  "triggers": [
    {
      "name": "trigger1",
      "start": [5, 4],
      "end": [5, 6]
    }
  ]
}
```

### Custom Resources
- **`TriggerData`** (`res://resources/trigger_data.gd`): Stores trigger name, start coordinate, and end coordinate. Includes `contains_cell(cell)` boundary checking.
- **`MapData`** (`res://resources/map_data.gd`): Stores grid dimensions, 1D grid representation (1 for non-walkable blocks, 0 for walkable cells), player start position, and list of `TriggerData`. Includes bounds and cell lookup helpers.

### Reusable Systems
- **`MapParser`** (`res://systems/map_parser.gd`): Reads map `.txt` files containing grid data and config file paths, parses the formal JSON configurations, and returns a populated `MapData` resource.
- **`MapSimulation`** (`res://systems/map_simulation.gd`): Manages player movement inside the grid, prevents moving onto `1` cells, and emits signals for player movement and trigger activation.
