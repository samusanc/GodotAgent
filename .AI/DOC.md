# Documentation - Godot 4 UI Anchoring & Layouts

To ensure Control nodes stay visible across different window sizes and resolutions, they must use Godot's anchor properties instead of absolute coordinates.

## Anchor Presets

- **Bottom-Left (Preset 2)**:
  ```gdscript
  anchor_left = 0.0
  anchor_top = 1.0
  anchor_right = 0.0
  anchor_bottom = 1.0
  grow_vertical = 0 # grows upwards
  ```
- **Bottom-Right (Preset 3)**:
  ```gdscript
  anchor_left = 1.0
  anchor_top = 1.0
  anchor_right = 1.0
  anchor_bottom = 1.0
  grow_horizontal = 0 # grows leftwards
  grow_vertical = 0 # grows upwards
  ```

## Offsets relative to Anchors
When anchors are set to a corner, the `offset_*` properties are relative to that corner. E.g., for bottom-right:
- `offset_left = -220.0` (starts 220 pixels left of the right edge)
- `offset_top = -140.0` (starts 140 pixels above the bottom edge)
- `offset_right = -20.0` (ends 20 pixels left of the right edge)
- `offset_bottom = -20.0` (ends 20 pixels above the bottom edge)
This guarantees a margin of 20 pixels from the corner.
