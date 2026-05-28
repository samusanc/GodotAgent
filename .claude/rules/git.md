# Git & Version Control

<!-- Always-loaded workflow rules. -->

## Branch Structure

```
master   <- production. Protected. PR-only. Never commit directly.
dev      <- integration. Protected. PR-only. All feature branches merge here.
```

This project uses `master`, not `main`. Never assume `main` exists.

## Workflow

Before every commit:

1. Run `git status` — verify the current branch.
2. Run `git pull` — sync with remote.
3. If on `master` or `dev`: **stop**. Branch from `dev` first.
4. For a feature or fix: `git checkout dev && git pull && git checkout -b <type>/<name>`.
5. Open a PR to `dev` when ready.
6. Release: `dev` → `master` via release PR only.

## Branch Naming

Format: `<type>/<short-kebab-description>`

| Type | Use | Example |
|---|---|---|
| `feature/` | New gameplay feature or system | `feature/double-jump` |
| `fix/` | Bug fix | `fix/camera-boundary-clamp` |
| `hotfix/` | Urgent production fix | `hotfix/save-data-corruption` |
| `refactor/` | Restructure without behavior change | `refactor/enemy-state-machine` |
| `docs/` | Documentation only | `docs/scene-structure` |
| `chore/` | Tooling, deps, project settings | `chore/upgrade-godot-4.3` |
| `test/` | Playtest or verification branch | `test/combat-balancing` |

## Commit Messages

- **Do not add `Co-Authored-By` or any AI attribution.** Commits are authored by the human developer only.
- Conventional commit format: `<type>(<scope>): <imperative description>`.

Examples:

```
feat(player): add double-jump with coyote time
feat(enemy): add patrol-and-chase state machine
fix(camera): clamp camera bounds to tilemap limits
refactor(stats): replace raw dict with PlayerStats Resource
perf(spawner): pool enemy instances instead of instancing per wave
chore(godot): upgrade engine to 4.3
style(player): apply gdformat
docs(readme): add env var setup instructions
```

## Godot-Specific Rules

- Commit `.tscn`, `.tres`, and `.gd` files together when they belong to the same feature. A scene without its script (or vice versa) breaks the build.
- Never commit with broken scene references, missing UIDs, or `<missing>` placeholders in scenes.
- The `.godot/` folder is generated. It must be in `.gitignore`.
- The `user://` data and any local `*.cfg` overrides must be in `.gitignore`.
- Binary assets (sprites, audio, fonts) are committed only when finalized. Avoid frequent re-commits of large binaries — squash them in the feature branch before merging.

## Required `.gitignore` Entries

```
.godot/
.import/
export.cfg
export_presets.cfg
*.translation
CLAUDE.local.md
```
