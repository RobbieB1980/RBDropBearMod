# Progress

**Last updated:** 2026-07-27  
**Current phase:** Phase 1 complete  
**Next phase:** Phase 2 — MCreator workspace + pack skeleton  

## Status summary

| Phase | Name | Status |
|------:|------|--------|
| 0 | Repo + knowledge base | **Done** |
| 1 | Research notes | **Done** |
| 2 | MCreator + pack skeleton | Not started |
| 3 | Blocks & items | Not started |
| 4 | Entity shell | Not started |
| 5 | Combat (poison + fever) | Not started |
| 6 | AI disengage | Not started |
| 7 | Ambush + depth spawn | Not started |
| 8 | Torch repulsion | Not started |
| 9 | Biome & trees | Not started |
| 10 | Art pass | Not started |
| 11 | Package & polish | Not started |

## Done this session (Phase 1)

- Inspected **MCreator EAP 2026.2** `generator-addon-26.1x` (templates, AI tasks, manifests, script module).
- Confirmed Creator biome options: override vs **partial replace**; biome = hand JSON.
- Locked implementation split: MCreator shell vs scripts for fever/ambush/torch/depth/disengage.
- Documented canopy + depth algorithms (`getBlock` / `getBiome`).
- Updated `01-research.md`, `04-mcreator-map.md`, `02-architecture.md`, `DECISIONS.md`.

## Next actions

1. **Phase 2:** Create MCreator 2026.2 workspace in this repo (`modid` `drop_bears`, generator 26.1x).
2. Generate empty BP/RP manifests + optional empty script entry; commit `src/main/drop_bears_*pack`.
3. Verify packs import into Minecraft 1.26.x without errors.
4. Then Phase 3: placeholder blocks/items.

## Blockers

- Phase 2 needs **interactive MCreator** on the author’s PC (we can also hand-scaffold BP/RP mirroring the generator if MCreator UI is unavailable in-session).
- Confirm Minecraft client on the machine is **≥ 1.26.10** before relying on generated `min_engine_version`.

## Playable?

**No** — research/docs only.
