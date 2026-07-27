# Architecture

**Status:** Initial — refine after Phase 2 skeleton exists.

## Pack layout (target)

```text
drop-bears/
├── docs/                          # Knowledge base (this tree)
├── README.md
├── AGENTS.md
├── drop_bears_BP/                 # Behavior pack (name may match MCreator export)
│   ├── manifest.json
│   ├── pack_icon.png
│   ├── entities/
│   ├── items/
│   ├── blocks/
│   ├── biomes/                    # if used
│   ├── features/ / feature_rules/
│   ├── loot_tables/
│   ├── recipes/
│   ├── spawn_rules/
│   ├── texts/
│   └── scripts/
│       └── main.js                # ambush, fever, depth, torch, AI assists
└── drop_bears_RP/                 # Resource pack
    ├── manifest.json
    ├── pack_icon.png
    ├── entity/
    ├── models/
    ├── textures/
    ├── texts/
    └── sounds/                    # optional later
```

**MCreator:** Workspace may live under `mcreator/` or as `*.mcreator` + `src/` — decide in Phase 2 and record in `DECISIONS.md`. Prefer exporting or syncing into `drop_bears_BP` / `drop_bears_RP` so Minecraft testing and git stay simple.

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

- Module: `@minecraft/server` **2.0.0** (stable; match Digger when possible).
- Entry: `scripts/main.js` (split into modules later if file grows).
- Player state for fever: dynamic properties (e.g. `drop_bears:fever_until` / tick counters).

## Versioning

- Pack `version` and git tags: `v0.1.0` first playable (placeholders), `v1.0.0` art-complete.
- `min_engine_version`: prefer `[1, 26, 0]`.

## Dependencies

- BP depends on RP (UUID link in manifests).
- BP script module depends on `@minecraft/server`.
