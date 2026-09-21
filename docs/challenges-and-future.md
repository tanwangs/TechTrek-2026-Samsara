# Challenges & Future Enhancements

## Challenges and Solutions

### Challenge: character depth-sorting bug from AnimatedSprite2D state overrides
Characters were rendering incorrectly in front of/behind props due to
pre-baked `frame_progress` attributes on `AnimatedSprite2D` nodes
interfering with engine-driven Y-sorting.

**Solution:** stripped the pre-baked `frame_progress` attributes,
restoring pure engine-driven Y-sorting across level layers, verified by
`test_prop_sorting.gd`.

### Challenge: AI-agent-generated decoration initially bypassed the TileMapLayer terrain system
Early in development, AI-agent-generated decoration (trees, rocks,
flags) was created as standalone `Sprite2D` nodes rather than as part of
the `props` TileMapLayer, creating structural inconsistency and
complicating collision/interaction management.

**Solution:** converted existing standalone sprites into TileMapLayer
cells via a mapping between each sprite and its corresponding TileSet
source/atlas coordinates, and refined future AI-agent prompts to
explicitly specify TileMapLayer cells rather than standalone sprites.

### Challenge: iterative design revision required propagating changes across already-implemented systems
As the storyline was revised across development (protagonist
characterization, per-realm mechanic redesigns, additional side quests),
each revision required careful sequencing — e.g. map/terrain layout
changes needed to happen before dialogue/NPC-positioning revisions that
depended on final NPC placement.

**Solution:** adopted a staged, ordered prompting approach with explicit
integration-audit passes after major changes to catch cross-system
inconsistencies (camera handoff, orphaned node references, transition
ordering).

### Challenge: matching AI-agent model capability to task complexity
Some tasks (e.g. spatial map-layout generation matching real-world
geography) proved difficult for smaller/faster AI models to execute
well, while working acceptably for larger reasoning-capable models.

**Solution:** matched task complexity to model tier — smaller, faster
models for contained, well-defined edits; larger reasoning models for
multi-system or spatially complex tasks.

---

## Future Enhancements

- Full documentation and test coverage for systems developed later in
  the design process: the taxi travel mechanism, and the additional
  side quests ("The Herder's Path," "Mending What's Shared," "The
  Pilgrim's Climb")
- A dedicated sound-effect layer, including mechanically significant
  audio feedback (e.g. real-time pacing cues at Jomolhari)
- Localization/translation support, particularly for Dzongkha-language
  terms and place names, to increase cultural authenticity and
  accessibility
- Expanded classroom-integration materials (e.g. discussion guides per
  subject application)
- Additional sacred realms/nyes beyond the initial three, following the
  established design pattern (mechanically distinct main quest + two
  thematically-contrasting side quests)
- Accessibility improvements (colorblind-friendly UI, remappable
  controls, adjustable text speed)
