# Project: GodotAgent

<!-- Maintainer notes: this CLAUDE.md is the entry point. Rules in .claude/rules/
     auto-load. Keep this file under 100 lines — it loads on every session. -->

Godot 4.x game project. GDScript only (no C#). `master` is the production branch, `dev` is integration.

## Always-On Project Context

@.AI/PROJECT.md
@.AI/GOAL.md

## Core Rules (read every session)

These are the non-negotiables. Detailed rules live in `.claude/rules/` and load automatically.

- **One responsibility per file. Max 50 lines of code per file.** If a file grows past 50 lines, split it before continuing.
- **Reusable systems and glue code are separate things.** A reusable script (e.g. `health.gd`, `mover.gd`) knows nothing about this specific game. A glue script (e.g. `player.gd`) wires reusable systems together for this game. See `.claude/rules/godot-architecture.md`.
- **Static typing on everything in GDScript.** No untyped variables, parameters, or return values. See `.claude/rules/gdscript.md`.
- **Custom `Resource` types for all structured data.** Never pass raw `Dictionary` between systems.
- **Simulation reads no view, view reads simulation.** Never the reverse.
- **Never commit directly to `master` or `dev`.** Branch from `dev`, PR back to `dev`. See `.claude/rules/git.md`.
- **No `Co-Authored-By` or AI attribution in commit messages.**

## Session Startup

1. `.AI/PROJECT.md` and `.AI/GOAL.md` are imported above and load automatically.
2. Read `.claude/rules/planning.md` to know the workflow for the current goal.
3. Before writing any code, confirm which `.AI/` stage the session is at (`PLAN.md`, `MILESTONES.md`, etc.).

## Verification Commands

- Syntax check a script: `godot --headless --check-only --script <path>.gd`
- Run the project headless (for tests): `godot --headless`
- Format GDScript before committing: `gdformat <path>`
- Lint GDScript: `gdlint <path>`

## Where Things Live

| Path | Contents |
|---|---|
| `res://systems/` | Reusable Lego-brick scripts |
| `res://autoload/` | Global managers (small, specialized) |
| `res://resources/` | Custom `Resource` data files (`.tres`) |
| `res://<feature>/` | Feature folders — scene + glue script + local data live together |
| `user://` | Runtime-writable data (saves, settings). Never written from `res://` |
| `.AI/` | Planning and session context. No code, no assets |
| `.claude/rules/` | Modular rule files. See files there for details |
