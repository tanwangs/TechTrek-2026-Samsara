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

## 2. Visual Assets & Sprite Development Architecture

### 2.1 Sprite & Character Technical Benchmarks

All character sprite sheets use a 48×48 pixel bounding box to allow room for movement, weapon swings, and posture padding, while world tilemaps utilize a standard 16×16 pixel grid. Engine import settings slice sprite grids uniformly at 48×48 pixels and enforce an animation speed of 12 to 16 FPS. All entities share a bottom-center grounding pivot, a 16-bit color palette, and consistent outline density derived from the base Mystic Woods hero style reference. Assets use RGBA8 format with transparent backgrounds.

| Asset File | Usage / Description |
| --- | --- |
| `res://assets/sprites/player (1).png` | Multi-directional movement sheet for Tashi (`idle_front`, `walk_front`, `idle_side`, etc.). |
| `res://assets/generated/aum_jomo_sheet.png` | Animation atlas for deity Aum Jomo. |
| `res://assets/generated/tshomen_sheet.png` | Animation atlas for the lake deity Tshomen. |
| `res://assets/generated/guide_sheet.png` | Animation atlas for the Crossroads Guide NPC. |
| `res://assets/generated/taktsang_monk.png` | Sprite sheet for monastery monks. |

### 2.2 Character Customization & AI Reference Pipelines

```
[ AI Reference Gen ] ---> [ Color Extraction ] ---> [ Canvas Base Editing ] ---> [ Motion / Polish ]
 (Gemini / Ludo.ai)        (ImageColorPicker)       (Piskel 48x48 Base)         (Engine Integration)

```

## 3. Making Sprites & Visual Assets

### 3.1 Sprite & Character Specifications

All character and environmental art follows a standardized 16×16 grid system (character frame sheets scaled at 48×48 per frame). All assets use the RGBA8 format with transparent backgrounds.

| Asset File | Usage / Description |
| --- | --- |
| `res://assets/sprites/player (1).png` | Multi-directional movement sheet for Tashi (`idle_front`, `walk_front`, `idle_side`, etc.). |
| `res://assets/generated/aum_jomo_sheet.png` | Animation atlas for deity Aum Jomo. |
| `res://assets/generated/tshomen_sheet.png` | Animation atlas for the lake deity Tshomen. |
| `res://assets/generated/guide_sheet.png` | Animation atlas for the Crossroads Guide NPC. |
| `res://assets/generated/taktsang_monk.png` | Sprite sheet for monastery monks. |

---

### 3.2 Base Character Setup & Technical Benchmarks

The player character from Game Endeavor's *Mystic Woods* asset pack was selected as the visual anchor. Core parameters were established around this reference to ensure visual and technical consistency across the project:

* **Grid & Bounding Box:** Character sprite sheets use a 48×48 pixel frame bounding box to allow room for weapon swings and animation padding, while world tilemaps fit a standard 16×16 pixel grid.
* **Engine Import Settings:** When importing sheets into the engine, grids are sliced uniformly at 48×48 pixels with animation rates set between 12 and 16 frames per second (FPS) for smooth movement.
* **Visual Reference Benchmark:** Using the base hero as the primary style reference ensures all future characters, NPCs, and custom edits match its 16-bit color palette, outline density, and bottom-center grounding pivot.

---

### 3.3 Character & Asset Creation Processes

#### Customizing the Hero: Adding a Gho

To make the main character unique, the original *Mystic Woods* sprite was modified so the hero wears a traditional Bhutanese Gho:

1. **Visual Reference:** Real-world photographs were gathered to capture key visual features—specifically the wrapped robe structure, wide white folded cuffs (*lagay*), hoisted belt (*kera*), and the pouch formed above the waist.
2. **Editing in Piskel:** The original 48×48 frame sprite sheet was imported into Piskel. The outfit was drawn directly over the base character's body frame-by-frame, translating fabric folds, colors, and traditional proportions into pixel art.

#### The Monk Character

* **Reference Generation:** Gemini generated initial visual reference images to assist in translating traditional monk robes, posture, and clothing details into top-down pixel art.
* **Color Palette:** Images were uploaded to ImageColorPicker to extract exact hex codes and color names, constructing a custom palette in Piskel.

* **Direct Base Editing:** Edits were applied directly over the 48×48 hero base frame in Piskel to maintain stance angle, scale, and the bottom-center grounding point.
* **Final Stance:** The monk strictly remains in an idle position to serve a stationary role without requiring walking or action animation cycles. Focus was placed on fine-tuning robe drapes and shading.

#### The Grandma NPC

* **AI Reference Generation:** Concept art was generated using Ludo.ai's Sprite Generator to guide posture, clothing folds, and hair styling.
* **Color Palette:** Concept images were sampled in ImageColorPicker to extract exact hex codes for clothing and hair before importing into Piskel.
* **Direct Canvas Editing:** Editing occurred directly over the 48×48 hero base sprite in Piskel to align her height, stance, and grounding point with the rest of the game world.
* **Final Polish:** Silhouettes and garment details were refined to ensure a distinct look that fits the *Mystic Woods* aesthetic as a stationary NPC.

#### The Guide NPC

* **Gemini Reference Generation:** Gemini was utilized to obtain precise visual prompts and character designs for the Guide NPC.
* **Color Palette & Setup:** Outputs were processed in ImageColorPicker to extract hex codes and build a custom palette in Piskel.
* **Direct Base Editing:** Modifications were drawn directly over the 48×48 hero sprite in Piskel to match cast proportions, perspective, and grounding points.
* **Final Polish:** Clothing details and shading were fine-tuned for seamless integration into the world.

#### The Mermaid Sprite (Tshomen)

* **Gemini Reference Generation:** Visual references were generated using Gemini to establish the upper body design, color scheme, and tail structure.
* **Tail Animation with SpriteFlow:** SpriteFlow.io was used to generate and refine tail-swishing motion for smooth, water-bound animation cycles.
* **Color Palette & Base Editing:** Exact hex codes were extracted via ImageColorPicker to build a custom palette in Piskel, editing over the standard 48×48 base frame to keep upper body scale consistent.
* **Final Integration:** Tail animation frames were integrated back into Piskel, cleaning up pixel edges and shading for final assembly.

---

### 3.4 Environmental & Prop Assets

* **Prototyping Placeholders:** Forest and wilderness environments utilize the open-source *PixelArt Forest Asset Pack* by zedpxl for terrain paths during prototyping.
* **Custom Props:** Specialized Bhutanese architecture and cultural props (`bhutan_house.png`, `dzong.png`, `stupa.png`, `prayer_flags.png`, `water_bowl.png`) were created and packed into `TileSet_props`.

---

### 3.5 Visual Bug Fixes & Rendering Pipeline

* **Animation State Overrides:** Character depth-sorting issues were resolved by stripping pre-baked `frame_progress` attributes from `AnimatedSprite2D` scene nodes, restoring pure engine-driven Y-sorting across level layers.

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

---

### 4.5 Manual & Integration Verification

In addition to the automated suite above, the following were manually
verified during development:
- The Jomolhari pacing mechanic correctly gates quest completion
  (rushed attempts trigger a retry rather than completing)
- Drakay Pangtsho's environmental cues (litter, disturbed offering
  stones) appear before the guide character's full explanation
- Prop Y-sort depth ordering renders correctly after the
  `frame_progress` bug fix (also covered by `test_prop_sorting.gd`)

### 4.6 User Acceptance Testing

*[To be completed — recommend testing with representative target users
(ages 12–18) and
recording qualitative feedback on pacing, clarity of mechanics, and
cultural resonance.]*
