# Project Context

This is the canonical project context for the Godot 4.x project (GDScript only).

## Architecture & Folder Structure

The project code and scenes reside in the `project/` directory (`res://`).
The standard folders are structured as follows:

- `res://systems/` - Reusable Lego-brick scripts (project-agnostic).
- `res://autoload/` - Global managers (small, specialized, < 50 lines).
- `res://resources/` - Custom Resource types and `.tres` data files.
- `res://scenes/` - Global or core screens/scenes (e.g. main menu, persistent HUD UI, splash screen).
- `res://shared/` - Cross-feature shared assets:
  - `res://shared/sprites/` - Shared gameplay 2D images and textures.
  - `res://shared/audio/` - Shared sound effects and background music.
  - `res://shared/fonts/` - UI text fonts.
  - `res://shared/models/` - 3D assets, meshes, and 3D models (FBX/OBJ/GLTF).
  - `res://shared/textures/` - 2D/3D images used as textures, normal maps, or noise patterns.
  - `res://shared/materials/` - Pre-configured `.tres` material files (StandardMaterial3D, ShaderMaterial).
  - `res://shared/shaders/` - Custom shader scripts (`.gdshader`).
- `res://level/` - Level features, setups, and level scenes.
  - `res://level/map_viewer.tscn` - Visual scene for testing grid map and player movement.
  - `res://level/map_viewer.gd` - Glue script to update visual representation and handle WASD/Arrow input.
  - `res://level/grid_visualizer.gd` - Helper class to draw colored ColorRect tiles for path, walls, and trigger zones.
- `res://player/` - Player logic, assets, and scenes.

## Map Parsing & Simulation System

A system to load, parse, and simulate grid-based movement and triggers.

### Configuration Format (JSON)
The map configurations are stored as formal JSON under `res://map-config.json` (or similar name matching the reference in the map file).
Example schema:
```json
{
  "player_start": [5.5, 1.5],
  "speed": 96.0,
  "tile_size": 32.0,
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
- **`MapData`** (`res://resources/map_data.gd`): Stores grid dimensions, 1D grid representation (1 for non-walkable blocks, 0 for walkable cells), player start position (decimal Vector2), speed (float), tile_size (float), and list of `TriggerData`. Includes bounds and cell lookup helpers.

### Reusable Systems
- **`MapParser`** (`res://systems/map_parser.gd`): Reads map `.txt` files containing grid data and config file paths, parses the formal JSON configurations, and returns a populated `MapData` resource.
- **`MapSimulation`** (`res://systems/map_simulation.gd`): Manages player movement inside the grid, using continuous decimal-based coordinates (`player_position`) and rotation angles (`player_angle`). Pre-calculates movement vectors relative to steering angles and checks boundaries and grid block collisions based on `floor(pos / tile_size)`.
