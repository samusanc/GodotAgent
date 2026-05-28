# Tests - Game Assets Directory Setup

Testing strategy for the milestones.

## Milestone 1: Create Game Asset and Shader Folders
- AI-Friendly:
  - Verify that the directories exist:
    `test -d project/shared/models`
    `test -d project/shared/textures`
    `test -d project/shared/materials`
    `test -d project/shared/shaders`
    `test -d project/scenes`
  - Verify that `.gitkeep` files exist in each.
