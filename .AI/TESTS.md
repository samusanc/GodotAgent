# Tests - Visual Map Viewer & WASD Movement

Testing strategy.

## Milestone 1: Create GridVisualizer helper
- AI-Friendly:
  - Check syntax:
    `/home/samusanc/Downloads/godot --headless --check-only --script project/level/grid_visualizer.gd`

## Milestone 2: Create MapViewer glue script
- AI-Friendly:
  - Check syntax:
    `/home/samusanc/Downloads/godot --headless --check-only --script project/level/map_viewer.gd`

## Milestone 3: Create MapViewer scene
- AI-Friendly:
  - Confirm the `.tscn` file exists.

## Milestone 4: Verification & Push
- AI-Friendly:
  - Run the test suite:
    `/home/samusanc/Downloads/godot --headless --script res://systems/test_runner.gd`
- Human-Only:
  - Run the scene inside Godot Editor visually: press WASD keys and check player movement, walls collision block, and trigger activation messages overlaying the canvas.
