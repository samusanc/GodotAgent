---
paths:
  - "**/*.gd"
  - "**/*.tscn"
  - "**/*.tres"
  - "project.godot"
---

# Godot Architecture

<!-- Loads when Claude reads any Godot project file. -->

## The Four Categories

Every piece of code in this project is one of four things. Always know which one you are writing.

| Category | Lives in | Knows about |
|---|---|---|
| **Reusable system** | `res://systems/` | Nothing project-specific |
| **Glue** | Feature folders (`res://player/`, etc.) | Specific scenes, resources, autoloads |
| **Data resource** | `res://resources/` or feature folders | Nothing — it's data |
| **View component** | Inside a scene, next to its glue | The simulation it observes |

If a script doesn't clearly fit one, stop and decide before writing more.

## Scene Structure

- One scene per logical entity. Never bundle unrelated nodes in one scene.
- Scenes must be self-contained: instancing a scene anywhere should work without context.
- **Children never reach up to parents.** No `get_parent()` for logic. Emit a signal and let the parent (glue) react.
- **Siblings never reach across.** Use signals, or `@export var other: NodePath` injected by the glue script that owns both.

## Node Naming

- Node names are `PascalCase` describing **role**, not type.
  - Correct: `HealthBar`, `PlayerBody`, `EnemySpawner`, `AttackTimer`
  - Wrong: `Label`, `CharacterBody2D`, `Node2D`, `Timer`
- A scene's root node is named after the scene file.

## Folder Layout

Group by feature, not by file type. Scene and script share a name and live together.

```
res://
├── systems/              # Reusable Lego bricks (no project-specific code)
│   ├── mover.gd
│   ├── health.gd
│   ├── hurtbox.gd
│   ├── attack.gd
│   └── spawner.gd
├── autoload/             # Global managers — small, specialized, <50 lines each
│   ├── event_bus.gd
│   ├── save_manager.gd
│   └── scene_loader.gd
├── resources/            # Shared Resource data (.tres) and Resource scripts (.gd)
├── player/               # Feature: scene + glue + local data
│   ├── player.tscn
│   ├── player.gd         # glue
│   └── player_stats.tres
├── enemy/
│   ├── enemy.tscn
│   └── enemy.gd
└── shared/               # Cross-feature assets (sprites, audio)
```

## Managers and Autoloads

- **Prefer many small specialized managers over one monolithic `GameManager`.** Build `EnemyManager`, `WaveManager`, `EconomyManager`, `DayNightManager` instead of one god object.
- Each autoload stays under 50 lines. If it grows, split it.
- Autoloads are reserved for truly global concerns: event bus, save system, scene loader, settings, audio bus.
- For cross-system communication, prefer an `EventBus` autoload (signal hub) over direct references — neither system has to know the other exists.

## Data: Treat It as a Database

Game data and game code live in separate places. The data layer is the database; code reads from it.

- **Use custom `Resource` subclasses for all structured data**: stats, item definitions, enemy archetypes, wave configs, balancing numbers.
- Never pass raw `Dictionary` between systems for structured data.
- Every Resource subclass has a `class_name` so it is type-safe.
- Resource files use `snake_case.tres`: `sword_stats.tres`, `wave_01.tres`.
- **Group related data together.** If a designer tunes two numbers in the same balancing pass, they go in the same `.tres`. Do not scatter `move_speed`, `attack_cooldown`, and `damage` across three different scripts.
- **All user-facing text goes through Godot's translation system from day one.** Use `tr("KEY")`. Never hardcode strings. Retrofitting localization is much harder than starting with it.
- **For non-trivial features, design the Resource schema before writing the systems that consume it.**

## Simulation vs. View

- **Simulation**: gameplay state, physics, AI, health, damage, timers. Source of truth.
- **View**: rendering, animations, particles, screen shake, audio, UI updates. Reads simulation.
- **The view reads from the simulation. The simulation never reads from the view.**
- A single script must not contain both. If `enemy.gd` updates position *and* plays the hurt animation, split it.
- The view connects to simulation signals to react; it never polls or pulls.

## Execution Order and Time

- Use `_physics_process(delta)` for simulation (movement, collision, AI, gameplay timers).
- Use `_process(delta)` only for view-layer updates.
- **Never mix simulation and view logic in the same callback.**
- For order-sensitive updates across systems, do not rely on Godot's default node-tree traversal order. Use one of:
  - Autoload order in Project Settings.
  - `process_priority` on nodes (lower runs first).
  - An explicit `TickDriver` autoload that calls subsystems in a defined order.
- Prefer explicit method calls (`combat_system.tick(delta)`) over signals when execution order matters. Signals are great for view reactions; they are dangerous for ordered gameplay updates.

## Physics

- `CharacterBody2D` / `CharacterBody3D` for player and AI movement.
- `RigidBody2D` / `RigidBody3D` only when real physics simulation is part of gameplay.
- `StaticBody` for non-moving collision.
- `Area2D` / `Area3D` for triggers and detection zones.
