# Documentation - Continuous 2D Movement & Rotational steering

## Direction Vector from Angle
In Godot, to obtain a directional movement vector from an angle in radians:
```gdscript
var direction := Vector2.from_angle(angle)
```

## Continuous Movement Integration
Instead of handling discrete input events, continuous movement updates inside `_physics_process(delta)`:
```gdscript
# Inside MapSimulation tick/update function:
var velocity := Vector2.from_angle(player_angle) * speed * move_input
var target_pos := player_position + velocity * delta
```

## Mapping Position to Grid Cells
To check collisions and triggers against the grid:
```gdscript
var cell_x := int(floor(position.x / tile_size))
var cell_y := int(floor(position.y / tile_size))
var cell := Vector2i(cell_x, cell_y)
```

## Polling Keyboard Inputs
For real-time player inputs:
```gdscript
var turn := 0.0
if Input.is_key_pressed(KEY_A) or Input.is_key_pressed(KEY_LEFT):
    turn -= 1.0
if Input.is_key_pressed(KEY_D) or Input.is_key_pressed(KEY_RIGHT):
    turn += 1.0
```
