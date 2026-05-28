# Project: GodotAgent

Godot 4.x game project. GDScript only (no C#). `master` is the production branch, `dev` is integration.

## Always-On Project Context

@.AI/PROJECT.md
@.AI/GOAL.md

## Modular Rules

The following files are imported and form the complete rule set. Run `/memory show` to inspect the full loaded context, or `/memory reload` after editing any rule file.

@.gemini/rules/universal.md
@.gemini/rules/gdscript.md
@.gemini/rules/godot-architecture.md
@.gemini/rules/config.md
@.gemini/rules/planning.md
@.gemini/rules/git.md

## Core Rules (read every session)

The non-negotiables. Detailed rules are in the imports above.

- **One responsibility per file. Max 50 lines of code per file.** Split before continuing past the limit.
- **Reusable systems and glue code are separate things.** A reusable script (`health.gd`, `mover.gd`) knows nothing about this specific game. A glue script (`player.gd`) wires reusable systems together for this game.
- **Static typing on everything in GDScript.** No untyped variables, parameters, or return values.
- **Custom `Resource` types for all structured data.** Never pass raw `Dictionary` between systems.
- **Simulation reads no view, view reads simulation.** Never the reverse.
- **Never commit directly to `master` or `dev`.** Branch from `dev`, PR back to `dev`.
- **No `Co-Authored-By` or AI attribution in commit messages.**

## Session Startup

1. `.AI/PROJECT.md` and `.AI/GOAL.md` are imported above and load automatically.
2. Confirm which `.AI/` stage the current session is at (`PLAN.md`, `MILESTONES.md`, etc.) before writing code.
3. If `GOAL.md` is empty or stale, run the feature workflow (see `.gemini/rules/planning.md`) before touching code.

## Verification Commands

- Syntax check a script: `godot --headless --check-only --script <path>.gd`
- Run the project headless: `godot --headless`
- Format GDScript: `gdformat <path>`
- Lint GDScript: `gdlint <path>`

## Where Things Live

| Path | Contents |
|---|---|
| `res://systems/` | Reusable Lego-brick scripts |
| `res://autoload/` | Global managers (small, specialized) |
| `res://resources/` | Custom `Resource` data files (`.tres`) |
| `res://<feature>/` | Feature folders — scene + glue script + local data |
| `user://` | Runtime-writable data (saves, settings). Never written from `res://` |
| `.AI/` | Planning and session context. No code, no assets |
| `.gemini/rules/` | Modular rule files imported above |

## Cross-Tool Note

To make the same context load in other AI tools (Claude Code, Antigravity CLI, etc.), either symlink `GEMINI.md` ↔ `CLAUDE.md` ↔ `AGENTS.md`, or set `context.fileName` in `.gemini/settings.json`:

```json
{
  "context": {
    "fileName": ["GEMINI.md", "AGENTS.md", "CLAUDE.md"]
  }
}
```
