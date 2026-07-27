# RB Drop Bear Mod (Minecraft Bedrock)

Survival add-on: **Eucalypt Forests**, **Drop Bears** that ambush from trees, **Drop Bear Fever**, and **eucalyptus oil/torches** that keep the bears away.

| | |
|---|---|
| **Platform** | Minecraft Bedrock Edition |
| **Target** | 1.26.x (engine 26) |
| **Repo** | https://github.com/RobbieB1980/RBDropBearMod |
| **Local path (home)** | `D:\Grok Build\drop-bears\` |
| **Status** | Phase 1 complete; **Phase 2 (MCreator) = home PC only** |

## Features (planned)

- **Eucalypt Forest** biome with custom log/leaf textures and tall trees (single stump + branches).
- **Drop Bears** (koala-like): drop from trees, claw attacks apply **Poison II (10s)**.
- **25%** chance of **Drop Bear Fever** (periodic heart loss until health floors at 3 hearts).
- Aggressive AI; flees/disengages only if the player is **sprinting** and the bear is at **≤50% HP**.
- Biome **depth** scales ambush size (edge: 1; deep: up to 5).
- Kill drops **eucalyptus oil** (25%) → furnace → **eucalyptus torch** (repels bears in **10-block** radius while active).

Full requirements: [`docs/00-requirements.md`](docs/00-requirements.md).

## Install (when packs exist)

1. Build or download the `.mcaddon` (later phases).
2. Double-click to import, or copy BP/RP into the world’s behavior/resource packs.
3. Enable both packs on the world. Prefer **no cheats** unless testing with commands.

*Packs are not in the repo yet — see `docs/PROGRESS.md`.*

## Multi-machine (work + home)

This repo is the **source of truth**. Do not rely on Google Drive for the code tree.

**Full resume guide:** [`docs/HOW-TO-RESUME.md`](docs/HOW-TO-RESUME.md)

### Grok Build — how to pick up this project

1. Open **this folder** as the Grok workspace (not just `D:\`).
2. `git pull`
3. Say something like:

```text
Continue the Drop Bears project (RBDropBearMod).
Read docs/PROGRESS.md, AGENTS.md, and only the docs for the current phase. Do the next phase only.
```

Or shorter: `Continue Drop Bears from docs/PROGRESS.md` / `Resume RBDropBearMod`.

Add `I'm on WORK PC (no MCreator)` or `I'm on HOME PC` when relevant.

### Git each session

```text
git pull
# work one phase
git add -A
git commit -m "Phase N: …"
git push
```

Prefer one machine actively editing `main` at a time.

## Docs map (token-limit strategy)

| File | Purpose |
|------|---------|
| [`docs/HOW-TO-RESUME.md`](docs/HOW-TO-RESUME.md) | Work/home + Grok pickup phrases |
| [`docs/00-requirements.md`](docs/00-requirements.md) | Canonical feature spec |
| [`docs/PROGRESS.md`](docs/PROGRESS.md) | Current phase, next steps |
| [`docs/DECISIONS.md`](docs/DECISIONS.md) | Locked design choices |
| [`AGENTS.md`](AGENTS.md) | Instructions for AI/coding sessions |
| [`docs/SESSION-LOG.md`](docs/SESSION-LOG.md) | Per-session notes |

Every coding session should read `PROGRESS.md` + requirements, implement **one phase**, update docs, commit, and push.

## Development approach

1. **MCreator** Bedrock generator for scaffold (blocks, items, entity shell, recipes).
2. **Hand scripts / JSON** for ambush, fever, depth spawn, torch repel, AI disengage (see `docs/04-mcreator-map.md` after Phase 1).
3. **Placeholders first**, art/Blockbench later (Phase 10).

## License / credits

TBD. Project outline originally captured in `Minecraft Bedrock Project - Drop Bears.docx`.
