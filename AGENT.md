# Agent Memory Protocol

This file defines how AI agents (Cursor, Claude Code, Copilot, etc.) should use the project memory system.

## Memory files

| File | Purpose | Update frequency |
|------|---------|-----------------|
| `memory/brief.md` | Project identity — what, why, for whom, constraints | Rarely. Only when the project's mission changes. |
| `memory/technical-summary.md` | Quick-glance architecture orientation (~40 lines) | After any major feature ships or architecture changes. |
| `memory/technical-details.md` | Mid-depth decisions, patterns, port/adapter tables | After significant technical decisions. Links to `docs/` for full depth. |
| `memory/progress.md` | Active work, current focus, blockers, next steps | Every session that moves work forward. |
| `memory/done.md` | Completed initiatives, shipped features, lessons learned | When an initiative is finished. |

## Three tiers of technical context

1. **Small** — `technical-summary.md`: Read this first. Enough to orient in 30 seconds. Keep under 50 lines.
2. **Medium** — `technical-details.md`: Architectural decisions with rationale, storage port tables, dependency rules. Keep under 200 lines. Links to `docs/` for diagrams and code patterns.
3. **Large** — The actual codebase and `docs/` folder: Full mermaid diagrams, code examples, framework handbook. Read on demand when you need implementation-level detail.

## When to read memory

- **Start of every session**: read `brief.md`, `technical-summary.md`, and `progress.md` to orient yourself.
- **Before architectural decisions**: read `technical-details.md` to avoid re-litigating settled decisions.
- **When implementing**: if `technical-details.md` isn't enough, follow its links into `docs/` or read the code directly.
- **Before proposing new work**: skim `done.md` to avoid duplicating past efforts.

## When to write memory

- **`progress.md`**: Update at the end of a session if meaningful work was done. Replace stale entries — this file reflects *current* state, not history.
- **`technical-summary.md`**: Update after a major feature ships or the architecture changes meaningfully. This is a snapshot, not a log — rewrite it to reflect current state.
- **`technical-details.md`**: Append when a non-obvious architectural decision is made. Include the decision, the alternatives considered, and why this one was chosen. Prune entries that are no longer relevant.
- **`done.md`**: Move an entry from `progress.md` to `done.md` when an initiative ships. Include: what was done, the date, and one sentence on outcome or lesson.
- **`brief.md`**: Only update if the user explicitly redefines the project's scope, audience, or core constraints.

## How to write

- Use plain markdown. No HTML, no embedded code blocks longer than 5 lines.
- Each entry in `technical-details.md` and `done.md` should be a `##` section with a date.
- `technical-summary.md` is a snapshot, not a log — rewrite the whole file to reflect current state.
- `progress.md` uses a flat structure: `##` per active initiative, bullet points for status.
- `technical-summary.md` must stay under 50 lines. `technical-details.md` under 200 lines.
- If `technical-details.md` exceeds 200 lines, move older/less-relevant decisions into `docs/` and link to them.
- Never delete content from `done.md` — it is append-only.
- When updating `progress.md`, remove or archive items that are no longer active.

## Tone

Write for a developer picking up the project cold. No jargon without context. Decisions should include *why*, not just *what*.
