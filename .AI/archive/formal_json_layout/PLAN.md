# Technical Plan - Formal JSON & Directory Setup

We will refactor our map configuration loading and set up standard game folders.

## Tasks

1. **Modify Config File**:
   - Rewrite `project/map-config.json` as valid JSON.
2. **Refactor `MapParser`**:
   - Change `_parse_config` in `project/systems/map_parser.gd` to load the config as a JSON string and parse it using `JSON.parse_string()`.
   - Maintain the 50-line file limit.
3. **Generate Folders**:
   - Create directories:
     - `project/shared/sprites/`
     - `project/shared/audio/`
     - `project/shared/fonts/`
     - `project/level/`
     - `project/player/`
   - Place a `.gitkeep` file in each directory.
4. **Verification**:
   - Run the headless test runner to verify everything behaves exactly as before.
5. **Documentation**:
   - Provide run and test instructions to the user.
