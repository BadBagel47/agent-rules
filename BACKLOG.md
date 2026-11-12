# Backlog – agent rules

Proposals for changes to the global agent rules (AGENTS.md).

- IDs: one shared running series. B = problem in the rules, F = new rule or improvement, D = planning/design.
- Status: **Förslag** (not yet decided) · **I utkast** (approved, in drafts/AGENTS-next.md) · **Publicerad** (in a released version) · **Nekad** (declined).
- Everything up to and including version 1.1 is described in the changelog in AGENTS.md. New proposals start at 001.

## Open

| ID | Status | Description | Source |
|---|---|---|---|
| F-001 | Förslag | Refer to adaptation plan items as "punkt 1.1" in the chat, so they are not confused with rules versions or product versions (e.g. "1.1 (automatiska versioner)" next to rules v1.1 and module v0.2.0). | geo-kit report, 2026-11-12 |
| F-002 | Förslag | The confirmation line also states the rules version the repo followed before, e.g. "Agentregler v1.1 inlästa (repot följde tidigare v1.0)", "(repot följer redan v1.1)" or "(repot har inte följt agentreglerna tidigare)". | User, 2026-11-12 |
| B-003 | Förslag | The rules do not cover the agent-rules repo itself: its AGENTS.md is the global rules, so an agent there would try to add a reference to itself, create HANDOFF.md, run an inventory etc. Add an exception: in agent-rules, AGENTS.md is the rules, BACKLOG.md is the backlog and UPDATING THE RULES is the workflow. | Self-check, 2026-11-12 |

## Published / declined

| ID | Status | Version | Description |
|---|---|---|---|
