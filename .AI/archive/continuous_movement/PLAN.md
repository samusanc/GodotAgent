# Technical Plan - Continuous Movement

We will refactor the player movement mechanics to use continuous decimal positioning, rotation angles, and time-scaled physics.

## Key Changes

1. **`project/map-config.json`**:
   - Add `"speed": 3.0` (in tiles/second, so absolute speed in units/second is `speed * tile_size`).
     Wait, if speed is 3.0 and tile_size is 32.0, the player moves 96.0 units per second.
     If the user says: "if the speed is 1 it moves 1 unit per second, so if a tilemap is size 1 it will move 1 tile per second but if the tile size is 10 it will move only 1 tile each 10 seconds".
     This means `speed` is in units per second. So if speed is 32.0, and tile_size is 32.0, it moves 32.0 units per second (which is 1 tile per second).
     Yes! So speed is in units/second. Let's specify `"speed": 96.0` and `"tile_size": 32.0`.
   - Update `"player_start": [5.5, 1.5]`.

2. **`project/resources/map_data.gd`**:
   - Add `speed` (float) and `tile_size` (float).
   - Make `player_start` a `Vector2` (decimal).

3. **`project/systems/map_parser.gd`**:
   - Read `speed`, `tile_size`, and float array for `player_start`.

4. **`project/systems/map_simulation.gd`**:
   - Implement `player_position: Vector2` and `player_angle: float`.
   - Implement `tick(move_input: float, turn_input: float, delta: float) -> void` to update position and angle with time delta, checking cell collisions.

5. **`project/level/map_viewer.gd`**:
   - Implement `_physics_process(delta)` to poll keyboard inputs and update the simulation.
   - Smoothly update player icon position.

6. **`project/systems/test_runner.gd`**:
   - Update tests to run continuous simulation ticks and verify collision blocks.
