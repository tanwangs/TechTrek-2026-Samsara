## 2. Godot Engine Architecture

### 2.1 Core Framework (Godot 4)
The game is developed in **Godot Engine 4** using **GDScript**. The project leverages Godot’s fundamental design principles: modular **Nodes**, **Scenes**, and global **Autoload Singletons**.

### 2.2 Node Hierarchy
| Node Type | Project Purpose & Application |
| :--- | :--- |
| `CharacterBody2D` | Physics body and player movement with environmental collision. |
| `AnimatedSprite2D` | Handles frame by frame character walking and idle animations. |
| `CollisionShape2D` | Defines hitboxes for terrain, obstacles, and player detection areas. |
| `Camera2D` | Attached as a child to the player node to smoothly track movement across maps. |
| `Area2D` | Triggers events without stopping physical movement (used for NPC talk triggers, `SceneExit` transitions, and viewpoint hitboxes). |
| `TileMapLayer` | Renders ground terrain, objects, and water layers efficiently. |

### 2.3 TileMap Layer Hierarchy & Depth Sorting
Every world map utilizes three distinct `TileMapLayer` nodes to handle visual layering and depth:
1. **`ground` Layer:** Ground tiles (grass, plains, paths) using `TileSet_lh53h`. Y-sorting is disabled.
2. **`props` Layer:** Boulders, houses, shrines, and trees using `TileSet_props`. **`y_sort_enabled = true`** with $16 \times 16$ pixel sorting origins so characters properly render in front of or behind objects.
3. **`CleanWater` Layer:** Visual water overlays using `TileSet_clean_water`. Y-sorting is disabled.

### 2.4 Main Scene Structure
* `res://scenes/game.tscn`: Main world map.
* `res://scenes/lobby.tscn`: Central crossroads hub & Chorten shrine.
* `res://scenes/player.tscn`: Student character entity.
* `res://scenes/npc.tscn`: Base NPC template (`Area2D` + `AnimatedSprite2D` + `CollisionShape2D` + Interaction Prompt).
* `res://scenes/nyes/`: Specific realm scenes (`drakay_pangtsho.tscn`, `tak_tsang.tscn`, `jhomo_lhari.tscn`).

---

## 3. Making Sprites & Visual Assets

### 3.1 Sprite & Character Specifications
All character and environmental art follows a standardized $16 \times 16$ grid system (character frame sheets scaled at $48 \times 48$ per frame). Assets use RGBA8 format with transparent backgrounds.

| Asset File | Usage / Description |
| :--- | :--- |
| `res://assets/sprites/player (1).png` | Multi-directional movement sheet for Tashi (`idle_front`, `walk_front`, `idle_side`, etc.). |
| `res://assets/generated/aum_jomo_sheet.png` | Animation atlas for deity Aum Jomo. |
| `res://assets/generated/tshomen_sheet.png` | Animation atlas for the lake deity Tshomen. |
| `res://assets/generated/guide_sheet.png` | Animation atlas for the Crossroads Guide NPC. |
| `res://assets/generated/taktsang_monk.png` | Sprite sheet for monastery monks. |

### 3.2 Environmental & Prop Assets
* **Prototyping Placeholders:** Forest and wilderness environments utilize the open-source **[PixelArt Forest Asset Pack](https://zedpxl.itch.io/pixelart-forest-asset-pack)** by *zedpxl* for prototyping terrain paths.
* **Custom Props:** Specialized Bhutanese architecture props (`bhutan_house.png`, `dzong.png`, `stupa.png`, `prayer_flags.png`, `water_bowl.png`) were created and packed into `TileSet_props`.

### 3.3 Visual Bug Fixes & Rendering Pipeline
* **Animation State Overrides:** Fixed character depth sorting bugs by stripping pre-baked `frame_progress` attributes from `AnimatedSprite2D` scene nodes, restoring pure engine-driven $Y$-sorting across level layers.

---

## 4. Development of the Game

### 4.1 SDLC Methodology
The project followed an **Agile / Iterative Development Model** across four main sprints:
1. **Sprint 1 (Architecture):** Setup of singletons (`GameState`, `DialogueManager`), player physics, and test scripts.
2. **Sprint 2 (World Building):** TileMap mapping, $Y$-sorting configuration, and scene exits.
3. **Sprint 3 (Quests & Mechanics):** Implementation of quest logic scripts (`drakay_pangtsho_quest.gd`, `taktsang_quest.gd`, `jomolhari_quest.gd`).
4. **Sprint 4 (Testing & Polishing):** Execution of automated test suites, bug fixing, and ending dream sequence logic.

### 4.2 Core Game Singletons (Autoloads)
* **`GameState` (`game_state.gd`):** Global singleton tracking progress variables (`awareness` stat, `seen_lore` dictionary, and completion flags like `jomolhari_complete`).
* **`DialogueManager` (`dialogue_manager.gd`):** Manages conversation sequences, blocks movement inputs during active dialogue (`is_active`), and emits line change signals.
* **`Global` (`global.gd`):** Retains player world spawn coordinates between scene loading transitions via `set_arrival_pos()` and `take_arrival_pos()`.
* **`ScreenFade` (`screen_fade.gd`):** Controls screen transition fades (`BLACK` and `WHITE` canvas overlays).

### 4.3 Dialogue & Quest Mechanics Workflow
1. **Proximity Trigger:** Player moves inside an NPC's `Area2D` zone; the interaction prompt highlights.
2. **Input Intercept:** Player presses interact (`E` / `Space`). `NPC.interact()` verifies player position and calls `DialogueManager.start(sequence)`.
3. **Branching Sequence:** `NPC._pick_sequence()` evaluates `GameState.has_seen(lore_key)` to automatically play primary narrative on first visit or repeat dialogue on subsequent visits.
4. **Quest Resolution:** Completing actions (cleaning waste, placing altar items, listening to all 3 monks) calls `GameState.mark_realm_complete("realm_name")`.

### 4.4 Automated Testing & QA
The codebase underwent rigorous automated testing using GDScript test runners. All **80 / 80 tests passed** across 11 test suites:

[PASSED] test_dialogue.gd             (8/8)
[PASSED] test_drakay_pangtsho_quest.gd(9/9)
[PASSED] test_ending_sequence.gd      (8/8)
[PASSED] test_game_state.gd           (9/9)
[PASSED] test_monk.gd                 (7/7)
[PASSED] test_project_setup.gd        (5/5)
[PASSED] test_prop_sorting.gd         (1/1)
[PASSED] test_scene_transitions.gd    (5/5)
[PASSED] test_shrine.gd               (7/7)
[PASSED] test_taktsang_quest.gd       (9/9)
[PASSED] test_village_opening.gd      (8/8)
TOTAL: 80 / 80 Passed (100% Pass Rate)
