# Documentation - Godot 4 3D Physics & Movement

## CharacterBody3D Player Controller
To move a player character in 3D:
```gdscript
var velocity := Vector3.ZERO
var input := Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down")
var dir := (global_transform.basis * Vector3(input.x, 0, input.y)).normalized()
velocity.x = dir.x * speed
velocity.z = dir.z * speed
if not is_on_floor():
    velocity.y -= gravity * delta
move_and_slide()
```

## AnimatableBody3D for Moving Platforms
In Godot 4, `AnimatableBody3D` is the recommended node for physics-controlled moving platforms.
- It automatically handles carrying and rotating `CharacterBody3D` nodes standing on top of it.
- Set its position and rotation in `_physics_process(delta)` to move the platform smoothly in sync with physics:
  ```gdscript
  global_position = target_position
  global_rotation.y = target_angle
  ```

## Dynamic 3D Collision Shapes
To create collidable 3D blocks programmatically:
```gdscript
var static_body := StaticBody3D.new()
var collision := CollisionShape3D.new()
var shape := BoxShape3D.new()
shape.size = Vector3(size, size, size)
collision.shape = shape
static_body.add_child(collision)
# Also add a MeshInstance3D to visualize
```
