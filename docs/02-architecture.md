# Architecture

**Status:** Initial — refine after Phase 2 skeleton exists.

## Pack layout (target — MCreator 26.1x)

```text
drop-bears/                        # git repo root = MCreator workspace (preferred)
├── docs/
├── README.md
├── AGENTS.md
├── *.mcreator                     # workspace file (Phase 2)
├── src/main/
│   ├── drop_bears_behaviourpack/  # BP (generator name)
│   │   ├── manifest.json          # min_engine [1,26,10]; script module
│   │   ├── entities/
│   │   ├── items/
│   │   ├── blocks/
│   │   ├── biomes/                # hand JSON (Phase 9)
│   │   ├── features/ / feature_rules/
│   │   ├── loot_tables/
│   │   ├── recipes/
│   │   ├── spawn_rules/
│   │   └── scripts/
│   │       ├── drop_bears_scripts.js   # entry (MCreator)
│   │       └── …                       # ambush, fever, torch, etc.
│   └── drop_bears_resourcepack/   # RP
│       ├── manifest.json
│       ├── entity/
│       ├── models/
│       ├── textures/
│       ├── texts/
│       └── sounds/
└── build/export/export.mcaddon    # gitignored
```

**MCreator:** Use **2026.2** generator **addon-26.1x**, `modid` `drop_bears`. See `04-mcreator-map.md`.

## Identifiers

| Kind | Pattern | Example |
|------|---------|---------|
| Namespace | `drop_bears` | — |
| Entity | `drop_bears:<name>` | `drop_bears:drop_bear` |
| Blocks | `drop_bears:<name>` | `drop_bears:eucalypt_log`, `drop_bears:eucalypt_leaves` |
| Items | `drop_bears:<name>` | `drop_bears:eucalyptus_oil`, `drop_bears:eucalyptus_torch` |

## Modules

| Module | Responsibility | Owner |
|--------|----------------|-------|
| Data (JSON) | Blocks, items, entity definition, recipes, loot, spawn rules, biome/features | MCreator + hand polish |
| Resources | Models, textures, lang, entity client | MCreator / Blockbench later |
| Scripts | Ambush, fever, depth packs, disengage assist, torch repel | Hand-authored JS |

## Scripting

- Module: `@minecraft/server` **2.2.0** (MCreator 26.1x default; prefer stable APIs).
- Entry: `scripts/drop_bears_scripts.js` (split modules later if needed).
- Player state for fever: dynamic properties (e.g. `drop_bears:fever_active`, next damage tick).
- Biome/depth: `dimension.getBiome(location)`; canopy: `dimension.getBlock` upward scan.

## Versioning

- Pack `version` and git tags: `v0.1.0` first playable (placeholders), `v1.0.0` art-complete.
- `min_engine_version`: **`[1, 26, 10]`** (MCreator template).

## Dependencies

- BP depends on RP (UUID link in manifests).
- BP script module depends on `@minecraft/server`.
