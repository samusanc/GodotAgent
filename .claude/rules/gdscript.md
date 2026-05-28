---
paths:
  - "**/*.gd"
---

# GDScript Standards

<!-- Loads when Claude reads any .gd file. -->

## Style

- Follow the [official GDScript style guide](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_styleguide.html).
- Indent with **tabs**, not spaces. (Godot default.)
- `snake_case` for variables, functions, file names, signal names.
- `PascalCase` for `class_name` and node names.
- `SCREAMING_SNAKE_CASE` for constants.
- Every script declares `class_name` on line 1 (after `@tool` if present) unless it is an autoload.
- Run `gdformat <file>` before committing. Run `gdlint <file>` to check style.

## Static Typing (Required)

- Type every variable, parameter, and return value. No exceptions.
- Use `@export` with explicit types for inspector-exposed fields.
- Use `: void` on functions that return nothing.

```gdscript
# Correct
var speed: float = 200.0
@export var max_health: int = 100
func take_damage(amount: int) -> void:
    pass

# Wrong
var speed = 200.0
@export var max_health = 100
func take_damage(amount):
    pass
```

## File Layout

Every `.gd` file follows this order. Skip sections that don't apply, never reorder them.

```gdscript
class_name MyThing extends Node

# 1. Signals
signal something_happened

# 2. Constants
const MAX_RETRIES: int = 3

# 3. Exported variables
@export var speed: float = 100.0

# 4. Private variables
var _internal_state: int = 0

# 5. @onready variables
@onready var _sprite: Sprite2D = $Sprite2D

# 6. Built-in callbacks (_ready, _process, _physics_process, _input, ...)
func _ready() -> void:
    pass

# 7. Public methods

# 8. Private methods (prefix with underscore)
```

Keep `_ready()`, `_process()`, `_physics_process()`, and `_input()` as thin orchestrators. Three lines maximum — delegate to named methods.

## Module Classification

Every `.gd` file is either **reusable** or **glue**. Decide which before writing the first line.

### Reusable script

Generic behavior, drop onto any node that needs it, no knowledge of this specific game.

- No `get_parent()`, no hardcoded `$NodePath` to siblings.
- No reading from autoloads or singletons.
- All dependencies arrive via `@export` fields or signal connections set up by a glue script.
- Communicates outward only via signals.
- Lives in `res://systems/` (or `res://addons/` if it's truly project-agnostic).

Examples: `health.gd`, `mover.gd`, `attack.gd`, `state_machine.gd`, `hurtbox.gd`, `spawner.gd`.

### Glue script

Wires reusable systems together for this specific game. Project-specific by design.

- Lives next to the scene it glues (e.g. `player/player.gd`).
- Allowed to know about specific scenes, resources, and autoloads.
- Connects signals between reusable components in its `_ready()`.
- Contains no generic, reusable behavior. If it grows generic logic, extract that logic to `res://systems/`.

Examples: `player.gd`, `wave_director.gd`, `boss_phase_controller.gd`.

> **Target ratio: ~70% reusable, ~30% glue.** If glue is growing fast, it is hiding reusable logic.

## Signals

- Declare signals at the top of the file (section 1 above), before constants.
- Signal names are past-tense `snake_case` verbs: `health_depleted`, `item_collected`, `phase_changed`.
- **Connect signals in code inside `_ready()`**, never via the Godot editor inspector. Editor connections are invisible to code review.
- Disconnect signals when a node is freed if the connection target may outlive it.

## Error Handling

- `assert(condition, "message")` for invariants that should never fail.
- `push_error("message")` for non-fatal errors that need surfacing.
- `push_warning("message")` for expected degraded paths.
- Never swallow errors silently.
- No `print()` calls in committed code. If runtime logging is needed, gate it behind a `const DEBUG: bool = false` constant.
