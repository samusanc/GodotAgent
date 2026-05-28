# Tests - Formal JSON & Directory Setup

Verification strategy for the milestones.

## Milestone 1: Create Game Development Folders
- AI-Friendly:
  - Verify folders exist:
    `test -d project/shared/sprites`
    `test -d project/shared/audio`
    `test -d project/shared/fonts`
    `test -d project/level`
    `test -d project/player`

## Milestone 3: Refactor MapParser
- AI-Friendly:
  - Verify syntax:
    `/home/samusanc/Downloads/godot --headless --check-only --script project/systems/map_parser.gd`

## Milestone 4: Verification
- AI-Friendly:
  - Run the test suite:
    `/home/samusanc/Downloads/godot --headless --script project/systems/test_runner.gd`
  - Verify that the output states: `All tests passed successfully!`
