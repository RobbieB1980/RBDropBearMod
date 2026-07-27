# Research notes

**Status:** Stub — fill in Phase 1.

## Goals of research

1. Confirm how custom biomes and tree features work on Bedrock Creator pipeline (data-driven + any 1.26 changes).
2. Find patterns for: ambush spawns, custom damage-over-time “disease”, item-based mob repulsion, aggressive AI goals.
3. Map MCreator Bedrock generator capabilities vs hand-authored BP/RP/scripts for target **1.26.x**.
4. Note similar community/marketplace add-ons (biomes, hostile wildlife, tree-related ambushes) for inspiration only — do not copy assets.

## Open research questions

- [ ] Does current MCreator EAP generate addon packs compatible with `min_engine_version` `[1,26,0]`?
- [ ] Best way to detect “under eucalypt canopy” for drop-from-tree (raycast up? leaf block tags? structure bounds?).
- [ ] Best way to measure “depth into biome” (sample columns outward until non-eucalypt? noise? feature density?).
- [ ] Can custom effects show UI icons, or must fever be script-only with actionbar messages?
- [ ] Torch repel: `minecraft:behavior.avoid_mob_type` vs script `clear target` / teleport-away / set property.

## References to gather (Phase 1)

- Microsoft Learn — Minecraft Creator documentation (entities, biomes, features, scripting)
- Official behavior/resource pack samples
- Local reference: `D:\Grok Build\Ideas\Digger\` (manifest + script module style)

## Findings

*(Append dated notes below during Phase 1.)*
