## 4.4 Testing and Validation
 
**Automated testing:** the codebase underwent automated testing using
GDScript test runners across 11 test suites, **80/80 tests passing
(100% pass rate)**:
 
```
test_dialogue.gd — 8/8 Passed
test_drakay_pangtsho_quest.gd — 9/9 Passed
test_ending_sequence.gd — 8/8 Passed
test_game_state.gd — 9/9 Passed
test_herder_quest.gd — 7/7 Passed
test_mending_quest.gd — 7/7 Passed
test_monk.gd — 7/7 Passed
test_music.gd — 9/9 Passed
test_project_setup.gd — 5/5 Passed
test_prop_sorting.gd — 1/1 Passed
test_scene_transitions.gd — 5/5 Passed
test_shrine.gd — 7/7 Passed
test_taktsang_quest.gd — 9/9 Passed
test_village_opening.gd — 8/8 Passed
TOTAL: 103 / 103 Passed (100% Pass Rate)
```
 
# Comprehensive GDScript Unit Test Suite

## 4.5. Core Systems & Technical Architecture

### Y-Sorting & Collision Alignment

* **TileMap & Sprite Sorting**: Ensures `TileMapLayer` tiles with `y_sort_enabled` match their art base pixel height (`y_sort_origin`), preventing depth-sorting issues where characters render behind or in front of props incorrectly.


* **NPC & Standalone Prop Offsets**: Confirms NPC sprites stand directly on node origins and `Sprite2D` prop nodes apply a vertical offset equal to `-height / 2`.


* **Layer Z-Index Restrictions**: Verifies Y-sorted layers remain strictly in `z_index == 0` so depth sorting isn't overridden.


* **Multi-Cell Tile Collisions**: Validates multi-cell tile collision polygons to guarantee physics boundaries extend to at least 70% of tile height and remain centered within 20% horizontal bounds.



### Audio & Music Autoload (`test_music.gd`)

* **Crossfading & Same-Track Guard**: Requesting the currently playing music track does nothing. Requesting a new track crossfades smoothly by running the fading track on a secondary player while setting up the active player to fade in.


* **Track Interruption & Silence**: Switching back to a track currently fading out immediately reassigns it to the active player. Requesting a `null` track clears active track references and fades audio to silence.


* **Scene & Root Mapping**: Maps realm scene paths (Jomolhari, Drakay Pangtsho, Taktsang) and root node names to corresponding tracks; unmapped or interior shrine scenes keep current playback.


* **Stream Loop & Boundary Validation**: Confirms forward looping on all audio streams (WAV, Ogg, MP3) and checks WAV loop point bounds to ensure start/end frames stay within valid audio buffer dimensions without trimming over half the track.



### Dialogue System Architecture

* **Authored Resource Validation**: Scans `res://dialogue/*.tres` to verify unique sequence IDs, non-empty text, valid speakers, and core cast dialogue files.


* **Flow & Signal Control**: Validates state management, signal emissions (`dialogue_started`, `line_changed`, `dialogue_ended`), line ordering, and early termination via `stop()`.


* **Interruption & Choice Handling**: Confirms active dialogue blocks new sequence starts and choice lines pause progression until `choose()` receives a valid option index.



### Taxi & Return-Home Beat System

* **Queue Management**: Verifies that completing a realm queues exactly one return beat in `GameState` without double-counting repeat completions.


* **Lobby Taxi Sequence**: Ensures return beats wait for the `arrival_completed` signal from the `LobbyTaxiStop` node, lock UI controls during playback, and clear the queue upon completion.



---

## 4.6 Realm Main Story Mechanics

### Jomolhari Realm & Pacing Gate Mechanics

* **Pacing Gate Enforcement**: Rapid input mashing during the ritual interaction at Tsheringma Ney altar triggers Aum Jomo's interrupt ("Again. Slower.") and grants 0 awareness.


* **Deliberate Ritual Completion**: Spacing inputs beyond the minimum interval completes the realm, grants awareness (4 points initially, 3 on retries), and unlocks Aum Jomo's progression dialogue ("Better.").


* **Item Collection & Dialogue Order**: Gathering all three items auto-triggers the altar offering sequence and updates Aum Jomo's conversation tree from intro to reminder, completion, and lore.



### Drakay Pangtsho Realm Mechanics

* **Shore & Item States**: Items remain visible prior to quest start. Tshomen re-asks her intro question until water cues are noticed (`CUES_NOTICED`), which unlocks her explanation.


* **Memory Flash & Altar Progression**: Tests memory flash triggers on the second waste item and verifies collecting three waste items updates the altar offering sequence.


* **Awareness & Side Quests**: Tracks awareness accumulation for examining water cues and placing offerings, while requiring all three sitting/listening locations for side quest completion.



### Taktsang Realm: "The Pilgrim's Climb" Escort Quest

* **Escort Initiation & Speed**: Dolma remains stationary until spoken to (`pilgrim_intro`), after which she follows the player up the trail at a fixed speed.


* **Distance Callout & Resume**: Rushing too far ahead causes Dolma to stop, issue a callout ("Wait - a moment, child! Let an old woman keep her pace..."), and wait until the player returns nearby.


* **Viewpoint Completion**: Escorting Dolma to the viewpoint completes the side quest, grants awareness, plays her arrival line ("Worth arguing for."), and permanently settles her at the top.



---

## 4.7. Realm Side Quests

### Drakay Pangtsho: "Mending What's Shared" (`test_mending_quest.gd`)

* **Quest Initiation & Gathering**: Initiated by Choden (`mending_intro`). Reed stands cannot be cut prior to her request, and all three stand bundles must be gathered along the shore before the fishing platform repair becomes available (`mending_repair`).


* **Pacing Gate Enforcement**: Hurrying inputs during cord-knotting causes the cord to slip, triggering Choden's interrupt line ("Slipped. Easy - hands before hurry..."), granting 0 awareness, and keeping the platform un-mended.


* **Deliberate Repair & Rewards**: Spacing knot interactions with deliberate pauses ($\ge \text{900ms}$) completes the platform repair, completes the side quest, awards awareness, auto-triggers Choden's family lore dialogue after a short delay, and settles Choden into her post-quest line (`mending_done`).


* **Persistence & Isolation**: Partial progress (e.g., 2 of 3 stands cut) persists across scene reloads, and completing the quest leaves the primary realm state and lake reflection quest untouched.



### Jomolhari: "The Herder's Path" (`test_herder_quest.gd`)

* **Sequential Trail Progression**: Unlocked by speaking with Dema (`herder_intro`). Trail clue markers must be read strictly in sequential walking order (1 through 4); reading a clue unlocks the next sign while silencing previous ones.


* **Yak Discovery & Resolution**: The lost yak becomes interactive (`herder_yak_found`) only after all four clues are read. Interacting with the yak sets `YAK_FOUND` and despawns the yak from the ridge so it follows the player back.


* **Completion Rewards**: Returning to Dema triggers her gratitude (`herder_thanks`), completes the second Jomolhari side quest, grants awareness, and awards the woven cord item. Dema and the yak permanently settle together near her stone at the trailhead (`herder_done`).


* **Persistence & Isolation**: Trail progress survives map reloads, and quest completion does not affect primary realm completion or the listening side quest.



---

## 4.8 Final Ending Sequence & Water Bowl Arc

* **Completion Requirement**: Confirms the ending sequence remains inactive until all three realms are finished (`retreat_finished()`).


* **Dream Dialogue & Transition**: Verifies `ending_dream.tres` contains three full lines regarding paying attention and tree light, delegating scene switching to lobby/game handlers.


* **Ending Water Bowl Interaction**: Ensures `EndingWaterBowl` appears post-dream (suppressing the tutorial bowl). Tending the bowl plays dialogue, raises awareness, marks `ending_complete`, and frees the node for free exploration.



---

## 4.9 Resource UID Register

| Asset / File Component | Resource UID |
| --- | --- |
| Y-Sorting & Collision Suite | `uid://bjijkx8cyait4`<br> |
| Taxi Beat System Suite | `uid://ctkiqwwdmvlnd`<br> |
| Dialogue & Realm Core Suite | `uid://c56nkd05xrqgv`<br> |
| `test_music.gd` | `uid://dghumsxplyesc`<br> |
| `test_mending_quest.gd` | `uid://cjpl2qnlpyl75`<br> |
| `test_herder_quest.gd` | `uid://cycpusg36ee6t`<br> |
