# Configuration & Persistence

## File Locations

| Data | Path | Writable at runtime? |
|---|---|---|
| Project defaults | `res://data/defaults.cfg` | No (read-only — shipped with build) |
| User settings | `user://settings.cfg` | Yes — by `SettingsManager` autoload only |
| Save files | `user://saves/slot_<n>.save` | Yes — by `SaveManager` autoload only |
| Secrets | env vars at startup | Never read from `res://` |

`res://` is read-only in exported builds. Always write to `user://`.

## Access Rules

- **Exactly one autoload owns reads and writes for each config file.** No other script opens a config file directly.
- Reading config goes through the manager: `SettingsManager.get_volume()`, never `ConfigFile.new().load(...)` elsewhere.
- Writing config goes through the manager: `SettingsManager.set_volume(v)`, which handles validation, persistence, and any signals.

## Loading Order

1. At startup, the relevant manager autoload loads `res://data/defaults.cfg`.
2. It then merges values from `user://settings.cfg` if it exists.
3. If a user value is invalid, the manager logs a warning with `push_warning()` and falls back to the default.

## Secrets

- API keys and external service credentials never appear in `res://`. They cannot — `res://` ships with the build.
- Load secrets from environment variables at startup. If a required var is missing, fail loudly at startup, not later.
- Document every required env var in `README.md`.
- Never log secret values. Never include them in error messages.

## Save Data

- Treat save data as untrusted input. Validate every field on load.
- Save files use Godot's `ConfigFile` or `FileAccess` with explicit format (e.g. JSON), not `var_to_str` / `str_to_var` (which can execute arbitrary code via `Object`).
- Include a `version` field in save data. On load, branch on it and migrate forward.
- Never crash on a corrupted save. Log, back the file up to `user://saves/corrupted/`, and start fresh.
