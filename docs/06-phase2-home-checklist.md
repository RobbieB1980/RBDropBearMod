# Phase 2 — Home PC checklist (MCreator)

**Why home only:** MCreator is **blocked on the work PC**. Phase 2 must run on the **home PC** where MCreator EAP **2026.2** and Minecraft Bedrock are available.

**Do not start Phase 2 on work.** Work PC can still `git pull`, edit docs/scripts later, but **not** create the MCreator workspace.

---

## Before you start (home)

1. `git pull` on the repo (preferred path: `D:\Grok Build\drop-bears\`).
2. Read `docs/PROGRESS.md` + this file + `docs/04-mcreator-map.md`.
3. Confirm:
   - MCreator **2026.2** launches  
     (`D:\Rob - Minecraft\MCreator.EAP.2026.2.22416.Windows.64bit\...` or your install)
   - Generator plugin includes **Bedrock Edition 26.1x** / `generator-addon-26.1x`
   - Minecraft Bedrock client is **≥ 1.26.10** (matches generated `min_engine_version`)

---

## Create the workspace

1. Open **MCreator 2026.2**.
2. **New workspace** → **Minecraft Bedrock Edition Add-On** (26.1x), not Java/NeoForge.
3. Settings (match research):

   | Field | Value |
   |-------|--------|
   | Mod / pack name | `Drop Bears` or `RB Drop Bear Mod` |
   | Mod ID / namespace | **`drop_bears`** |
   | Author | your name |
   | Workspace folder | **Inside the git repo**, e.g. `D:\Grok Build\drop-bears\` (repo root) **or** `D:\Grok Build\drop-bears\mcreator\` if you prefer a subfolder — if subfolder, still commit the generated packs into git |

4. Prefer **repo root as workspace** so output is:
   ```text
   src/main/drop_bears_behaviourpack/
   src/main/drop_bears_resourcepack/
   ```
   as in `docs/02-architecture.md`.

5. Save. Confirm a `*.mcreator` file appears under the workspace path.

---

## Minimal Phase 2 content (skeleton only)

Do **not** build full features yet (that is Phases 3+). Only enough to export a loadable add-on:

1. **Pack icon** — any 128×128 placeholder (MCreator will copy to both packs).
2. **Script element (recommended)** — create one empty Bedrock script so the BP manifest gets a `script` module and `@minecraft/server` dependency. Entry will be like `scripts/drop_bears_scripts.js`.
3. Optional: one dummy item **or** skip items until Phase 3 — empty packs with manifests only is fine if MCreator allows export.

4. **Build / export** once (`export.mcaddon` under `build/export/` — gitignored).

---

## Verify in Minecraft (home)

1. Import `build/export/export.mcaddon` **or** copy:
   - `src/main/drop_bears_behaviourpack` → world’s behavior packs  
   - `src/main/drop_bears_resourcepack` → resource packs  
2. Create/open a test world → enable both packs.
3. Confirm world loads with **no red pack errors**.
4. Note engine version in `docs/SESSION-LOG.md` if anything warns about version mismatch.

---

## Git (home — required before leaving the PC)

```text
git pull
git add -A
git status   # should show .mcreator, src/main/drop_bears_*pack, etc. — not build/export/*.mcaddon
git commit -m "Phase 2: MCreator 26.1x workspace and empty pack skeleton"
git push
```

Then update:

- `docs/PROGRESS.md` → Phase 2 **Done**, next = Phase 3  
- `docs/SESSION-LOG.md` → short home session note  
- `docs/04-mcreator-map.md` → list actual generated paths if they differ  

---

## Exit criteria (Phase 2 done)

- [ ] MCreator workspace in repo (or documented subfolder)
- [ ] `src/main/drop_bears_behaviourpack/manifest.json` and RP manifest exist
- [ ] Script module present if scripts were added (preferred)
- [ ] Packs activate in Minecraft without errors
- [ ] Changes **committed and pushed** to https://github.com/RobbieB1980/RBDropBearMod

---

## If something goes wrong

| Problem | Action |
|---------|--------|
| Only 1.21.x generator available | Wrong MCreator install — use **2026.2** EAP with addon-26.1x |
| Workspace outside git | Move/copy into repo or re-create; always push packs |
| Work PC next day | `git pull` only; continue Phase 3+ only if no MCreator needed, or wait for home again |
| Export overwrites hand scripts later | Re-apply hand patches; track files in `04-mcreator-map.md` |

---

## Work PC (allowed now)

- Edit docs, research, planning
- Later: pure script/JSON hand edits **after** Phase 2 packs exist on GitHub  
- **Not allowed:** running MCreator, claiming Phase 2 complete without home export
