# Project Planning (`.AI/` Directory)

## Purpose

`.AI/` is the planning and documentation directory. It is committed to the repository. It contains only non-code artifacts: plans, goals, architecture notes, and session context.

**Never place source code, scenes, or assets inside `.AI/`.**

## Files

| File | Purpose |
|---|---|
| `PROJECT.md` | Canonical project description — architecture, scene structure, key systems. Update when systems are added, removed, or significantly changed. Imported by root `GEMINI.md`. |
| `GOAL.md` | Goal of the current session. Overwrite at session start with the new objective and open decisions. Imported by root `GEMINI.md`. |
| `DOC.md` | Godot API references, external docs, and snippets relevant to the current goal. |
| `PLAN.md` | High-level technical approach for the current goal. |
| `MILESTONES.md` | Plan broken into atomic, deliverable steps. |
| `TESTS.md` | Testing criteria — what can be verified headlessly vs. needs manual playtest. |
| `CLEANUP.md` | Refactoring and reset plan for after the goal is complete. |

## Layout

```
.AI/
├── PROJECT.md
├── GOAL.md
├── DOC.md
├── PLAN.md
├── MILESTONES.md
├── TESTS.md
├── CLEANUP.md
├── scripts/             # Subagent prompt scripts (one per workflow step)
│   ├── archive.md
│   ├── branch.md
│   ├── clean-plan.md
│   ├── cleanup.md
│   ├── doc.md
│   ├── feature.md
│   ├── loop.md
│   ├── milestones.md
│   ├── plan.md
│   └── test.md
└── archive/             # Completed goals and their context snapshots
```

## Feature Workflow

When a new feature or goal is described, execute these steps in order. Each step must write its output to the corresponding `.AI/` file before the next step begins.

| Step | Script | Writes to | Purpose |
|---|---|---|---|
| 0 | `archive.md` | `.AI/archive/` | Archive current state, reset `.AI/` files |
| 1 | `branch.md` | (git) | Create and switch to the appropriate branch |
| 2 | `doc.md` | `DOC.md` | Gather Godot API docs and references for the goal |
| 3 | `plan.md` | `PLAN.md` | Define the high-level technical approach |
| 4 | `milestones.md` | `MILESTONES.md` | Break the plan into atomic, deliverable steps |
| 5 | `test.md` | `TESTS.md` | Define testing strategy per milestone |
| 6 | `cleanup.md` | `CLEANUP.md` | Pre-plan post-goal refactoring |
| 7 | `loop.md` | (code) | Execute the implementation loop |
| 8 | `clean-plan.md` | All `.AI/` files | Run cleanup and update context files |

Each subagent inherits: `PROJECT.md`, the `.AI/` files already produced by earlier steps, and all `.gemini/rules/`.

## When To Write Code

- If `GOAL.md` is empty or stale, refuse to write code. Run the feature workflow first.
- If `PLAN.md` and `MILESTONES.md` don't exist for the current goal, refuse to write code. Steps 3 and 4 must complete first.
- Always know which milestone in `MILESTONES.md` you are currently implementing.
