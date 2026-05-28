# Tests - Standard Godot Folders

Testing strategy for each milestone.

## Milestone 1: Create Folder Structure and .gitkeep files

### AI-Friendly Tests
- Run `test -d project/systems`
- Run `test -d project/autoload`
- Run `test -d project/resources`
- Run `test -d project/shared`
- Run `test -f project/systems/.gitkeep`
- Run `test -f project/autoload/.gitkeep`
- Run `test -f project/resources/.gitkeep`
- Run `test -f project/shared/.gitkeep`

### Human-Only Tests
- Verify project folders show up correctly in Godot Editor FileSystem dock.

## Milestone 2: Verification

### AI-Friendly Tests
- Run `git status` to verify the new files are staged or ready to commit.
