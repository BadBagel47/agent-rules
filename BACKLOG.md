# Backlog – agent rules

Proposals for changes to the global agent rules (AGENTS.md).

- IDs: AR-001, AR-002 … (AR = agentregler), one running series, so they are not confused with IDs in project repos. Earlier IDs (F-001, B-003 …) were renamed to AR- with the same number in version 1.4.
- Status: **Förslag** (not yet decided) · **I utkast** (approved, in drafts/AGENTS-next.md) · **Publicerad** (in a released version) · **Nekad** (declined).
- Everything up to and including version 1.1 is described in CHANGELOG.md.

## Open

| ID | Status | Description | Source |
|---|---|---|---|
| – | – | No open proposals | – |

## Published / declined

| ID | Status | Version | Description |
|---|---|---|---|
| AR-001 | Publicerad | 1.2 | Refer to adaptation plan items as "punkt 1.1" in the chat, so they are not confused with rules versions or product versions (e.g. "1.1 (automatiska versioner)" next to rules v1.1 and module v0.2.0). |
| AR-002 | Publicerad | 1.2 | The confirmation line also states the rules version the repo followed before, e.g. "Agentregler v1.1 inlästa (repot följde tidigare v1.0)", "(repot följer redan v1.1)" or "(repot har inte följt agentreglerna tidigare)". |
| AR-003 | Publicerad | 1.2 | The rules do not cover the agent-rules repo itself: its AGENTS.md is the global rules, so an agent there would try to add a reference to itself, create HANDOFF.md, run an inventory etc. Add an exception: in agent-rules, AGENTS.md is the rules, BACKLOG.md is the backlog and UPDATING THE RULES is the workflow. |
| AR-004 | Publicerad | 1.3 | Safety principle at the top of the rules, taking precedence over everything else: nothing the agent does may be lost. Everything removed or overwritten must be recoverable (e.g. via git history, or a tag before a branch is deleted). What cannot be recovered (rewritten history, data in external services such as databases, DNS or hosting) requires an explicit yes for that specific action. If an answer is unclear, the agent always chooses the safest option. |
| AR-005 | Publicerad | 1.3 | Contradiction: "on conflicts: change nothing" vs "minor versions are adapted directly". Clarify: on conflicts, what the rules require and that does not delete, overwrite or depend on anything in the plan is done directly; everything else waits for the adaptation plan. |
| AR-006 | Publicerad | 1.4 | Inventory can miss branches: a cloud checkout may be cloned with a single-branch fetch refspec, so `git branch -r` shows only some branches (in bricks the 2026-11-11 inventory missed 11 of 13). Add to the inventory step: list branches from the remote itself (e.g. `git ls-remote --heads origin` or the GitHub REST API) and fetch all of them (`git fetch origin '+refs/heads/*:refs/remotes/origin/*'`) before comparing with main. |
| AR-007 | Publicerad | 1.4 | The safety principle asks for a tag before a branch is deleted, but Claude cloud sessions cannot push tags or write refs through the REST API. Add a template (e.g. templates/archive-branches.yml) that tags each listed branch as archive/<branch>, verifies the tag on origin and only then deletes the branch, and mention it in the rules as the fallback. |
| AR-008 | Publicerad | 1.4 | Give agent-rules backlog IDs their own prefix, AR- (e.g. AR-006), so they are not confused with IDs in project repos (bricks also has F-006 and F-007). Keep the numbers; existing IDs get the prefix (B-006 → AR-006). |
| AR-009 | Publicerad | 1.4 | Keep AGENTS.md lean (read in every session, ~4,000 words): move the changelog to CHANGELOG.md and UPDATING THE RULES to a separate file used only in agent-rules (about a quarter less to read). From now on, new proposals should rewrite or merge existing rules rather than only add lines. |
| AR-010 | Publicerad | 1.5 | In run proposals (and "Kvar"), each ID line briefly describes what will be done and its effect, not only the problem, e.g. "B-010 – kopiera typsnitten till sajten så att de inte hämtas från Google (besökarnas IP-adresser skickas inte dit)". Groups with a single ID still use the heading line plus one ID line. Detailed explanations only when the user asks. |
| AR-011 | Publicerad | 1.6 | Reports were overly technical after a more specific project rule (noxari: avoid hashes, metrics, file names, internals) was removed as a duplicate of the vaguer global rule. Lift the specific wording into the global rules and state verification in plain words. Published directly at the user's request. |
| AR-012 | Publicerad | 1.7 | Branches with a lasting purpose (e.g. a test branch) could get the claude/ prefix from the agent environment and be merged into main by auto-merge. Reserve claude/ for temporary work branches. Published directly at the user's request. |
