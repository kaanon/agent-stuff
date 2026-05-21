# Prompt: Populate memory files from current codebase

Paste this into Cursor to have it update the memory system.

---

## Prompt

You are updating the project's memory system in `memory/`. Read `memory/AGENT.md` first for the protocol — especially the three-tier technical context model.

### Step 1: Audit current state

Read the following to understand what exists now:

- `docs/brief.md` — product brief
- `docs/framework.md` — architecture handbook
- `docs/deprecated-ui-features.md` — deprecated features
- `docs/stub-inventory.md` — API route completion status
- `docs/operations-and-storage-diagrams.md` — mermaid diagrams
- `CODEBASE.md` — codebase shape overview
- `MEETINGS_PLAN.md` — meetings feature engineering plan
- `plan-cursor-consolidation.md` — consolidation plan

Also scan the actual codebase to verify what's true *right now*:

- `git log --oneline -20` for recent work
- `ls src/core/operations/` for current operations
- `ls src/server/routes/` for current routes
- `ls src/client/src/views/` for current views
- `ls electron/src/` for Electron structure
- Check `src/server/db/schema.ts` for current tables

### Step 2: Update memory files

Do NOT copy docs wholesale. Condense to what an agent needs. Link to `docs/` for depth.

**`memory/brief.md`** — Update with:
- What Fetch is (one paragraph)
- Who it's for
- Why it exists (if you can infer from docs or ask the user)
- Core constraints (from framework.md §1 and plan-cursor-consolidation.md §2)
- Feature surface (condensed — feature names + which views/routes, not full descriptions)
- Set `last-updated` in frontmatter to today

**`memory/technical-summary.md`** — Rewrite to reflect current state. This is tier 1: quick orientation.
- Architecture in ~5 bullet points (layers, what each does)
- Key patterns in ~5 bullet points (operations, styling, auth)
- Electron/meetings in 2–3 bullets
- Deprecated surfaces in 1–2 bullets
- **Must stay under 50 lines.** No decisions log, no rationale — just "what is true right now."
- Set `last-updated` in frontmatter to today

**`memory/technical-details.md`** — Update as tier 2: decisions with rationale.
- One `##` entry per major architectural decision. Include: decision, alternatives considered, why.
- Pull from: `docs/framework.md` (hexagonal core, operation pattern, composition root), `docs/deprecated-ui-features.md` (what was deprecated and why), `MEETINGS_PLAN.md` (dual-surface transcription choice).
- Include the storage port/adapter table (port → adapter → notes).
- For diagrams and code patterns, DON'T reproduce them — write "See `docs/framework.md` §N" with a one-line summary.
- Verify decisions against the actual code. If docs contradict code, trust code and flag with `<!-- VERIFY -->`.
- **Must stay under 200 lines.**
- Set `last-updated` in frontmatter to today

**`memory/progress.md`** — Update with:
- One `##` section per active initiative
- For each: what's done, what's remaining, any blockers
- Pull status from: `docs/stub-inventory.md` (routes done vs deferred), `MEETINGS_PLAN.md` (meetings progress), recent git log
- Remove anything clearly finished — move to `done.md`
- Set `last-updated` in frontmatter to today

**`memory/done.md`** — Update with:
- Any initiatives that are clearly shipped
- Reverse chronological, one `##` per initiative
- Include: what was done, approximate date (from git log), one-line outcome
- Set `last-updated` in frontmatter to today

### Rules

- `technical-summary.md` under 50 lines. `technical-details.md` under 200 lines. Other files under 200 lines.
- Use links like `See [docs/framework.md](../docs/framework.md)` for detail
- Write for a developer (or agent) picking up the project cold
- If something is unclear or contradictory, flag it with `<!-- VERIFY: ... -->` rather than guessing
- Do not delete or modify anything in `docs/` — those are the source of truth for deep reference
