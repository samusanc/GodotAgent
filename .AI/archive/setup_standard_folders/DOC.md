# Folder Layout Documentation

As specified in `GEMINI.md` and `.gemini/rules/godot-architecture.md`, the standard layout inside the Godot project is:

- `res://systems/` - Reusable Lego-brick scripts (no project-specific code, e.g., `health.gd`, `mover.gd`).
- `res://autoload/` - Global managers (small, specialized, < 50 lines, e.g., `event_bus.gd`).
- `res://resources/` - Shared Resource data (`.tres`) and Resource scripts (`.gd`).
- `res://shared/` - Cross-feature assets (sprites, audio, fonts).
- `res://<feature>/` - Feature folders containing scene + glue script + local data (e.g., `res://player/player.tscn`, `res://player/player.gd`).

To prevent Git from ignoring empty folders, we will create a placeholder `.gitkeep` file in each directory.
