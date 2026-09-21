# Architecture & Asset Technical Reference

## 1. Godot 4 Engine Architecture

### Core Framework & Singletons (Autoloads)

Built in **Godot 4** using **GDScript**. Core state and UI transitions are managed globally via Autoloads:

* **`Global` (`global.gd`):** Manages scene transitions and persists spawn coordinates (`set_arrival_pos()`, `take_arrival_pos()`).
* **`GameState` (`game_state.gd`):** Tracks stats (`awareness`), lore flags, and quest completions (`mark_realm_complete()`).
* **`DialogueManager` (`dialogue_manager.gd`):** Handles conversation flows, locks inputs while active, and emits text signals.
* **`ScreenFade` (`screen_fade.gd`):** Controls screen canvas overlay fades (`BLACK` / `WHITE`).

---

### Node & Layer Structure

#### Essential Nodes

* **`CharacterBody2D`:** Player movement and collision physics.
* **`AnimatedSprite2D`:** Handles sprite frame animations.
* **`Camera2D`:** Parented to the player for smooth tracking.
* **`Area2D`:** Non-blocking triggers for NPCs, scene transitions, and interaction radii.
* **`TileMapLayer`:** World tile and depth rendering.

#### TileMap Layers & Depth Sorting

Every map uses 3 layered `TileMapLayer` nodes:

1. **`ground`:** Paths, grass, and terrain (`y_sort_enabled = false`).
2. **`props`:** Buildings, trees, rocks (`y_sort_enabled = true`). Origin set to $16 \times 16\text{ px}$ so entities render correctly in front of/behind props.
3. **`CleanWater`:** Visual water overlays (`y_sort_enabled = false`).

---

## 2. Visual Assets & Character Pipeline

### Technical Specifications

* **Grid Standards:** $16 \times 16\text{ px}$ world tiles; $48 \times 48\text{ px}$ character sprite frame bounding boxes.
* **Import Settings:** Uniform $48 \times 48\text{ px}$ grid slices, $12\text{--}16\text{ FPS}$ animation rates, RGBA8 format with transparent backgrounds.
* **Style Anchor:** Derived from *Mystic Woods* hero sprite (16-bit color palette, bottom-center grounding pivot).

### Character Creation Workflow

1. **AI Reference:** Concepts generated via Gemini/Ludo.ai.
2. **Color Palette:** Hex codes extracted via ImageColorPicker.
3. **Canvas Editing:** Hand-drawn over the $48 \times 48\text{ px}$ base frame in Piskel to ensure consistent stance and grounding pivots (e.g., adding a traditional Gho, monk robes, or NPC outfits).
4. **Special Movement:** Custom tools like *SpriteFlow.io* were used to generate liquid tail-swishing frames for the lake deity (*Tshomen*).

---

## 3. Travel System — Roadside Taxi Architecture

Moves players between maps using a shared, data-driven taxi rank (`scenes/taxi_rank.tscn` + `scripts/travel/taxi_rank.gd`).

### Journey Flows

* **Outbound (Base Camp $\rightarrow$ Realm):** Player interacts with the shrine (*Chorten*). `dispatch_outbound()` spawns the taxi off-screen. Player boards with **E**, controls lock, and the taxi drives off-screen to change scenes.
* **Return (Realm $\rightarrow$ Base Camp):** Player approaches the post and presses **T**. The taxi arrives, the player boards with **E**, and returns to the lobby rank (`LobbyTaxiStop`).
* **Shared Arrival Beat:** The taxi drives in with the student hidden inside, stops, pauses 1.4 seconds, drops the student off at `rank.global_position + lane_offset`, and drives away.

### Primary Taxi Properties

* `destinations`: Array of `.tres` (`TravelDestination`) resources defining destination scene paths and spawn coordinates.
* `lane_offset`: Parking position offset `(104, 18)` relative to the post.
* `allow_manual_call`: Toggles key **T** calling (`false` on lobby rank, `true` in realms).

---

## 4. Interaction & Narrative Loops

```
[ Player enters Area2D ] ---> [ Interaction Prompt Displays ]
                                      |
                                  (Press E)
                                      |
[ NPC._pick_sequence() ] ---> Check GameState.has_seen()
                                      |
                        +-------------+-------------+
                        |                           |
                 (First Visit)              (Repeat Visit)
                        |                           |
               Primary Dialogue              Fallback Dialogue

```

1. **Dialogue Gating:** Proximity triggers the prompt. Pressing **E** checks `GameState` history to branch between main and repeat dialogue.
2. **Quest Resolution:** Completing realm mechanics (cleaning litter, placing offerings, completing oral retellings) triggers `GameState.mark_realm_complete()`.
3. **State Persistence:** Persistent trip data and player coordinates are retained across scene changes via `Global` singletons.
