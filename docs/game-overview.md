# The Tapestry of Monyul — Project Documentation

## 1. Game Overview

## 1.1 Game Title & Logline
Title: The Tapestry of Monyul

Genre: 2D Top-Down Narrative RPG

Logline: Step into the boots of Tashi, a young student going on a "Nature Retreat" across Bhutan's sacred landscapes (nyes), where interactions with local guardians, historical figures, and lake deities unlock ancient wisdom, environmental mindfulness, and Gross National Happiness (GNH) values.

<a href="https://imgbb.com/"><img src="https://i.ibb.co/T5Jr42Y/Screenshot-2026-09-21-at-10-35-27-PM-2.png" alt="Screenshot 2026 09 21 at 10 35 27 PM 2" border="0"></a>


---

## 1.2 Educational Purpose & GNH Alignment

### Purpose
Cultural Revitalization: Bridge the gap between modern digital-native youth and Bhutan’s traditional heritage, spiritual oral histories, and sacred nature reverence.

Active Learning: Shift learning from passive textbook reading into an active, experiential journey through interactive dialogue choices, mindful exploration, and consequential gameplay actions.

Educational Alignment (Gross National Happiness)Cultural Preservation & Promotion: Direct engagement with Bhutanese folklore, Buddhist monastic history, local deities (Tshomen, Aum Jomo), and ancient names of the sacred land (Monyul / Lhomon).  Environmental Conservation: Interacting directly with fragile ecosystems to teach non-interference, high-altitude respect, and lake preservation.

## Subject Integration & Curricular Core

```
                             +-----------------------------------+
                             |     THE TAPESTRY OF MONYUL       |
                             +-----------------------------------+
                                               |
         +-------------------------------------+-------------------------------------+
         |                                     |                                     |
+------------------+                 +------------------+                 +------------------+
|      GNH &       |                 |  ENVIRONMENTAL   |                 |    ART, DESIGN   |
| CULTURAL VALUES  |                 |     STUDIES      |                 |   & HUMANITIES   |
+------------------+                 +------------------+                 +------------------+
| • Oral Folklore  |                 | • Interdependence|                 | • 16-bit Pixel   |
| • Sacred Nyes    |                 | • Pollution/Waste|                 |   Art Aesthetics |
| • Ley-Ju-Drey    |                 | • High-Altitude  |                 | • Architecture   |
|   (Cause-Effect) |                 |   Ecology        |                 |   Preservation   |
+------------------+                 +------------------+                 +------------------+
```



Living in Coherence with Nature: Explorations through distinct environmental ecosystems encourage reflection on the current condition of sacred spaces and human impact.

Cultural Values & Sacred Oral History: Interactive storytelling with monks, elder keepers, and deities passed down through generations.

Ley-Ju-Drey (Karma / Cause and Effect): Gameplay mechanics reinforce that every human action yields a direct environmental or spiritual reaction (e.g., disturbing sacred waters directly triggers a deity's wrath/reaction).

Art, Architecture, and Visual Humanities: Meticulous pixel art representation of Bhutanese traditional dress (Gho and Kira), architectural landmarks (Dzongs, Chortens, Stupas), and traditional iconography.

---

## 1.3 Target Audience & Classroom Integration

### Target Audience & Demographics

Primary Group: Students and youth (Ages 12–18+) studying Digital Humanities, Environmental Studies, Value Education, and Bhutanese History.

Secondary Group: Indie RPG players and international audiences interested in Himalayan culture, sacred geography, and eco-centric narrative games.

Classroom Integration Strategy
Modular Play Sessions: Structured for 30–45 minute class periods matching standard secondary school time slots.

### Subject Applications:

Value Education / GNH: Discussion on Ley-Ju-Drey and personal responsibility after playing the Drakay Pangtsho lake quest.

History & Social Studies: Examining oral traditions at Tak Tsang through dialogue with generation keepers.

Environmental Studies: Studying high-altitude alpine ecology and conservation themes at Jhomo Lhari.

---

## 1.4 Problem Statement & Value Proposition

### The Problem
As globalized lifestyles, technology, and screen time dominate modern youth culture, young generations are becoming increasingly disconnected from Bhutan's sacred oral traditions, spiritual roots, and deep-seated ecological wisdom. Traditional textbook education often feels abstract or disconnected from a student's lived experience, risking the gradual loss of intangible cultural heritage.

### The Solution / Value Proposition
The Tapestry of Monyul gamifies cultural preservation. By embedding core educational values into top-down RPG gameplay, narrative choices, and environmental puzzles, the project transforms passive observers into active participants, preserving vital Bhutanese wisdom in a medium that natively resonates with digital natives.

## 1.5 Sacred Realms (Nyes) Overview

| Realm/Nye | Deity/Character | Core Educational Concept | Gameplay Action |
| Jhomo Lhari | Aum Jomo | High-altitude ecology, sacred offerings, and spiritual respect | |
| Drakey Pangtsho | Tshomen | Right aligned | |
| Tak Tsang | Monks | Column data | |

<a href="https://ibb.co/FbrzTh5G"><img src="https://i.ibb.co/MDv70gcq/Screenshot-2026-09-21-at-10-44-47-PM-2.png" alt="Screenshot-2026-09-21-at-10-44-47-PM-2" border="0"></a>


## 1.6 Objectives
 
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
 
## 1.7 Scope of the Project
 
**Features included:**
- Full playable loop: village → dream sequence → crossroads/lobby hub →
  three realm quests → return-to-lobby sequence
- A `DialogueManager` autoload supporting branching first-visit vs.
  repeat-visit dialogue, driven by `GameState.has_seen(lore_key)`
- A `GameState` autoload tracking an `awareness` stat, a `seen_lore`
  dictionary, and per-realm completion flags
- A `Global` autoload persisting player spawn coordinates across scene
  transitions (`set_arrival_pos()` / `take_arrival_pos()`)
- A `ScreenFade` autoload controlling black/white screen transition
  overlays
- Three `TileMapLayer`-based terrain layers per world map (ground,
  props, water) with Y-sort depth ordering on the props layer
- Custom Bhutanese architectural props (Dzong, Stupa, prayer flags,
  water bowl) packed into a dedicated TileSet
- An automated GDScript test suite (11 suites, 80 tests)
**Limitations and exclusions (at time of this documentation):**
- The taxi travel mechanism (calling/entering a taxi to travel between
  the lobby and each realm) and the additional side quests developed
  later in the design process ("The Herder's Path," "Mending What's
  Shared," "The Pilgrim's Climb") are part of the design and later
  development work but are not yet reflected in the official
  `development.md`/test-suite documentation as of this writing —
  update this section once those passes are confirmed merged and
  covered by tests.
- Sound effects (distinct from any background music/ambience) are a
  planned but not-yet-fully-documented layer.
- No combat or branching-choice narrative structure.

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
