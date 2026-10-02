# Architecture & Asset Technical Reference

## 1. Godot 4 Engine Architecture

### Core Framework & Singletons (Autoloads)

Built in **Godot 4** using **GDScript**. Core state and UI transitions are managed globally via Autoloads:

* **`Global` (`global.gd`):** Manages scene transitions and persists spawn coordinates (`set_arrival_pos()`, `take_arrival_pos()`).
* **`GameState` (`game_state.gd`):** Tracks stats (`awareness`), lore flags, and quest completions (`mark_realm_complete()`).
* **`DialogueManager` (`dialogue_manager.gd`):** Handles conversation flows, locks inputs while active, and emits text signals.
* **`ScreenFade` (`screen_fade.gd`):** Controls screen canvas overlay fades (`BLACK` / `WHITE`).

<a href="https://imgbb.com/"><img src="https://i.ibb.co/MxHcgFLp/Screenshot-2026-09-22-at-1-06-38-AM.png" alt="Screenshot 2026 09 22 at 1 06 38 AM" border="0"></a>

---

### Node & Layer Structure

#### Essential Nodes

* **`CharacterBody2D`:** Player movement and collision physics.
* **`AnimatedSprite2D`:** Handles sprite frame animations.
* **`Camera2D`:** Parented to the player for smooth tracking.
* **`Area2D`:** Non-blocking triggers for NPCs, scene transitions, and interaction radii.
* **`TileMapLayer`:** World tile and depth rendering.

All nodes here:

<a href="https://ibb.co/PJmQZTv"><img src="https://i.ibb.co/LBk5zQX/Screenshot-2026-09-22-at-1-07-35-AM.png" alt="Screenshot-2026-09-22-at-1-07-35-AM" border="0"></a>

Important Nodes in our Game:

<a href="https://imgbb.com/"><img src="https://i.ibb.co/ks4yRxwF/Screenshot-2026-09-22-at-1-30-38-AM.png" alt="Screenshot 2026 09 22 at 1 30 38 AM" border="0"></a>

#### TileMap Layers & Depth Sorting

Some map uses 3 layered `TileMapLayer` nodes:

1. **`ground`:** Paths, grass, and terrain (`y_sort_enabled = false`).
2. **`props/yset`:** Buildings, trees, rocks (`y_sort_enabled = true`).
3. **`cliff`:** The cliffs in (`y_sort_enabled = true`).

The Three TileMapLayer nodes:

<a href="https://imgbb.com/"><img src="https://i.ibb.co/czkdqkN/Screenshot-2026-09-22-at-1-09-57-AM.png" alt="Screenshot 2026 09 22 at 1 09 57 AM" border="0"></a>

---

## 2. Visual Assets & Character Pipeline

### Technical Specifications

* **Grid Standards:** $16 \times 16\text{ px}$ world tiles; $48 \times 48\text{ px}$ character sprite frame bounding boxes.
* **Import Settings:** Uniform $48 \times 48\text{ px}$ grid slices, $12\text{--}16\text{ FPS}$ animation rates, RGBA8 format with transparent backgrounds.
* **Style Anchor:** Derived from *Mystic Woods* hero sprite (16-bit color palette, bottom-center grounding pivot).

<a href="https://ibb.co/Jf5yGQ4"><img src="https://i.ibb.co/P7w9PQn/Screenshot-2026-09-22-at-1-32-59-AM.png" alt="Screenshot 2026 09 22 at 1 32 59 AM" border="0"></a>

### Character Creation Workflow

1. **AI Reference:** Concepts generated via Gemini/Ludo.ai.

Monk:

<a href="https://ibb.co/sJN2TmNB"><img src="https://i.ibb.co/n8YbXgYW/Screenshot-2026-09-22-at-1-12-59-AM.png" alt="Screenshot 2026 09 22 at 1 12 59 AM" border="0"></a>

Aum Jomo:

<a href="https://ibb.co/GQqQYXCY"><img src="https://i.ibb.co/fdsd6br6/Screenshot-2026-09-22-at-1-13-49-AM.png" alt="Screenshot-2026-09-22-at-1-13-49-AM" border="0"></a>

Kinley the Guide:

<a href="https://ibb.co/fVd0SjHp"><img src="https://i.ibb.co/wZh6L54W/Screenshot-2026-09-22-at-1-14-59-AM.png" alt="Screenshot 2026 09 22 at 1 14 59 AM" border="0"></a>

Tshomen:

<a href="https://imgbb.com/"><img src="https://i.ibb.co/Q3Wr1Bzb/Screenshot-2026-09-22-at-1-15-46-AM.png" alt="Screenshot 2026 09 22 at 1 15 46 AM" border="0"></a>

Choden the Villager:

<a href="https://ibb.co/JjRMXMZQ"><img src="https://i.ibb.co/chc7z7qL/Screenshot-2026-09-22-at-1-16-20-AM.png" alt="Screenshot-2026-09-22-at-1-16-20-AM" border="0"></a>

The Pilgrim:

<a href="https://imgbb.com/"><img src="https://i.ibb.co/DxvpyGb/Screenshot-2026-09-22-at-1-17-10-AM.png" alt="Screenshot 2026 09 22 at 1 17 10 AM" border="0"></a>

2. **Color Palette:** Hex codes extracted via ImageColorPicker.

The Monk:

<a href="https://ibb.co/Mk1W8Bnx"><img src="https://i.ibb.co/4RS9s1Wn/Screenshot-2026-09-22-at-1-18-10-AM.png" alt="Screenshot-2026-09-22-at-1-18-10-AM" border="0"></a>

Aum Jomo:

<a href="https://ibb.co/0jxXDZDr"><img src="https://i.ibb.co/pvSP0Z0d/Screenshot-2026-09-22-at-1-18-18-AM.png" alt="Screenshot-2026-09-22-at-1-18-18-AM" border="0"></a>
<a href="https://ibb.co/G31t362f"><img src="https://i.ibb.co/Xkd3kQsf/Screenshot-2026-09-22-at-1-18-28-AM.png" alt="Screenshot-2026-09-22-at-1-18-28-AM" border="0"></a>

3. **Canvas Editing:** Hand-drawn over the $48 \times 48\text{ px}$ base frame in Piskel to ensure consistent stance and grounding pivots (e.g., adding a traditional Gho, monk robes, or NPC outfits).

The Monk Finished Sprite:

<a href="https://ibb.co/9fPV3yk"><img src="https://i.ibb.co/krZ96qs/Screenshot-2026-09-22-at-1-19-02-AM.png" alt="Screenshot-2026-09-22-at-1-19-02-AM" border="0"></a>

Kinley Finished Sprite:

<a href="https://ibb.co/j95p09wb"><img src="https://i.ibb.co/twhdjw2Q/Screenshot-2026-09-22-at-1-19-19-AM.png" alt="Screenshot-2026-09-22-at-1-19-19-AM" border="0"></a>

Aum Jomo Finished Sprite:

<a href="https://ibb.co/bjj2kDQr"><img src="https://i.ibb.co/fVVnsLqC/Screenshot-2026-09-22-at-1-19-11-AM.png" alt="Screenshot-2026-09-22-at-1-19-11-AM" border="0"></a>

Tshomen Finished Sprite:

<a href="https://ibb.co/G4Qc6KN7"><img src="https://i.ibb.co/Nd2Zv8bx/Screenshot-2026-09-22-at-1-19-29-AM.png" alt="Screenshot-2026-09-22-at-1-19-29-AM" border="0"></a>

Choden Finished Sprite:

<a href="https://ibb.co/dw9hynMH"><img src="https://i.ibb.co/7dc9F7C0/Screenshot-2026-09-22-at-1-19-37-AM.png" alt="Screenshot-2026-09-22-at-1-19-37-AM" border="0"></a>

Pilgrim Finished Sprite:

<a href="https://ibb.co/9m0ySPys"><img src="https://i.ibb.co/MyHPQdPM/Screenshot-2026-09-22-at-1-19-46-AM.png" alt="Screenshot-2026-09-22-at-1-19-46-AM" border="0"></a>

4. **Special Movement:** Custom tools like *SpriteFlow.io* were used to generate liquid tail-swishing frames for the lake deity (*Tshomen*).

Tshomen:

<a href="https://ibb.co/ccbc49XN"><img src="https://i.ibb.co/3yfygbY0/Screenshot-2026-09-22-at-1-18-42-AM.png" alt="Screenshot-2026-09-22-at-1-18-42-AM" border="0"></a>

---

## 3. Travel System — Roadside Taxi Architecture

Moves players between maps using a shared, data-driven taxi rank (`scenes/taxi_rank.tscn` + `scripts/travel/taxi_rank.gd`).

<a href="https://ibb.co/8LKZmPz0"><img src="https://i.ibb.co/jP6X83VT/Screenshot-2026-09-22-at-1-27-37-AM.png" alt="Screenshot-2026-09-22-at-1-27-37-AM" border="0"></a>

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

## 5. The Addition of Music

**Script:** `res://scripts/music_manager.gd`, registered as the `MusicManager` autoload in `project.godot`. Audio tracks are stored in `res://assets/audio/music/`.

### System

To keep background music persistent across scene changes, the music system is managed by a single global singleton (`MusicManager`). 

- **Crossfading:** When switching scenes or triggering atmosphere changes, `MusicManager` crossfades between two internal `AudioStreamPlayer` nodes using a `Tween` to prevent jarring audio cuts.
- **State Memory:** `MusicManager` tracks the currently playing track and timestamp, allowing returning areas (e.g., exiting a house back to the overworld) to resume seamlessly without restarting the track from the beginning.

### 5.2 Track Assignments and Triggering

| Region / Event | Track File | Behavior |
|---|---|---|
| Main Menu / Title | `main_theme.ogg` | Loops continuously |
| Overworld / Exploration | `main_theme.ogg` | Continues playing across map transitions |
| Shrine / Sacred Sites | `shrine_theme.ogg` | Crossfades in upon entering shrine zone area |

---

## 6. The Sound Effects (SFX) System

**Script:** `res://scripts/sfx_manager.gd`, registered as the `SFXManager` autoload in `project.godot`. All UI and gameplay feedback sounds live in `res://assets/audio/sfx/`.

### Fire-and-Forget Architecture

To prevent SFX playback from cluttering world nodes, the `SFXManager` autoload handles positional and UI audio through a dynamic pool of standard `AudioStreamPlayer` nodes:

- **Audio Pooling:** Calling `play_sfx(stream, pitch_randomness = 0.0, volume_db = 0.0)` retrieves an available `AudioStreamPlayer` from an internal pool (or instances a new one if all pooled players are busy).
- **Pitch Variation:** A subtle pitch shift (`randf_range(1.0 - delta, 1.0 + delta)`) is applied to repetitive actions like footstep cycles, button presses, and UI navigation to reduce auditory fatigue.
- **Auto-Cleanup:** When a non-looping sound finishes playing (`finished` signal), the stream is cleared, volume/pitch parameters reset to baseline, and the player node is returned to the inactive pool.

### Key SFX Mappings and Trigger Events

| Sound Event | Trigger / Signal Source | Default Pitch Spread |
|---|---|---|
| `ui_click` | Dialogue choice focus, travel menu selection | ±0.05 |
| `text_type` | `DialogueBox` typewriter step (`substr` reveal) | ±0.02 |
| `page_turn` | Advancing dialogue lines / Journal interaction | 0.0 (Fixed) |
| `step_footstep` | `Player._physics_process` walking state timer | ±0.08 |
| `water_cleanse` | `DrakayPangtshoQuest` restoration trigger | 0.0 (Fixed) |
| `offering_placed` | `JomolhariQuest` altar interaction | 0.0 (Fixed) |
| `taxi_engine` | `TaxiRank._play_arrival()` & departure sequence | 0.0 (Fixed) |

---

### Cross-cutting patterns worth keeping in the documentation:

* **Autoload Singletons:** Global manager instances (`SFXManager`, `MusicManager`, `GameState`) decoupled from scene hierarchies.
* **Signal-Driven Events:** UI and world interactions trigger events through signals rather than direct node dependencies.
* **Object Pooling:** SFX instances are pooled and cleaned up automatically upon completion.
