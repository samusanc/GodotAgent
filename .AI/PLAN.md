# Technical Plan - 3D Map Viewer & Platform Controller

We will create a 3D level viewer with a playable 3D character and a steering platform.

## Proposed Components

1. **`res://level/grid_visualizer_3d.gd`**
   - Instantiates collidable 3D block meshes for wall tiles ('1') and overlays floor colliders/meshes for walkable tiles ('0').
   - Uses `MeshInstance3D` with `BoxMesh` and `StaticBody3D` for collision.
   - Max 50 lines.

2. **`res://player/player_3d.gd`**
   - Controls a `CharacterBody3D` standing on top of the platform.
   - Listens to W/A/S/D or Arrow keys.
   - Handles gravity and standard walking.
   - Max 50 lines.

3. **`res://level/platform_controller.gd`**
   - Interacts with `MapSimulation`.
   - References the UI buttons for steering.
   - Updates the platform's `AnimatableBody3D` position and rotation in 3D.
   - Max 50 lines.

4. **`res://level/map_viewer_3d.tscn`**
   - 3D environment scene containing lighting, camera, grid visualizer target, the AnimatableBody3D platform, the player CharacterBody3D, and the Control UI buttons.
