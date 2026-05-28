# Technical Plan - UI Layout Fix & Backward Movement

We will refactor the UI anchoring in the 3D scene and add the backward movement controls.

## Plan Details

1. **`project/level/map_viewer_3d.tscn`**:
   - Re-arrange `SteeringPanel` and `DebugLabel` using proper anchors (preset 2 and 3).
   - Add a `BackwardButton` to the `SteeringPanel` Control node tree.
2. **`project/level/platform_controller.gd`**:
   - Reference `BackwardButton` via `@onready var backward_btn: Button = $UILayer/SteeringPanel/BackwardButton`.
   - Update `_physics_process(delta)` to poll `backward_btn.is_pressed()` and decrement `move_input` when pressed (e.g. `move_input -= 1.0`).
   - Check file size limit is kept under 50 lines.
3. **Verification**:
   - Re-check GDScript compilation and run regression tests.
