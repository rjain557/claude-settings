---
name: gsd:sdlc-review
description: Run comprehensive multi-agent code review pipeline (Phase G Code Debugger)
argument-hint: "[--layer=frontend|backend|database|auth]"
allowed-tools:
  - Read
  - Write
  - Bash
  - Grep
  - Glob
  - Task
---

<objective>
Run the Phase G comprehensive code review pipeline. Spawns parallel review agents for each code layer, builds traceability matrix, and generates developer handoff with prioritized findings.

Orchestrator role: Parse options, spawn sdlc-code-reviewer agent, present findings summary.
</objective>

<execution_context>
@docs/sdlc/phase.g.codedebugger/code-debugger.md
@.planning/STATE.md
</execution_context>

<context>
Options: $ARGUMENTS
- (no flags): Full review — all layers + traceability matrix + SDLC gap analysis
- --layer=frontend: Frontend layer only
- --layer=backend: Backend layer only
- --layer=database: Database layer only
- --layer=auth: Auth/SSO layer only
</context>

<process>

## 1. Parse Options

Determine review scope from $ARGUMENTS:
- Default: full review (all layers + cross-layer analysis)
- --layer=X: single layer review only

## 2. Spawn sdlc-code-reviewer Agent

Spawn via Task tool:
- description: "SDLC Code Review ({scope})"
- prompt: Include scope and reference to SDLC code debugger docs

The agent will:
1. Inventory the repository (Phase 0)
2. Spawn layer reviewers — 4 in parallel for full, or 1 for single-layer (Wave 1)
3. Spawn cross-layer agents — traceability + SDLC gaps (Wave 2, full only)
4. Spawn MCP reviewer if detected (Wave 3, conditional)
5. Run build verification (MANDATORY)
6. Consolidate findings into reports

Output locations:
- docs/review/EXECUTIVE-SUMMARY.md
- docs/review/FULL-REPORT.md
- docs/review/DEVELOPER-HANDOFF.md
- docs/review/PRIORITIZED-TASKS.md

## 3. Present Results

Display executive summary:
> **Code Review Complete** — Overall Health: {score}
>
> Findings: {blocker} Blocker | {high} High | {medium} Medium | {low} Low
>
> **Top 5 Risks:**
> 1. {risk description}
> ...

Offer next steps:
- "View full report at docs/review/FULL-REPORT.md"
- "View developer handoff at docs/review/DEVELOPER-HANDOFF.md"
- "Run `/gsd:sdlc-validate` to check contract consistency"

</process>
