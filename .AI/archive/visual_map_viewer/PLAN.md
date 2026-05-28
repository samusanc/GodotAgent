# Technical Plan - Visual Map Viewer & WASD Movement

We will create a map viewer feature.

## Components to Create

1. **`res://level/grid_visualizer.gd`**
   - Static function to iterate through the map grid and spawn colored `ColorRect` tiles under a parent node.
   - Highlights cells belonging to triggers.
   - Max 50 lines.

2. **`res://level/map_viewer.gd`**
   - Glue script for the scene.
   - Loads the map, handles user keyboard input (WASD/Arrows), updates the player icon position, and updates debug text.
   - Max 50 lines.

3. **`res://level/map_viewer.tscn`**
   - Text scene containing Node2D structure with `TileContainer`, `PlayerIcon`, and a `CanvasLayer` containing a `DebugLabel`.

## Execution
- Check script syntax and run test runner.
- Perform a manual check of the scene.
- Push everything.
