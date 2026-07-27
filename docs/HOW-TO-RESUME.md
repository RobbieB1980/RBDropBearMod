# How to resume this project (Grok Build · work + home)

The **GitHub repo** is memory across machines and chat sessions. Grok does **not** automatically remember past chats forever — you point it at this folder and the docs.

---

## Preferred way to start a Grok Build session

### 1. Open the project folder as the workspace

| PC | What to do |
|----|------------|
| **Home** | Open / set workspace to `D:\Grok Build\drop-bears\` (or wherever you cloned) |
| **Work** | `git clone` once if needed, then open that folder as the Grok workspace |

Always run first (terminal or ask Grok):

```text
git pull
```

### 2. Tell Grok something like this

**Best (copy-paste):**

```text
Continue the Drop Bears project (RBDropBearMod).
Repo: https://github.com/RobbieB1980/RBDropBearMod
Read docs/PROGRESS.md, AGENTS.md, and only the docs needed for the current phase. Do the next phase only.
```

**Also fine:**

```text
Continue with the Drop Bears GitHub project — pull, read PROGRESS.md, next phase.
```

```text
Resume RBDropBearMod from docs/PROGRESS.md
```

You do **not** need the old Word doc or the old plan chat every time. Spec lives in `docs/00-requirements.md`.

### 3. Be explicit about the machine if it matters

```text
I'm on the WORK PC (no MCreator). Continue Drop Bears from PROGRESS.md.
```

```text
I'm on the HOME PC. Continue Drop Bears — Phase 2 MCreator checklist.
```

---

## What Grok should do every resume

Defined in `AGENTS.md`:

1. `git pull`
2. Read `docs/PROGRESS.md` → know current phase  
3. Read `docs/00-requirements.md` if implementing features  
4. Do **one phase** (or a thin slice)  
5. Update `PROGRESS.md` + `SESSION-LOG.md`  
6. `git commit` + `git push`

---

## What not to rely on

| Fragile | Better |
|---------|--------|
| “Remember what we did last week?” (old chat) | Open this repo + `PROGRESS.md` |
| Google Drive as code home | GitHub only for code/docs |
| Re-pasting the full Word outline | `docs/00-requirements.md` already has it |
| Starting Grok in `D:\` with no clone | Workspace = **this repo folder** |

---

## Quick machine matrix

| | Work | Home |
|---|------|------|
| Git pull / push | Yes | Yes |
| Edit docs | Yes | Yes |
| MCreator (Phase 2+) | **No** | **Yes** |
| Minecraft pack test | If installed | Yes |
| Hand scripts after packs exist | Yes | Yes |

Phase 2 checklist: `docs/06-phase2-home-checklist.md`.

---

## One-line cheat sheet

> **Open `drop-bears` folder → `git pull` → tell Grok: “Continue Drop Bears / RBDropBearMod from `docs/PROGRESS.md`.” → work one phase → push.**
