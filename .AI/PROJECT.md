# Project Context

This is the canonical project context for the Godot 4.x project (GDScript only).

## Architecture & Folder Structure

The project code and scenes reside in the `project/` directory (`res://`).
The standard folders are structured as follows:
- `res://systems/` - Reusable Lego-brick scripts (project-agnostic).
- `res://autoload/` - Global managers (small, specialized, < 50 lines).
- `res://resources/` - Custom Resource types and `.tres` data files.
- `res://shared/` - Cross-feature assets (sprites, audio, fonts).
- `res://<feature>/` - Feature folders (e.g. `res://player/player.tscn`, `res://player/player.gd`).
