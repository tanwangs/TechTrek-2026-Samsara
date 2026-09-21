# 4. Testing & QA Framework

## 4.1 Overview & Test Results

The project uses automated GDScript test suites covering all core systems, mechanics, and narrative sequences.

* **Pass Rate:** **100%** (All 14 test suites passing)
* **Coverage:** Singletons, dialogue flows, audio crossfading, taxi journeys, quest states, and spatial rendering.

---

## 4.2 Core Architecture Tests

### Spatial & Rendering Checks

* **Y-Sorting:** Validates that `TileMapLayer` and prop sprite sorting origins (`y_sort_origin`) match their base height to prevent visual layering bugs.
* **Collisions & Offsets:** Confirms prop nodes apply proper vertical offsets (`-height / 2`) and multi-cell tile collision bounds cover $\ge 70\%$ of tile height.

### Audio Pipeline (`test_music.gd`)

* **Crossfading:** Ensures new track requests trigger a smooth crossfade while re-requesting the current track does nothing.
* **Interrupts & Fallbacks:** Switching back to a fading track restores it smoothly; requesting a `null` track fades audio to silence.
* **Scene Mapping:** Confirms maps play their designated track while unmapped interiors maintain the active ambient audio.

### Dialogue System

* **Resource Health:** Verifies unique sequence IDs, valid speaker assignments, and non-empty lines in `res://dialogue/`.
* **Signal Flow:** Validates start/end signals (`dialogue_started`, `dialogue_ended`) and confirms active dialogue blocks input until choices are resolved.

### Taxi & Transition Persistence

* **Return Queue:** Confirms returning from a realm queues exactly one return beat.
* **Sequence Control:** Ensures return beats lock UI input and wait for `LobbyTaxiStop`'s `arrival_completed` signal before clearing.

---

## 4.3 Quest & Story Mechanics Tests

### Main Quests

* **Jomolhari (Pacing Gate):** Rapid inputs at the altar trigger a retry interrupt ("Again. Slower.") with 0 points awarded. Spaced inputs grant awareness and complete the ritual.
* **Drakay Pangtsho (Lake Quest):** Verifies water cues unlock deity explanations, memory flashes trigger on waste pickup, and placing 3 offerings completes the realm.
* **Taktsang (Escort Quest):** Confirms Dolma follows at a fixed speed, stops with a callout if the player rushes too far ahead, and settles permanently at the viewpoint.

### Side Quests

* **Mending Quest (`test_mending_quest.gd`):** Mashing inputs while knotting cords triggers a slip interrupt. Pausing between steps ($\ge 900\text{ ms}$) successfully repairs the platform and awards awareness.
* **Herder's Path (`test_herder_quest.gd`):** Verifies clue markers must be read sequentially (1 to 4) before the lost yak becomes interactive and follows the player home.

### Ending Sequence

* **Trigger Requirements:** Confirms the final ending sequence stays locked until all 3 main realms are complete (`retreat_finished()`).
* **Post-Dream Bowl:** Verifies the final water bowl appears post-dream, awards final awareness, and sets `ending_complete`.
