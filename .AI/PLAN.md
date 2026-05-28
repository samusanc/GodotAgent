# Technical Plan - Map Parser & Simulation

We will implement a modular, type-safe system to parse grid maps and configs, track player movement, check cell transitability, and detect triggers.

## Components to Create

1. **`res://resources/trigger_data.gd`**
   - Inherits `Resource`.
   - Stores trigger name, start coordinate, and end coordinate.
   - Max 50 lines.

2. **`res://resources/map_data.gd`**
   - Inherits `Resource`.
   - Stores grid dimensions, 1D grid array (`grid`), player start, and triggers.
   - Max 50 lines.

3. **`res://systems/map_parser.gd`**
   - Reusable parser class.
   - Reads a map text file from `res://`, processes the grid and `config:` reference, reads the configuration file, and returns a `MapData` resource.
   - Max 50 lines.

4. **`res://systems/map_simulation.gd`**
   - Reusable class to simulate player position, handle movement commands, block movement on `1` cells, and check trigger overlaps.
   - Max 50 lines.

5. **`res://systems/test_runner.gd`**
   - Headless verification script to load `res://map-example.txt`, parse it, run movements, verify collision blocks, and verify trigger activation.
   - Max 50 lines.

## Copying Map Files
- Move `map-example.txt` and `map-config.json` from the root workspace to `project/` directory so they are loaded as resources (`res://`).
