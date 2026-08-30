# Agentic Build Graph

The build discipline installed in the Velents Agent workspace: operating rules, subagents, and skills that force grounded, verified, gated increment work.

## What's here

| Path | What it is |
|---|---|
| `CLAUDE.md` | The binding operating rules (§1–§12): Definition of Done, no false green, read-before-build, migrations, security-as-property, shared-infra rules, escalation. Drop into your workspace root. |
| `.claude/agents/` | `grounder` (read-only codebase mapper), `builder` (scoped increment executor), `reviewer` (principal-engineer review, never writes code). |
| `.claude/skills/` | `/increment` (the main loop: ground → plan → **gate** → build → verify → review → **gate** → report), `/verify`, `/status`, `/signal`, `/stage`. |
| `docs/build-graph/` | The specs and handbook: `Agentic_Build_Handbook.md`, `Agent_Graph_Spec.md`, `Product_Graph.md`, `PM_Agent_Graph_Spec.md` (the sibling PM graph), `feature-ledger.template.md`, `doctor.sh`. |

## Install

Copy `CLAUDE.md`, `.claude/`, and `docs/build-graph/` into your workspace root. Claude Code picks up the agents and skills automatically.

The workspace also expects four registers under `docs/` that the graph writes to — create them empty if they don't exist: `PROJECT_CONTEXT.md`, `BLOCKERS.md`, `COVERAGE.md`, `DECISIONS.md`, plus `RESUME.md` (the session-continuity note, §11).

## Invoke

- `/increment <task or Linear ID>` — one disciplined code-change increment. It **halts at the plan gate** for your approval before writing code, and again before anything consequential lands.
- `/verify <claim>` — prove a surface works: real request, negative case, downstream contract.
- `/status` — evidence-checked status report.
- `/signal` / `/stage` — route a product ask into the Product Graph / advance a feature ledger.

## The one rule that summarizes the rest

"Done" is real verified behaviour against a real system — a 200 with real data **and** the proven negative case (403, cross-tenant denial). Anything less is labelled UNVERIFIED, never rounded up.
