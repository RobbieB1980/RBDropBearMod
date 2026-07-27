# Decisions (ADR-style log)

Append-only. Newest at top.

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
