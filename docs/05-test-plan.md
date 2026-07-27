# Test plan

Run tests in a dedicated creative/survival test world with the BP+RP enabled. Check off when a phase claims done.

## Phase gates

### Phase 2 — Skeleton

- [ ] Packs appear in world settings and activate without error spam
- [ ] World loads with packs on

### Phase 3 — Items/blocks

- [ ] `/give` or creative: eucalypt log, leaves, oil, torch
- [ ] Furnace: oil → torch
- [ ] Place log/leaves; break as expected

### Phase 4 — Entity shell

- [ ] Summon / spawn egg Drop Bear
- [ ] Bear attacks player
- [ ] Kill yields oil ~25% over enough kills

### Phase 5 — Combat

- [ ] Hit applies Poison II ~10s
- [ ] ~25% of hits start Fever (message or observable DoT)
- [ ] Fever damages 1 heart / 2 min while HP > 3 hearts
- [ ] Fever stops at 3 hearts
- [ ] Relog keeps or intentionally clears fever (match DECISIONS)

### Phase 6 — AI

- [ ] Bear pursues relentlessly at full HP
- [ ] At ≤50% HP + player sprinting → stops attacking
- [ ] Stopping sprint allows re-aggro (if that decision stands)

### Phase 7 — Ambush / depth

- [ ] Walking under eucalypt in biome can cause drop ambush
- [ ] Cooldown prevents infinite spawns
- [ ] Edge chop → 1 bear
- [ ] Deep biome → higher counts up to 5

### Phase 8 — Torch

- [ ] Holding torch: no attack within 10 blocks
- [ ] Placed lit torch: same within 10 blocks of block
- [ ] Without torch: ambush/attack resume outside radius

### Phase 9 — Biome/trees

- [ ] New world contains eucalypt forest regions
- [ ] Trees: tall, single stump column, branches
- [ ] Distinct placeholder textures readable in-game

### Phase 11 — Release

- [ ] `.mcaddon` imports cleanly on a second machine / second world
- [ ] README install steps accurate
- [ ] Full regression of above smoke checks

## Commands useful for testing

```text
/give @s drop_bears:eucalyptus_oil
/give @s drop_bears:eucalyptus_torch
/summon drop_bears:drop_bear
# health / effect commands as needed for AI tests
```

*(Exact identifiers confirmed after Phase 2–3.)*
