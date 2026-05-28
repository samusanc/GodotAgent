# Documentation - Godot Project Structure Standards

Godot recommends organizing files by **feature** rather than by **type** for gameplay entities (e.g., keeping a player's scene, script, and local textures inside `res://player/`), while keeping global, shared, or raw asset files in centralized folders (e.g., `res://shared/` or `res://assets/`).

## Centralized Folders vs. Feature-Based Folders

- **Feature-Based folders**: A self-contained folder containing everything unique to that entity. E.g., `res://enemy/` contains `enemy.tscn`, `enemy.gd`, and any textures specific to the enemy. This makes entities modular and easily portable.
- **Centralized Shared folders**: For cross-feature assets used by multiple components. E.g., a shared wood texture, a generic impact sound, or custom global shaders are kept in `res://shared/` subdirectories.
