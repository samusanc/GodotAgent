# Tests - UI Layout Fix & Backward Movement

Testing strategy.

## Milestone 1: Refactor UI Scene Layout
- AI-Friendly:
  - Verify that the `map_viewer_3d.tscn` file exists.

## Milestone 2: Update PlatformController
- AI-Friendly:
  - Check GDScript syntax:
    `/home/samusanc/Downloads/godot --headless --check-only --script project/level/platform_controller.gd`

## Milestone 3: Verification
- AI-Friendly:
  - Run the test suite:
    `/home/samusanc/Downloads/godot --headless --script res://systems/test_runner.gd`
- Human-Only:
  - Run the 3D scene.
  - Verify the debug panel (bottom-left) and the button steering pad (bottom-right) appear correctly on screen.
  - Verify clicking and holding "Down" moves the platform backward.
