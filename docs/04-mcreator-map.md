# MCreator vs hand-authored map

**Status:** Phase 1 filled from generator inspection (MCreator EAP **2026.2** / `generator-addon-26.1x`).  
**Update again** when the workspace is created (Phase 2).

## Tooling

| Setting | Value |
|---------|--------|
| MCreator | **2026.2** (EAP path on home PC: `D:\Rob - Minecraft\MCreator.EAP.2026.2.22416.Windows.64bit\...`) |
| Generator | **Add-On for Bedrock Edition 26.1x** |
| modid | `drop_bears` |
| Expected export | `src/main/drop_bears_behaviourpack/`, `src/main/drop_bears_resourcepack/` |
| mcaddon | `build/export/export.mcaddon` (gitignored) |
| BP min_engine (template) | `[1, 26, 10]` |
| Script module (template) | `@minecraft/server` **2.2.0**, entry `scripts/drop_bears_scripts.js` |

## Prefer MCreator

| Content | Notes |
|---------|--------|
| Pack manifests (initial) | Template already 1.26.10 — avoid older 1.21.x generator |
| Custom blocks (log, leaves) | Placeholder textures; ore-feature optional unused |
| Custom items (oil, torch) | Torch may need hand polish if “placeable light” needed |
| Smelting recipe | Oil → torch |
| Entity shell (Drop Bear) | Placeholder model (e.g. spider/creeper base until Blockbench); hostile; loot 25% oil |
| Spawn egg + spawn rules | Rules later restricted to eucalypt biome by hand |
| Lang keys | en_US via MCreator localization |
| Script element shell | Create empty/bescript so manifest includes script module |
| Basic AI tasks | Melee attack (long memory), nearest attackable, wander — **not** panic |

## Prefer hand JSON / scripts after export

| Content | Why |
|---------|-----|
| Drop-from-tree ambush | World queries + spawn timing |
| Biome depth 1–5 packs | `Dimension.getBiome` sampling |
| Drop Bear Fever | Dynamic properties + interval damage |
| Sprint + 50% HP disengage | Precise conditions |
| Torch radius repel | Inventory + block scan (not avoid_mob_type alone) |
| Poison II on hit | MCreator entity template is damage-only; add effect JSON or script `addEffect` |
| Eucalypt Forest biome | No biome element in 26.1x generator |
| Tall tree (1 stump + branches) | No tree feature template; feature/structure JSON |
| Client biome fog/colors | Resource pack client biome files |
| Feature rules for trees | Hand JSON in BP |

## Process

1. Create/change element in **MCreator 2026.2** when possible.
2. Keep the **`.mcreator` workspace inside this git repo** (recommended path: repo root or `mcreator/`).
3. Commit generated `src/main/drop_bears_*pack` trees.
4. Apply script/JSON patches in git with clear commits; list hand-touched files below.
5. After re-export from MCreator, re-apply or merge hand patches carefully.

## Hand-touched files (fill as we go)

| Path | Reason |
|------|--------|
| *(none yet)* | Phase 1 research only |

## What MCreator will not own

- `biomes/` definitions and `minecraft:replace_biomes`
- Custom tree `features/` + `feature_rules/`
- Full `scripts/` game logic beyond empty entry (we replace/extend `drop_bears_scripts.js`)
