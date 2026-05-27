---
When I describe a new feature or goal, follow this workflow:

**1. Archive the previous goal**
Run `archive.md` first to archive the current state and reset all `.AI/` files before anything else is touched.

**2. Write the goal**
Capture the full, well-defined goal in `.AI/GOAL.md` before doing anything else.

**3. Execute subagents in order**
Spawn each subagent using the corresponding script from `.AI/scripts/` as its base prompt. Each agent also inherits the full project context: `PROJECT.md`, the relevant `.AI/` files already produced, your project rules, and code quality standards.

**Project context structure:**
```
.AI/
├── PROJECT.md       # Permanent project context (architecture, stack, core rules)
├── GOAL.md          # Current feature or bug being worked on
├── DOC.md           # Documentation, API references, and snippets for the goal
├── PLAN.md          # High-level technical approach
├── MILESTONES.md    # Plan broken into atomic, self-contained steps
├── TESTS.md         # Testing criteria (AI-Friendly vs. Human-Only)
├── CLEANUP.md       # Refactoring and state-reset plan for post-goal
├── scripts/         # One prompt script per workflow step
│   ├── archive.md
│   ├── branch.md
│   ├── doc.md
│   ├── plan.md
│   ├── milestones.md
│   ├── test.md
│   ├── cleanup.md
│   ├── feature.md
│   ├── loop.md
│   └── clean-plan.md
└── archive/         # Completed goals and their context snapshots
```

**Execution order:**

| Step | Script | Purpose |
|------|--------|---------|
| 1 | `branch.md` | Create and switch to the appropriate branch |
| 2 | `doc.md` | Research and gather documentation for the goal |
| 3 | `plan.md` | Define the high-level technical approach |
| 4 | `milestones.md` | Break the plan into atomic, deliverable steps |
| 5 | `test.md` | Define the testing strategy for each milestone |
| 6 | `cleanup.md` | Pre-plan the post-goal refactoring and reset |
| 7 | `loop.md` | Execute the implementation loop |
| 8 | `clean-plan.md` | Run post-execution cleanup and update all context files |

Each step must complete and write its output to the corresponding `.AI/` file before the next step begins.

---
