# Tests - Map Parser & Simulation

Verification strategy for the milestones.

## Milestone 1: Setup Assets and Resources
- AI-Friendly:
  - Check file existence of `project/map-example.txt`, `project/map-config.json`.
  - Check GDScript syntax:
    `godot --headless --check-only --script project/resources/trigger_data.gd`
    `godot --headless --check-only --script project/resources/map_data.gd`

## Milestone 2: Implement MapParser
- AI-Friendly:
  - Check GDScript syntax:
    `godot --headless --check-only --script project/systems/map_parser.gd`

## Milestone 3: Implement MapSimulation
- AI-Friendly:
  - Check GDScript syntax:
    `godot --headless --check-only --script project/systems/map_simulation.gd`

## Milestone 4: Automated Testing & Verification
- AI-Friendly:
  - Run the test runner:
    `godot --headless --script project/systems/test_runner.gd`
  - Verify that the simulation correctly:
    1. Blocks movement into wall cells ('1').
    2. Allows movement in path cells ('0').
    3. Triggers signals/events when entering trigger coordinates.
