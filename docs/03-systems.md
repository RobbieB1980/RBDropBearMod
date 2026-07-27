# Systems design

**Status:** Spec-level design. Implementation details refined per phase.

---

## S1 — Eucalypt blocks & trees

- **Blocks:** log, leaves (placeholders); later wood set optional.
- **Tree shape:** tall trunk from **one** base stump column + side **branches** with leaves.
- **Generation:** biome feature / feature rule (Phase 9); may prototype as structure or jigsaw if easier in MCreator.

## S2 — Drop Bear entity (shell)

- Hostile mob, medium health (tune in testing; start near spider/zombie band).
- Melee reach appropriate to claws.
- Spawn egg for creative testing.
- Loot table: 25% eucalyptus oil (no guaranteed drop).

## S3 — Poison on hit

- On successful melee hit → **Poison II, 10 seconds**.
- Prefer entity component / attack effect if MCreator supports; else script `entityHurt` / projectile-free melee event.

## S4 — Drop Bear Fever

| Step | Behaviour |
|------|-----------|
| Roll | On hit, 25% apply fever if not already active (or refresh — **default: do not stack duration; keep existing timer**). |
| Tick | Every **120 seconds** (2 minutes), damage **1 heart** (2 HP) while current health **> 3 hearts** (6 HP). |
| Floor | If health ≤ 6 HP, clear fever and stop periodic damage. |
| Feedback | Periodic chat/actionbar message optional: “Drop Bear Fever…”. |
| Persist | Prefer dynamic properties so relog keeps fever until floor. |

## S5 — AI & disengage

- Default: pursue and attack players in range (relentless).
- Each AI/script tick while targeting: if target player is **sprinting** AND bear health ≤ **50% max**, clear target / flee short distance / stop attack.
- If player stops sprinting or bear heals above 50% (unlikely), re-aggro if still in range (**default: re-aggro allowed**).

## S6 — Ambush (drop from tree)

- Trigger: player moves through eucalypt forest near eucalypt leaves/logs.
- Find nearest suitable tree column; spawn Drop Bear above player or at leaf level; let gravity drop them (**visual “drop”**).
- Cooldown per player (e.g. 30–60s) to avoid spawn storms.
- Do not ambush if torch repel active (S8).

## S7 — Chop response & depth packs

| Context | Spawn count |
|---------|-------------|
| Chop eucalypt log/leaves at **biome edge** | 1 |
| Chop or ambush **deeper** | scale 2→5 by depth metric |

**Depth metric (proposal):** sample horizontal steps toward biome exterior (or count consecutive eucalypt samples in expanding rings). Normalize 0.0 (edge) → 1.0 (deep); map to spawn count 1–5. Document final algorithm in research + DECISIONS after prototype.

## S8 — Eucalyptus torch repel

- Active if player holds torch item **or** is within 10 blocks of a placed lit eucalyptus torch.
- Drop Bears within 10 blocks of the active source: do not acquire player as target; clear existing target; optionally path away.
- Ambush system respects the same check.

## S9 — Oil & crafting

- Oil item from loot.
- Furnace recipe: 1 oil → 1 eucalyptus torch (fuel rules: vanilla furnace fuel OK).
- Creative inventory groups when available.

---

## Dependency order

```text
S9/S1 items-blocks → S2 entity → S3/S4 combat → S5 AI → S1 trees+S6/S7 ambush → S8 torch
Biome (S1 gen) can lag behind combat if trees exist via commands for tests.
```
