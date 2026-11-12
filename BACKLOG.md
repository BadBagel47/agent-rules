# Backlog – agent rules

Proposals for changes to the global agent rules (AGENTS.md).

- IDs: one shared running series. B = problem in the rules, F = new rule or improvement, D = planning/design.
- Status: **Förslag** (not yet decided) · **I utkast** (approved, in drafts/AGENTS-next.md) · **Publicerad** (in a released version) · **Nekad** (declined).
- Everything up to and including version 1.1 is described in the changelog in AGENTS.md. New proposals start at 001.

## Open

| ID | Status | Description | Source |
|---|---|---|---|
| B-006 | Förslag | Inventory can miss branches: a cloud checkout may be cloned with a single-branch fetch refspec, so `git branch -r` shows only some branches (in bricks the 2026-11-11 inventory missed 11 of 13). Add to the inventory step: list branches from the remote itself (e.g. `git ls-remote --heads origin` or the GitHub REST API) and fetch all of them (`git fetch origin '+refs/heads/*:refs/remotes/origin/*'`) before comparing with main. | bricks, 2026-11-12 |
| B-007 | Förslag | The safety principle asks for a tag before a branch is deleted, but Claude cloud sessions cannot push tags or write refs through the REST API. Add a template (e.g. templates/archive-branches.yml) that tags each listed branch as archive/<branch>, verifies the tag on origin and only then deletes the branch, and mention it in the rules as the fallback. | bricks, 2026-11-12 |

## Published / declined

| ID | Status | Version | Description |
|---|---|---|---|
| F-001 | Publicerad | 1.2 | Refer to adaptation plan items as "punkt 1.1" in the chat, so they are not confused with rules versions or product versions (e.g. "1.1 (automatiska versioner)" next to rules v1.1 and module v0.2.0). |
| F-002 | Publicerad | 1.2 | The confirmation line also states the rules version the repo followed before, e.g. "Agentregler v1.1 inlästa (repot följde tidigare v1.0)", "(repot följer redan v1.1)" or "(repot har inte följt agentreglerna tidigare)". |
| B-003 | Publicerad | 1.2 | The rules do not cover the agent-rules repo itself: its AGENTS.md is the global rules, so an agent there would try to add a reference to itself, create HANDOFF.md, run an inventory etc. Add an exception: in agent-rules, AGENTS.md is the rules, BACKLOG.md is the backlog and UPDATING THE RULES is the workflow. |
| F-004 | Publicerad | 1.3 | Safety principle at the top of the rules, taking precedence over everything else: nothing the agent does may be lost. Everything removed or overwritten must be recoverable (e.g. via git history, or a tag before a branch is deleted). What cannot be recovered (rewritten history, data in external services such as databases, DNS or hosting) requires an explicit yes for that specific action. If an answer is unclear, the agent always chooses the safest option. |
| B-005 | Publicerad | 1.3 | Contradiction: "on conflicts: change nothing" vs "minor versions are adapted directly". Clarify: on conflicts, what the rules require and that does not delete, overwrite or depend on anything in the plan is done directly; everything else waits for the adaptation plan. |
