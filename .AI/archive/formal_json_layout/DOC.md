# Documentation - JSON Parsing in Godot 4.x

To read and parse a formal JSON file in Godot 4.x:

```gdscript
var file := FileAccess.open(path, FileAccess.READ)
if file:
    var json_text := file.get_as_text()
    var data = JSON.parse_string(json_text)
    if data is Dictionary:
        # Access parameters safely, e.g. data["player_start"]
```

## JSON Data Extraction
- Array of coordinates: `var start_arr = data.get("player_start", [0, 0])`
- Construct Vector2i from array: `var start_pos = Vector2i(int(start_arr[0]), int(start_arr[1]))`
- Triggers array:
  ```gdscript
  var triggers_arr = data.get("triggers", [])
  for trig_dict in triggers_arr:
      var name = trig_dict.get("name", "")
      var start = Vector2i(trig_dict["start"][0], trig_dict["start"][1])
      var end = Vector2i(trig_dict["end"][0], trig_dict["end"][1])
  ```
