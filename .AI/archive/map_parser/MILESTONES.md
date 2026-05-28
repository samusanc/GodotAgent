# Milestones - Map Parser & Simulation

Each milestone keeps the project in a working state.

## Milestone 1: Setup Assets and Resources
- Copy `map-example.txt` and `map-config.json` to the `project/` directory.
- Create `res://resources/trigger_data.gd`.
- Create `res://resources/map_data.gd`.

## Milestone 2: Implement MapParser
- Create `res://systems/map_parser.gd`.
- Read and parse map grid, parse config file lines, assemble and return a `MapData`.
- Enforce the 50-line limit.

## Milestone 3: Implement MapSimulation
- Create `res://systems/map_simulation.gd`.
- Maintain player position, handle grid boundaries and wall checks (`1` vs `0`), trigger detection.
- Enforce the 50-line limit.

## Milestone 4: Automated Testing & Verification
- Create `res://systems/test_runner.gd`.
- Execute headless tests verifying movement blockages and trigger events.
- Output test reports.
