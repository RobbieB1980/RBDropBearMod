# Decisions (ADR-style log)

Append-only. Newest at top.

---

## 2026-07-27 — Phase 2 home-only

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Where Phase 2 runs | **Home PC only** | MCreator is blocked on work PC |
| Work PC role until Phase 2 ships | Docs / git only for pack creation; no fake skeleton required | Avoid diverging from MCreator-generated layout |
| Home checklist | `docs/06-phase2-home-checklist.md` | Single place for resume after machine switch |

---

## 2026-07-27 — Phase 1 research lock-ins

| Decision | Choice | Rationale |
|----------|--------|-----------|
| MCreator version | **2026.2** + generator **addon-26.1x** | Present on home PC; matches engine 26; older 1.21.x generator is insufficient |
| Engine / script versions | `min_engine_version` **[1, 26, 10]**; `@minecraft/server` **2.2.0** | Match MCreator 26.1x templates (Digger used 2.0.0 / [1,26,0] — adopt MCreator’s higher bar) |
| Workspace layout | MCreator project **inside git repo**; packs at `src/main/drop_bears_behaviourpack` + `_resourcepack` | Matches generator.yaml; versioned source of truth |
| Biome implementation | Hand JSON **partial biome replacement** / custom biome (Phase 9); not MCreator | Generator has no biome element |
| Trees | Hand feature/structure JSON | Generator only has simple ore-style features |
| Poison II | Hand entity attack effect **or** script `addEffect` | MCreator living entity template is damage-only |
| Fever / ambush / depth / torch / disengage | **Script** | Requires world/player queries and custom timers |
| Depth metric | Distance-to-edge via `getBiome` sampling; fallback eucalypt block density | Stable Script API `Dimension.getBiome` |
| Canopy ambush | Upward `getBlock` for eucalypt leaves + biome check | Simple, no structure query API needed |

---

## 2026-07-27 — Project kickoff defaults

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Platform | Bedrock add-on (BP + RP + scripts) | Author outline + existing Bedrock tooling |
| Target version | **1.26.x** / engine 26 | Match recent Digger-style packs |
| Tooling | **MCreator first**, hand scripts for hard systems | Author preference; speed for shell content |
| Art v1 | **Placeholders** | Ship systems before art |
| Multi-machine | **GitHub** https://github.com/RobbieB1980/RBDropBearMod | Work + home; better than Drive for code |
| Local path (home) | `D:\Grok Build\drop-bears\` | Next to other Grok Build projects |
| Namespace | **`drop_bears`** | Clear, unique |
| Torch repel | **Held (main/offhand) OR placed lit**, radius **10** | Spec + practical play |
| Fever stacking | **No stack**; keep existing fever if already active | Simpler; avoid infinite timers |
| Re-aggro after disengage | **Allowed** when sprint stops / conditions fail | Keeps threat real |
| Knowledge base | `docs/*` + `AGENTS.md` session protocol | Survive token limits and multi-session work |

---

## Template for future entries

```markdown
## YYYY-MM-DD — Title

| Decision | Choice | Rationale |
|----------|--------|-----------|
| … | … | … |
```
