# Documentation - Godot 2D Visualization & Inputs

## Input Event Handling
In Godot 4, raw keys can be detected in `_unhandled_input(event)`:
```gdscript
func _unhandled_input(event: InputEvent) -> void:
    if event is InputEventKey and event.pressed and not event.is_echo():
        match event.keycode:
            KEY_W: # Up
            KEY_A: # Left
            KEY_S: # Down
            KEY_D: # Right
```

## Instantiating ColorRect Dynamically
To draw simple blocks on screen:
```gdscript
var rect := ColorRect.new()
rect.size = Vector2(30, 30)
rect.position = Vector2(x * 32, y * 32)
rect.color = Color.GRAY
add_child(rect)
```

## CanvasLayer Debug Text
A `CanvasLayer` allows displaying HUD elements independent of the game camera:
```gdscript
# UILayer (CanvasLayer)
# └── DebugLabel (Label)
$UILayer/DebugLabel.text = "Debug Info"
```
