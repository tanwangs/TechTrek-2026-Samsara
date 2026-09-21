## APPEND THIS TO THE END OF YOUR EXISTING game-overview.md
## (These are new sections — 1.6 Objectives and 1.7 Scope — your
## existing 1.1–1.5 content stays as-is above this.)

---

### 1.6 Objectives

**General objective:** design and build a GNH-aligned narrative
exploration game that bridges modern digital-native youth and Bhutan's
sacred oral traditions, spiritual heritage, and ecological wisdom.

**Specific objectives:**
- Implement three sacred-realm quests, each tied to a distinct GNH
  pillar (cultural values, environmental studies, art/humanities) and a
  mechanically distinct core lesson
- Model Ley-Ju-Drey (cause and effect) directly through gameplay
  consequences, not only narration
- Build a functional core systems layer — `GameState`, `DialogueManager`,
  `Global`, and `ScreenFade` autoloads — supporting consistent quest
  tracking, dialogue, spawn persistence, and scene transitions across
  all realms
- Represent Bhutanese architecture and dress authentically in pixel art
  (Dzongs, Chortens, Stupas, Gho/Kira)
- Validate implementation through an automated GDScript test suite
  covering dialogue, quest logic, scene transitions, and game state

---

### 1.7 Scope of the Project

**Features included:**
- Full playable loop: village → dream sequence → crossroads/lobby hub →
  three realm quests → return-to-lobby sequence
- A `DialogueManager` autoload supporting branching first-visit vs.
  repeat-visit dialogue
- A `GameState` autoload tracking an `awareness` stat, a `seen_lore`
  dictionary, and per-realm completion flags
- A `Global` autoload persisting player spawn coordinates across scene
  transitions
- A `ScreenFade` autoload controlling black/white screen transition
  overlays
- Three `TileMapLayer`-based terrain layers per world map (ground,
  props, water) with Y-sort depth ordering on the props layer
- Custom Bhutanese architectural props packed into a dedicated TileSet
- An automated GDScript test suite (11 suites, 80 tests, 100% passing)

**Limitations and exclusions (at time of this documentation):**
- The taxi travel mechanism and the additional side quests developed
  later in the design process ("The Herder's Path," "Mending What's
  Shared," "The Pilgrim's Climb") are part of later development work —
  update this section once those passes are confirmed merged and
  covered by tests
- Sound effects (distinct from background music/ambience) are a planned
  but not-yet-fully-documented layer
- No combat or branching-choice narrative structure
