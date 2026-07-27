# MCreator vs hand-authored map

**Status:** Stub for Phase 1–2. Update as the workspace is created.

## Prefer MCreator

| Content | Notes |
|---------|--------|
| Pack manifests (initial) | May hand-bump `min_engine_version` to 1.26 |
| Custom blocks (log, leaves) | Placeholder textures |
| Custom items (oil, torch item) | |
| Furnace recipe | Oil → torch |
| Entity shell (Drop Bear) | Model placeholder, basic hostile AI |
| Loot table | 25% oil |
| Spawn egg | Testing |
| Lang keys | en_US |
| Basic biome (if generator supports) | Verify in Phase 1 |

## Prefer hand JSON / scripts after export

| Content | Why |
|---------|-----|
| Drop-from-tree ambush | Needs world queries + spawn timing |
| Biome depth 1–5 packs | Custom sampling |
| Drop Bear Fever | Custom DoT + HP floor |
| Sprint + 50% HP disengage | Precise conditions |
| Torch radius repel | Inventory + block scan |
| Tree shape fine-tuning | Feature JSON may need manual edit |
| Script module wiring | Match Digger-style `manifest` script entry if MCreator omits it |

## Process

1. Create/change element in MCreator when possible.
2. Export or copy generated BP/RP into repo folders.
3. Apply script/JSON patches in git with clear commits.
4. Avoid re-exporting over hand patches without re-applying them (track hand files in this doc).

## Hand-touched files (fill as we go)

| Path | Reason |
|------|--------|
| *(none yet)* | Phase 0 |
