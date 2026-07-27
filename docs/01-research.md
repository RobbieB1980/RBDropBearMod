# Research notes

**Status:** Phase 1 complete (2026-07-27)  
**Target:** Bedrock **1.26.x** / engine 26, namespace `drop_bears`

## Goals of research

1. Confirm how custom biomes and tree features work on Bedrock Creator pipeline.
2. Find patterns for ambush spawns, custom DoT “disease”, item-based mob repulsion, aggressive AI.
3. Map MCreator Bedrock generator capabilities vs hand-authored BP/RP/scripts for **26.1x**.
4. Note similar add-ons for inspiration only (do not copy assets).

---

## Open research questions — answers

| Question | Answer |
|----------|--------|
| Does current MCreator generate 1.26-compatible packs? | **Yes.** Home machine has **MCreator EAP 2026.2** with `generator-addon-26.1x.zip`. Manifest template sets `min_engine_version: [1, 26, 10]` and script dependency `@minecraft/server` **2.2.0**. Older installs only have `generator-addon-1.21.x` — use **2026.2** for this project. |
| Detect “under eucalypt canopy”? | **Script:** from player position, scan upward with `dimension.getBlock` for `drop_bears:eucalypt_leaves` (and/or log) within ~8–16 blocks; require player in eucalypt biome via `dimension.getBiome(location).id`. Optional: tag leaves/logs with a block tag if we add one. |
| Measure “depth into biome”? | **Script:** if player biome is eucalypt, sample horizontal ring/steps outward with `getBiome` until non-eucalypt; distance-to-edge maps to depth 0→1 → spawn count 1–5. Fallback if custom biome delayed: use density of eucalypt blocks in a radius. |
| Custom effects UI for fever? | **No practical custom effect icon** for full vanilla-style UI without experiments/hacks. Implement **Drop Bear Fever in script** + actionbar/chat feedback. Poison II for claw hits can use vanilla effect via `entity.addEffect("poison", 200, { amplifier: 1 })` (10s = 200 ticks) or entity attack effect JSON. |
| Torch repel: avoid AI vs script? | MCreator has `minecraft:behavior.avoid_mob_type`, but that filters by **entity family**, not “player holding item”. **Script is required** for held/placed torch checks. Optionally combine with a temporary family/tag on protected players (advanced). |

---

## Findings

### 1. Local tooling (author machine)

| Install | Bedrock addon generator | Use for Drop Bears? |
|---------|-------------------------|---------------------|
| `MCreator.EAP.2026.2.22416` | **`generator-addon-26.1x`** | **Yes — primary** |
| `MCreator.EAP.2026.1.10319` | `generator-addon-1.21.x` | Only if forced; then hand-bump manifests |
| Older `Mcreator\` | `generator-addon-1.21.x` | No |

**MCreator 26.1x generator supports (from plugin templates):**

- Living entities (with AI tasks: melee attack, avoid entity, wander, leap, etc.)
- Blocks, items, recipes (including **smelting**), loot tables
- Spawn rules, spawn eggs
- **Scripts** (`bescript` → `scripts/<modid>_scripts.js` + per-script files)
- Functions (mcfunction)
- Block ore **feature / feature_rule** (not full custom trees)

**MCreator 26.1x does NOT generate:**

- Custom **biome** elements
- Custom **tree** feature graphs (only ore-style block features in templates)
- Attack-applied **status effects** on the living-entity template by default (`minecraft:attack` is damage-only)
- Complex structure trees

**Generated layout (from `generator.yaml`):**

```text
@WORKSPACEROOT/src/main/@modid_behaviourpack/
@WORKSPACEROOT/src/main/@modid_resourcepack/
build/export/export.mcaddon
```

Manifest BP: `min_engine_version` **[1, 26, 10]**; script module `@minecraft/server` **2.2.0**.

**Decision for Phase 2:** Use MCreator **2026.2** + **Bedrock Edition 26.1x**, `modid` = `drop_bears`. Prefer workspace **inside the git repo** so BP/RP export paths stay versioned.

### 2. Custom biomes (Creator docs)

Microsoft documents two patterns:

1. **Override** an existing Overworld biome identifier (full replace of that vanilla biome definition).
2. **Partial biome replacement** (`minecraft:replace_biomes`) — insert a new biome over a fraction of vanilla biomes.

Notes from docs (as of research date):

- Partial replacement historically tied to Custom Biomes experiment; docs also state **partial replacement available without experimental toggle from ~1.21.110** (format version ≥ 1.21.110). Still verify on target 1.26 client when implementing Phase 9.
- Client look (fog, water color, etc.) uses **client biome** JSON in the resource pack.
- Samples: Microsoft **Chill Oasis** blocks/features sample on GitHub.

**Implication for Drop Bears:** Eucalypt Forest should be a **new biome** via `replace_biomes` targeting temperate forests (e.g. forest, birch_forest, taiga-like) — not only a texture pack. This is **hand JSON** (or post-MCreator), **not** an MCreator element today.

**Fallback (already in requirements):** If biome gen is unstable, place eucalypt **tree features** into existing biomes so combat/ambush can ship first.

### 3. Trees / features

- World gen pipeline: biomes → surface → **features** (trees, ores, vegetation).
- Tall “1 stump + branches” tree will need custom **feature** JSON and/or a **structure** in `structures/`, plus feature rules restricted to eucalypt biome tags.
- MCreator only scaffolds simple ore-style block features → **hand-author tree** (or Blockbench structure + structure feature).

### 4. Entity combat & AI

| Need | Approach |
|------|----------|
| Hostile pursuit | MCreator: mob behaviour + `melee_attack` / attack-on-collide style AI tasks |
| Claw Poison II 10s | Prefer **hand-edit** entity `minecraft:attack` with effect, **or** script on `entityHurt` / hit detection: `addEffect("poison", 200, { amplifier: 1 })` |
| Relentless AI | High follow range; avoid panic/flee AI; long-memory melee (`attack_once: false` in MCreator melee task) |
| Disengage sprint + ≤50% HP | **Script** interval: if target is player sprinting and `health/current ≤ 0.5 * max`, clear target / apply short avoid |
| Family of 5 | Scripted spawns, not vanilla herd components |

Bedrock Wiki: entity attacks need navigation + attack components; mob effects on hit are a known pattern for vanilla-style effects (poison list includes `poison`).

### 5. Drop Bear Fever (custom disease)

| Concern | Approach |
|---------|----------|
| Not a real custom effect | Script simulation |
| Persist across relog | Player **dynamic properties** (e.g. `drop_bears:fever_active`, last tick / next damage time) |
| 1 heart / 2 minutes | `system.runInterval` every N ticks; every 2400 ticks (2 min) apply 2 damage while HP > 6 |
| Floor at 3 hearts | Stop when `getComponent("minecraft:health").currentValue ≤ 6` |
| 25% on hit | On damage from Drop Bear type family, `Math.random() < 0.25` |
| Feedback | `player.onScreenDisplay.setActionBar` or `sendMessage` |

API anchors: `Entity.addEffect`, dynamic properties on player, `world.afterEvents.entityHurt` (or equivalent stable event in 2.2.0).

### 6. Ambush (drop from tree)

Recommended algorithm (script):

1. Throttle per player (cooldown dynamic property / Map).
2. Skip if torch repel active.
3. Require biome = eucalypt (or fallback: eucalypt leaves nearby).
4. Confirm canopy: upward scan finds `eucalypt_leaves`.
5. `dimension.spawnEntity("drop_bears:drop_bear", { x, y: canopyY, z })` above player; gravity drops them.
6. Optional small horizontal offset toward nearest leaf column.

**Chop response:** subscribe to player break block; if block is eucalypt log/leaves and in/near biome, spawn 1–5 by depth metric with separate chop cooldown.

### 7. Torch repulsion (radius 10)

Script tick (or every 5–10 ticks for perf):

1. For each player: active if main/offhand item is eucalyptus torch **or** any placed lit eucalyptus torch within 10 blocks (block scan or tracked placed positions).
2. For each Drop Bear within 10 of an active source: clear attack target; optional `teleport` / impulse away; skip ambush rolls.

Do not rely solely on `avoid_mob_type` (entity-family based).

### 8. Script API version alignment

| Reference | `@minecraft/server` | min_engine |
|-----------|---------------------|------------|
| Digger (local) | 2.0.0 | [1, 26, 0] |
| MCreator 26.1x template | **2.2.0** | **[1, 26, 10]** |
| Drop Bears (follow MCreator) | **2.2.0** | **[1, 26, 10]** |

Hand scripts should match MCreator’s 2.2.0 once the workspace exists. Prefer stable APIs; document any beta use in `DECISIONS.md`.

### 9. Similar mods / inspiration (no asset reuse)

| Reference | Useful idea |
|-----------|-------------|
| Marketplace / community “more biomes” packs | Biome identity, fog, custom trees feel |
| Aggressive wildlife / “ambush” mobs (e.g. cave-ambush style add-ons) | Tension, spawn cooldowns, audio stingers later |
| Microsoft Chill Oasis sample | Official biome + custom blocks/features structure |
| Local Digger / SCA | Manifest + script module patterns, dynamic properties |

---

## Recommended implementation split (Phase 1 conclusion)

| System | MCreator | Hand JSON | Script |
|--------|:--------:|:---------:|:------:|
| Pack shell, icons | ✓ | | |
| Log, leaves, oil, torch item | ✓ | polish | |
| Smelting oil → torch | ✓ | | |
| Drop Bear shell + loot 25% | ✓ | | |
| Basic hostile AI | ✓ | tune | |
| Poison on hit | | ✓ preferred | ✓ fallback |
| Fever | | | ✓ |
| Sprint + 50% disengage | | | ✓ |
| Ambush + chop packs | | | ✓ |
| Torch repel | | | ✓ |
| Eucalypt biome | | ✓ | depth uses getBiome |
| Tall tree feature | | ✓ | optional structure place |

---

## Official / primary links

- [Biome JSON and Overview](https://learn.microsoft.com/en-us/minecraft/creator/documents/biomes/biomeoverview?view=minecraft-bedrock-stable)
- [Custom Biome Tutorial](https://learn.microsoft.com/en-us/minecraft/creator/documents/biomes/custombiometutorial?view=minecraft-bedrock-stable)
- [Partial Biome Replacements](https://learn.microsoft.com/en-us/minecraft/creator/documents/biomes/custompartialbiomereplacement?view=minecraft-bedrock-stable)
- [World Generation Overview](https://learn.microsoft.com/en-us/minecraft/creator/documents/world-generation?view=minecraft-bedrock-stable)
- [Dimension.getBiome / getBlock](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/dimension?view=minecraft-bedrock-stable)
- [Entity.addEffect](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/entity?view=minecraft-bedrock-stable)
- [MCreator 2026.2 Bedrock notes](https://mcreator.net/news/123730/minecraft-mod-maker-mcreator-20262-armor-trims-custom-skyboxes-bedrock-edition)
- Chill Oasis sample: `https://github.com/microsoft/minecraft-samples/tree/main/chill_oasis_blocks_and_features`

---

## Phase 1 exit checklist

- [x] MCreator 26.1x compatibility confirmed on author PC  
- [x] Biome approach: partial replace / custom biome JSON (hand)  
- [x] Fever / ambush / torch / depth → script  
- [x] Poison → effect API or entity attack JSON  
- [x] MCreator map updated (`04-mcreator-map.md`)  
- [x] Decisions logged for engine + script module versions  
