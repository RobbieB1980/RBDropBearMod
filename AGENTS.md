# AGENTS.md — Drop Bears (RBDropBearMod)

Instructions for AI assistants and humans continuing this project across sessions.

## Always do first

1. `git pull` (if git is available).
2. Read **`docs/PROGRESS.md`** (current phase).
3. Read **`docs/00-requirements.md`** for product truth.
4. Read only the extra docs needed for **this phase** (do not load the entire plan into context).
5. Implement **one phase** (or a clearly scoped slice). Do not boil the ocean.

## Always do last

1. Update `docs/PROGRESS.md` (done / next / blockers).
2. Append a short note to `docs/SESSION-LOG.md`.
3. Update `docs/DECISIONS.md` if a choice was locked.
4. Commit with a message like `Phase N: short description`.
5. `git push` so work/home stay in sync.

## Project facts

| Key | Value |
|-----|--------|
| GitHub | https://github.com/RobbieB1980/RBDropBearMod |
| Preferred local path | `D:\Grok Build\drop-bears\` (may differ on work PC) |
| Target | Bedrock **1.26.x**, `@minecraft/server` **2.0.0** for scripts |
| Namespace (default) | `drop_bears` |
| Tooling | **MCreator first**, then hand-tune scripts/JSON |
| Art v1 | **Placeholders** |

## Reference packs on the author’s home machine

- `D:\Grok Build\Ideas\Digger\` — BP/RP + script module, 1.26 manifests
- `D:\Grok Build\survival-creative-access\` — dynamic properties / script patterns

Do not assume these paths exist on every machine; clone this repo instead.

## Conventions

- **Repo-relative paths only** in docs and scripts.
- Namespace: `drop_bears` (identifiers like `drop_bears:drop_bear`).
- Prefer stable Script API; avoid Beta APIs unless documented in DECISIONS.
- New ideas → `docs/BACKLOG.md`, not silent scope changes to requirements.
- Do not commit `*.mcaddon` (see `.gitignore`) unless under an intentional `releases/` policy.
- Do not commit world saves or `%localappdata%\Packages\...\com.mojang` paths.

## Phase list (summary)

| Phase | Name |
|------:|------|
| 0 | Repo + knowledge base |
| 1 | Research notes |
| 2 | MCreator + pack skeleton |
| 3 | Blocks & items (placeholders) |
| 4 | Entity shell + loot |
| 5 | Combat (poison + fever) |
| 6 | AI disengage rules |
| 7 | Ambush + depth spawn |
| 8 | Torch repulsion |
| 9 | Biome & trees (world gen) |
| 10 | Art pass |
| 11 | Package & polish |

Full plan may also live in a Grok session `plan.md`; **this repo’s `docs/` is authoritative for day-to-day work**.

## Hard features that need scripts (expect)

- Drop-from-tree ambush
- Drop Bear Fever (custom timer / HP floor)
- Biome-depth pack size (1–5)
- Sprint + ≤50% HP disengage
- Eucalyptus torch radius-10 repel

## Do not

- Rewrite the whole mod in one session.
- Change namespace casually after packs exist.
- Paste the entire Word outline into every chat — point at `docs/00-requirements.md`.
- Force-push `main` unless the user explicitly asks.
