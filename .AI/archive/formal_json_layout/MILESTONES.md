# Milestones - Formal JSON & Directory Setup

Each milestone keeps the project in a working state.

## Milestone 1: Create Game Development Folders
- Create the directories for sprites, audio, fonts, levels, and players.
- Add `.gitkeep` files to each.

## Milestone 2: Rewrite map-config.json
- Replace the content of `project/map-config.json` with formal JSON matching the coordinates and triggers from the prototype.

## Milestone 3: Refactor MapParser
- Update `MapParser._parse_config` in `project/systems/map_parser.gd` to use `JSON.parse_string()`.
- Ensure the script remains under 50 lines.

## Milestone 4: Verification
- Run syntax checks and the headless `TestRunner` to verify correct loading and simulation behavior.
