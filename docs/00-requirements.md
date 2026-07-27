# Requirements — Drop Bears Survival Add-on

**Source:** `Minecraft Bedrock Project - Drop Bears.docx` (author outline)  
**Platform:** Minecraft Bedrock Edition  
**Canonical status:** This file is the product source of truth for implementation. Change only with an explicit decision entry in `DECISIONS.md`.

---

## 1. Vision

A survival-focused **mcaddon** where players exploring **eucalypt forests** risk ambush by **Drop Bears** — koala-like predators that drop from trees. Players can craft **eucalyptus oil** into **torches** that keep Drop Bears at bay.

---

## 2. Biome: Eucalypt Forest

| Requirement | Detail |
|-------------|--------|
| Identity | Own biome (not only a reskin of an existing forest). |
| Generation | Appears in world gen (spawn randomly as a biome region). |
| Blocks | Own **leaf** and **log** textures (placeholders allowed in v0.x). |
| Trees | **Tall**; **one log** for the vertical stump; **branches** (not a simple oak clone). |

**Fallback (if custom biome gen blocks progress):** plant eucalypt trees as features in existing temperate biomes and document in `DECISIONS.md`. Prefer true biome for v1.0.

---

## 3. Entity: Drop Bear

| Requirement | Detail |
|-------------|--------|
| Appearance | Based on a **koala**; **bloodshot eyes**; **large claws**. Placeholders OK early. |
| Habitat | Eucalypt forests; associated with trees. |
| Ambush | When player walks through forest, Drop Bear **drops from the nearest tree** and attacks. |
| Melee | Claw attacks. |
| Poison | Each attack applies **Poison II for 10 seconds**. |
| Fever | **25%** chance per attack to apply **Drop Bear Fever** (see §4). |
| AI tone | Fierce / relentless (comparable to creeper commitment); does not casually back down. |
| Disengage | Attack ceases **only if** the player is **running (sprinting)** **and** the Drop Bear is at **≤50% of its max health**. |
| Edge chop | Chopping eucalypt on the **outer / edge** of the biome → **one** lone Drop Bear. |
| Depth packs | Deeper into the biome → more Drop Bears, **up to a family of 5**. Count depends on **how far the player is inside the biome**. |

---

## 4. Status: Drop Bear Fever

| Requirement | Detail |
|-------------|--------|
| Trigger | 25% chance when a Drop Bear’s attack hits the player. |
| Effect | Player loses **1 heart** every **2 minutes**. |
| Accompaniment | Poison-like pressure while fever is active (implementation may use poison effect and/or script damage). |
| End condition | Continues until player health reaches **3 hearts**, then fever stops (floor — does not kill via fever alone past this). |

*Implementation note:* Bedrock may not support a custom named status effect with full UI; script + dynamic properties is acceptable if behaviour matches this table.

---

## 5. Loot and items

| Requirement | Detail |
|-------------|--------|
| Kill drop | **25%** chance to drop **eucalyptus oil**. |
| Processing | Furnace: eucalyptus oil → **eucalyptus torch**. |
| Repulsion | If the player is using this torch in the biome (lit / active), Drop Bears **stay away** within a **radius of 10 blocks** and **do not attack** while the torch condition is met. |

**Default interpretation (locked unless DECISIONS changes it):**

- **Held** eucalyptus torch (main or offhand) counts as active.
- **Placed lit** eucalyptus torch also counts for entities within 10 blocks of the block.

---

## 6. Non-functional

| Requirement | Detail |
|-------------|--------|
| Edition | Bedrock (behavior pack + resource pack; optional Script API). |
| Target version | **1.26.x** for first playable release. |
| Art | Placeholders first; final koala-like model/textures later. |
| Tooling | MCreator Bedrock generator for scaffold; scripts/JSON for hard systems. |
| Collaboration | GitHub repo is source of truth for work + home PCs. |

---

## 7. Explicit research request (from outline)

Implementation strategy should include research of **similar mods/add-ons** for ideas on:

- Ambush / tree-drop logic  
- Hostile AI structure  
- Custom biome / tree generation on Bedrock  
- Custom disease-like effects  
- Item-based mob repulsion  

Findings go in `01-research.md`.

---

## 8. Out of scope (until backlog says otherwise)

- Java Edition port  
- Marketplace certification package  
- Multiplayer-specific economy balancing beyond basic scripts  
- Boss-tier Drop Bear variants  

Add future ideas to `BACKLOG.md` without changing this file unless approved.
