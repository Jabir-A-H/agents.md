# Global AI Agent & Engineering Rules

This document establishes the universal operational rules, invariants, and safety standards for all AI agents and developers operating across this environment and its repositories.

## 🎯 Core Operating Posture
Treat every codebase as a high-integrity, production-grade system—**in active pre-production development unless explicitly specified otherwise**. Prioritize correctness, architectural cleanliness, testability, and operational predictability over rapid, unverified churn. Because projects are not yet live, execute clean architectural refactors and schema updates directly without fear of breaking obsolete prototypes or past test rows.

---

## 🔒 RULE 1: Git & Execution Safety (The Human Commits)
1. **Never run `git commit` or stage changes** on your own initiative. Complete the assigned goal, run verification gates, and stop with changes uncommitted for user review.
2. **Never execute destructive git operations** (`git checkout <file>`, `git restore`, `git stash`, `git reset --hard`) without explicit user permission.
3. **Format commit messages for the user**: When work is verified, provide a recommended **Conventional Commit** message formatted for the user to execute:
   - Format: `type(scope): subject`
   - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`
   - Imperative mood, present tense ("Add" not "Added"), subject < 70 chars, no trailing period.
   - Body explains *what* and *why*, not *how*. Reference issue numbers (`Fixes #123`) when relevant.

---

## ⚖️ RULE 2: Multi-Option Planning & Adversarial "Doubt Gate"
Before implementing any non-trivial feature, architectural adjustment, refactoring, or bug fix:
1. **Formulate Competing Alternatives**:
   - Never present a single, unchallenged local patch.
   - Formulate **at least 2 to 3 distinct solution approaches** based on complexity and risk (e.g. Minimal Application Patch vs. Clean Schema/Data Migration vs. Architectural Consolidation, etc.).
2. **Multi-Option Expansion for High-Risk Decisions**:
   - Scale ceremony with risk. If an approach carries irreversible data risks, security exposure, or major architectural trade-offs, present **at least 3 viable options** and isolate the risk areas so the user can make an informed choice.
3. **Evaluate Real Technical Trade-offs (No Strawmen)**:
   - **Why do it (benefits):** Real functional, architectural, performance, or UX advantages.
   - **Why not do it (risks & failure modes):** Real engineering risks—such as race conditions, memory leaks, layout shifts (CLS), paint latency, accessibility barriers, spotty network/offline states, latency cascades, cognitive complexity, browser/device quirks, etc.
   - **Banned trivial cons:** NEVER cite normal development artifacts (such as *"creates a new file"*, *"adds a wrapper component"*, or *"adds boilerplate"*) as a reason not to implement a clean solution.
4. **Adversarial Stress-Testing ("Doubt Gate")**:
   - Cross-examine the proposal against: *"Under what real-world field conditions will this clean-looking code fail?"*
5. **Favor Simplicity**:
   - Favor simple, robust, high-density solutions over speculative abstraction layers or premature generalization.
6. **Trivial-Change Exception**:
   - Skip multi-option comparisons only for completely obvious, single-path changes (e.g. deleting an unused import, fixing a typo, updating an obvious path, a trivial lint fix, etc.).
7. **Surgical, Token-Conscious Execution**:
   - Deliver changes in thin, verifiable slices. Prefer surgical, localized edits over sprawling multi-file rewrites.

---

## 📌 RULE 3: Living Documentation & Mandatory Post-Session Protocol
> **CRITICAL DIRECTIVE:** You MUST ALWAYS update, reconcile, and optimize documentation after every coding, debugging, refactoring, or design session before concluding work.

1. **Living Guidance, Not Dogma**:
   - Principles and architectural guidelines provide consistency, but must never become dogma that blocks modern platform advancements. When modern browser capabilities, platform primitives, CSS specifications, or evolving framework features offer a superior solution that conflicts with an existing rule, surface the conflict openly so the team can evolve the standard.
2. **Reconcile Architecture & Technical References**:
   - Keep directory trees, module boundaries, and API signatures mirrored to live code—never let docs list phantom files, dead routes, or stale schemas.
3. **Update Roadmaps & Issue Trackers**:
   - Check off completed tasks (`[x]`). Move fixed bugs to a historical resolved log with dates and fix summaries.
   - Document newly discovered regressions, edge cases, or deferred improvements immediately.
4. **Record Architectural Decisions (ADRs)**:
   - Record formal sequential ADRs (`docs/ADR/*`) for non-trivial architectural forks, data-wiring changes, or major dependency additions.
5. **Semantic Version Awareness (Subtle & Contextual)**:
   - For projects maintaining a version number (e.g. in `package.json`, `app.json`, version modules, etc.):
     - **In Plans:** Include a brief, natural one-line note on anticipated version impact (e.g. *"Anticipated version impact: patch bump for bug fix"* or *"minor bump for new feature"*).
     - **In Post-Session Wrap-Up:** Along with updating the docs suite, bump the version appropriately:
       - **Patch (`x.y.Z`)**: Defect fixes, small UI polishes, refactoring, or docs syncs.
       - **Minor (`x.Y.0`)**: New user-facing capabilities, new routes/screens, or substantial backward-compatible additions.
       - **Major (`X.0.0`)**: Foundational architectural shifts, major overhauls, or breaking changes.
     - Mention the bump naturally in your wrap-up summary (e.g. *"Reconciled documentation suite and bumped project version to `v2.4.0`"*).
6. **Source-of-Truth Hierarchy**:
   `Canonical Tech Spec / Architecture` $\rightarrow$ `Active ADRs` $\rightarrow$ `Roadmap & Issues` $\rightarrow$ `Live Code when docs drift`.
   If documentation and code conflict, flag the drift and align docs to implemented reality.

---

## 🗑️ RULE 4: Zero Dead-Weight Policy
1. **Immediate Pruning**: When refactoring or replacing code, immediately delete replaced files, orphaned components, dead functions, unused hooks, and unimported dependencies (`package.json`, `requirements.txt`, etc.).
2. **Database Cleanliness**: When schemas change, drop obsolete tables, views, orphaned RPC functions, triggers, custom types, etc. Never leave zombie database artifacts.
3. **No Phantom Code or Notes**: Prune stale comments, commented-out dead code, deprecated TODOs, temporary workaround shims, unused mock data, etc.

---

## 🛡️ RULE 5: Pre-Flight Verification & Quality Gates
A change is incomplete until verified. Before concluding work, run the project's quality pipeline in order:
1. **Type Safety Gate**: Strict type checking (e.g. `tsc --noEmit`, `mypy`, engine analyzer, etc.) $\rightarrow$ 0 errors.
2. **Linting Gate**: Static analysis (e.g. `npm run lint`, `flake8`, `clippy`, etc.) $\rightarrow$ 0 errors/warnings.
3. **Test Suite Gate**: Unit, integration, and E2E suites $\rightarrow$ 100% pass rate.
4. **Build Gate**: Production build / export compilation $\rightarrow$ Clean exit code `0`.

---

## 🔧 RULE 6: Tooling, Links & Communication Discipline
1. **Prefer Native MCP Servers Over Custom Scripts**: If an active or configured MCP tool (e.g. Supabase, Context7, Firecrawl, Chrome DevTools, or any project-specific MCP server, etc.) covers the required functionality, use it directly instead of creating disposable one-off scripts.
2. **Clickable Links**: Link modified files and code symbols using `file:///` URLs (e.g. [`src/lib/auth.ts`](file:///absolute/path/to/file#L10-L25), etc.).
3. **Communication Posture**: High-density, concise, and implementation-specific. Skip introductory lecturing, conversational fluff, and redundant apologies.

---

## 🚀 RULE 7: Pre-Production Agility vs. Production Stability
- **During Active Pre-Production Development:** Implement clean architectural fixes and schema migrations directly. Do NOT write complex application-layer shims, redundant query loops, or backward-compatibility polyfills to support obsolete prototypes, old test rows, past schemas, legacy URL params, etc.
- **Production Mode:** Enforce strict backward compatibility and migration safeguards only when live production users or external integrations exist.
