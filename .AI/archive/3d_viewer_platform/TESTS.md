# Tests - 3D Map Viewer & Platform Controller

Testing strategy.

## Milestone 1: Implement GridVisualizer3D
- AI-Friendly:
  - Check script syntax:
    `/home/samusanc/Downloads/godot --headless --check-only --script project/level/grid_visualizer_3d.gd`

## Milestone 2: Implement Player3D Controller
- AI-Friendly:
  - Check script syntax:
    `/home/samusanc/Downloads/godot --headless --check-only --script project/player/player_3d.gd`

## Milestone 3: Implement PlatformController
- AI-Friendly:
  - Check script syntax:
    `/home/samusanc/Downloads/godot --headless --check-only --script project/level/platform_controller.gd`

## Milestone 4: Setup MapViewer3D Scene & Run Tests
- AI-Friendly:
  - Verify that the test runner passes successfully:
    `/home/samusanc/Downloads/godot --headless --script res://systems/test_runner.gd`
- Human-Only:
  - Launch the game inside Godot Editor.
  - Verify 3D player moves on the platform using WASD/Arrow keys.
  - Verify clicking and holding UI screen buttons (Forward, Left, Right) steers the platform smoothly through the 3D maze.
