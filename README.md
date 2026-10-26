# agents.md

A battle-tested, universal operational ruleset, safety standard, and behavioral invariant guide for AI coding agents (**Antigravity**, **Claude Code**, **Cursor**, **Codex**, **Gemini**, etc.).

Designed to eliminate common agent failure modes—such as unprompted destructive git commits, phantom documentation drift, brittle backward-compatibility shims during pre-production, lazy one-line patches without trade-off analysis, and zombie code accumulation.

---

## 🎯 Core Operating Posture

> **Treat every codebase as a high-integrity, production-grade system—in active pre-production development unless explicitly specified otherwise.**

Prioritizes correctness, architectural cleanliness, testability, and operational predictability over rapid, unverified churn. Because projects in active development are not yet live, agents are instructed to execute clean architectural refactors and schema updates directly without fear of breaking obsolete prototypes or past test rows, while safely quarantining retired files rather than permanently deleting them.

---

## 🏛️ The 7 Universal Rules

| Rule | Title | Summary |
| :--- | :--- | :--- |
| **Rule 1** | **Git & Execution Safety** | The human commits. AI is strictly forbidden from executing `git commit` or destructive operations (`checkout`, `reset --hard`, `stash`). Includes built-in Conventional Commits formatting helper. |
| **Rule 2** | **Multi-Option Planning & Doubt Gate** | Mandatory 2–3 competing alternatives for non-trivial tasks with real trade-offs (CLS, race conditions, memory leaks, spotty offline states). Banned trivial cons (*"adds a file"*). Includes the Trivial-Change Exception, Favor Simplicity, and token-conscious surgical execution. |
| **Rule 3** | **Living Documentation & Post-Session Protocol** | Mandatory reconciliation across architecture docs, roadmaps, known issues, and ADRs. Enforces "Living Guidance, Not Dogma" and subtle Semantic Version bumping. |
| **Rule 4** | **Safe Quarantine & Zero Deletion** | Never delete files unilaterally. Obsolete or replaced files must be safely quarantined (`.discard/` or `_discarded/`) or confirmed with the user. User backups and copies are strictly protected. |
| **Rule 5** | **Pre-Flight Verification & Quality Gates** | Ordered quality pipeline: Strict Types $\rightarrow$ Linting $\rightarrow$ Test Suites (100% pass) $\rightarrow$ Clean Production Build (exit code `0`) before concluding any work. |
| **Rule 6** | **Tooling, Links & Communication Discipline** | Prefer native MCP tools (Supabase, Context7, Firecrawl, Chrome DevTools, etc.) over disposable scripts. Clickable `file:///` URLs and high-density, concise prose. |
| **Rule 7** | **Pre-Production Agility vs. Production Stability** | Direct schema/architectural migrations during pre-production; strict backward-compatibility safeguards only when live production users exist. |

---

## 🚀 How to Use

### 1. Global (Machine-Wide) — Recommended
Place [`AGENTS.md`](./AGENTS.md) in your user configuration directory so every coding session inherits these rules automatically across all workspaces:

- **Antigravity / Gemini:** `~/.gemini/config/AGENTS.md` (or `~/.agents/AGENTS.md`)
- **Claude Code / OpenCode:** `~/.agents/AGENTS.md`
- **Cursor / Windsurf / VS Code:** Symlink or copy to your global rules folder or project root.

### 2. Workspace / Repository Root
Drop [`AGENTS.md`](./AGENTS.md) directly into the root of any repository:
```bash
curl -o AGENTS.md https://raw.githubusercontent.com/Jabir-A-H/agents.md/main/AGENTS.md
```

### 3. Parent / Monorepo Directory
Place [`AGENTS.md`](./AGENTS.md) in a parent folder (e.g. `~/Developer/AGENTS.md` or `D:\WebDev\AGENTS.md`). Hierarchical agent runners will automatically discover and enforce it for all sub-repositories.

---

## 📄 License
[MIT](LICENSE) © [Jabir A.H](https://github.com/Jabir-A-H)
