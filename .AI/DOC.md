# Documentation - Map Parsing APIs

## File I/O in Godot 4.x

To read a file line-by-line at runtime:
```gdscript
var file := FileAccess.open(path, FileAccess.READ)
if file:
    while not file.eof_reached():
        var line := file.get_line().strip_edges()
        if line.is_empty():
            continue
        # Process line
```

## String Parsing

- Check prefixes: `line.begins_with("config:")`
- Splitting strings: `line.split(" ")` or `line.split(",")`
- Converting to integers: `int(string_val)`
- Vector2i construction: `Vector2i(x, y)`

## Custom Resources

Custom resource scripts must have a `class_name` and inherit from `Resource` to be type-safe:
```gdscript
# trigger_data.gd
class_name TriggerData
extends Resource

@export var name: String = ""
@export var start: Vector2i = Vector2i.ZERO
@export var end: Vector2i = Vector2i.ZERO
```

```gdscript
# map_data.gd
class_name MapData
extends Resource

@export var width: int = 0
@export var height: int = 0
@export var grid: Array[Array] = [] # 2D array of ints: 1 = block, 0 = transitable
@export var player_start: Vector2i = Vector2i.ZERO
@export var triggers: Array[TriggerData] = []
```
*(Note: Godot 4 arrays of arrays can be represented as `Array[Array]`, but since nested typed arrays are tricky in some Godot versions, `Array` or a flattened 1D array of size `width * height` is often safer and easier. Let's use a 1D typed array `Array[int]` of size `width * height`, which can be accessed using `x + y * width`. This is robust and fully supported. Let's export `grid: Array[int]`.)*

## Grid & Collision representation

A custom `MapModel` or `MapSimulation` can track the active map state.
- Is cell transitable: `func is_transitable(cell: Vector2i) -> bool` returns true if cell coordinates are within bounds and the cell value in `grid` is 0.
