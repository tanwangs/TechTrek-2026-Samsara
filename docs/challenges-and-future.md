# Challenges & Future Enhancements

## Key Challenges & Solutions

* **Depth-Sorting Sprite Bug:** Pre-baked `frame_progress` attributes on `AnimatedSprite2D` nodes broke engine Y-sorting.
* **Solution:** Stripped `frame_progress` from scene nodes, restoring pure engine-driven depth sorting (verified by `test_prop_sorting.gd`).


* **Standalone AI Decor Sprites:** Early AI-generated props (trees, rocks) were spawned as individual `Sprite2D` nodes instead of `TileMapLayer` cells, complicating collisions.
* **Solution:** Mapped standalone sprites into `props` TileSet atlas coordinates and updated AI generation prompts to output TileMapLayer cells directly.


* **Multi-System Iteration Sequencing:** Storyline and quest redesigns created cross-system bugs when NPC placements or camera handoffs desynced from map revisions.
* **Solution:** Enforced a strict update order (map layout $\rightarrow$ NPC positions $\rightarrow$ dialogue) combined with explicit integration audits.


* **AI Model Capability Tiering:** Smaller AI models struggled with spatial map layouts matching real-world geography.
* **Solution:** Routed simple, isolated edits to faster models and reserved complex spatial/multi-system tasks for larger reasoning models.



---

## Future Enhancements

* **Expanded Test Coverage:** Add dedicated test suites for the taxi travel system and all realm side quests.
* **Dedicated SFX Layer:** Implement real-time audio feedback for mechanics (e.g., pacing cues at Jomolhari).
* **Dzongkha Localization:** Add native language/translation support for Bhutanese place names and cultural terms.
* **Classroom Resources:** Develop dedicated discussion guides and curriculum integration tools.
* **New Sacred Realms:** Add more *nyes* following the core design formula (1 unique main quest + 2 thematic side quests).
* **Accessibility Features:** Add remappable controls, text speed adjustments, and colorblind-friendly UI options.
