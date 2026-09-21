# Requirements & Research

## Literature Review / Research

### Referenced External Assets
Forest and wilderness prototyping terrain uses the open-source
[PixelArt Forest Asset Pack]([https://zedpxl.itch.io/pixelart-forest-asset-pack](https://game-endeavor.itch.io/mystic-woods))
by *zedpxl*, used for prototyping terrain paths. *(Confirm the asset
pack's license terms are compatible with the competition's submission
requirements, and credit the author in the final submission.)*


### Research Directions
- Comparable narrative/cultural-education games (e.g. *Never Alone*,
  which embeds Indigenous Alaskan storytelling into mechanics rather
  than cutscenes) as a reference point for this design approach.

<a href="https://imgbb.com/"><img src="https://i.ibb.co/kkmcNcN/never-alone-1554756467.jpg" alt="never alone 1554756467" border="0"></a>
  
- Research on experiential/embodied learning vs. didactic instruction in
  educational game design, relevant to justifying the mechanics-first
  approach used throughout (e.g. the pacing mechanic at Jomolhari,
  where "intention matters more than action" is enforced mechanically
  rather than only stated in dialogue).
- Background research specifically on Ley-Ju-Drey and GNH pillars as
  taught in Bhutanese education, to ground the curricular claims in
  `game-overview.md` in cited sources.

*[Expand this section with actual citations before final submission.]*

---

## User Requirement Specification (URS/URD)

### Functional Requirements
- The player must be able to move Tashi using keyboard input, with
  physics-based collision against terrain and props (`CharacterBody2D`
  + `CollisionShape2D`)
- The player must be able to trigger NPC dialogue via proximity
  (`Area2D`) and an interact key (E / Space)
- `DialogueManager` must block movement input while a dialogue sequence
  is active (`is_active`) and emit line-change signals
- `NPC._pick_sequence()` must correctly branch between first-visit and
  repeat dialogue based on `GameState.has_seen(lore_key)`
- Completing a realm's required actions must call
  `GameState.mark_realm_complete("realm_name")`
- Player spawn position must persist correctly across scene transitions
  via `Global.set_arrival_pos()` / `take_arrival_pos()`
- Scene transitions must use `ScreenFade`'s black/white overlay system

### Non-Functional Requirements
- Stable frame rate on standard consumer hardware (2D sprite/tile
  rendering, no specialized GPU requirement)
- Responsive dialogue advancement and interaction detection, no
  noticeable input lag
- Consistent 16×16 grid-based pixel art across all character and
  environmental assets (48×48 per animation frame), RGBA8 with
  transparent backgrounds

### System Constraints
- Built in Godot Engine 4 / GDScript
- Prop/character tiles depend on correctly configured Y-sort origins
  (16×16) on the `props` TileMapLayer for correct depth ordering

### User Expectations
- Narrative-first, low-difficulty exploration experience appropriate
  for a 30–45 minute classroom session

### Assumptions and Dependencies
- Assumes familiarity with standard top-down/WASD movement conventions
- Dependent on Godot 4's `TileMapLayer`, `CharacterBody2D`, `Area2D`,
  and `AnimatedSprite2D` node behavior remaining stable across the
  development period
