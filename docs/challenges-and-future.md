# Challenges & Future Enhancements

## Key Challenges & Solutions

* **Depth-Sorting Sprite Bug:** Pre-baked `frame_progress` attributes on `AnimatedSprite2D` nodes broke engine Y-sorting.
<a href="https://imgbb.com/"><img src="https://i.ibb.co/YBJw9Xcx/Screenshot-2026-09-20-at-9-26-19-PM.png" alt="Screenshot 2026 09 20 at 9 26 19 PM" border="0"></a>
* **Solution:** Stripped `frame_progress` from scene nodes, restoring pure engine-driven depth sorting (verified by `test_prop_sorting.gd`).

<a href="https://ibb.co/k6JQYGSP"><img src="https://i.ibb.co/PzMwBr6V/Screenshot-2026-09-22-at-12-58-08-AM.png" alt="Screenshot-2026-09-22-at-12-58-08-AM" border="0"></a>

* **Standalone AI Decor Sprites:** Early AI-generated props (trees, rocks) were spawned as individual `Sprite2D` nodes instead of `TileMapLayer` cells, complicating collisions.

<a href="https://imgbb.com/"><img src="https://i.ibb.co/gZ1L1Pgw/Screenshot-2026-09-22-at-12-58-56-AM.png" alt="Screenshot 2026 09 22 at 12 58 56 AM" border="0"></a>
* **Solution:** Mapped standalone sprites into `props` TileSet atlas coordinates and updated AI generation prompts to output TileMapLayer cells directly.

<a href="https://imgbb.com/"><img src="https://i.ibb.co/PZsn18HN/Screenshot-2026-09-22-at-12-59-33-AM.png" alt="Screenshot 2026 09 22 at 12 59 33 AM" border="0"></a>

* **AI Model Capability Tiering:** AI models struggled with map layouts matching real-world geography.

<a href="https://ibb.co/RTxTBNt6"><img src="https://i.ibb.co/Qv2vCkhH/Screenshot-2026-09-22-at-1-01-49-AM.png" alt="Screenshot-2026-09-22-at-1-01-49-AM" border="0"></a>
* **Solution:** I did it myself.

<a href="https://ibb.co/GQkpscXM"><img src="https://i.ibb.co/zVbx8G12/Screenshot-2026-09-22-at-1-04-03-AM.png" alt="Screenshot-2026-09-22-at-1-04-03-AM" border="0"></a>


---

## Future Enhancements

* **Expanded Test Coverage:** Add dedicated test suites for the taxi travel system and all realm side quests.
* **Dedicated SFX Layer:** Implement real-time audio feedback for mechanics (e.g., pacing cues at Jomolhari).
* **Dzongkha Localization:** Add native language/translation support for Bhutanese place names and cultural terms.
* **Classroom Resources:** Develop dedicated discussion guides and curriculum integration tools.
* **New Sacred Realms:** Add more *nyes* following the core design formula (1 unique main quest + 2 thematic side quests).
* **Accessibility Features:** Add remappable controls, text speed adjustments, and colorblind-friendly UI options.
