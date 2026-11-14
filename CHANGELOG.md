# Changelog – global agent rules

- 1.7 (2026-11-14): The prefix claude/ is only for temporary work branches; branches with a lasting purpose (test, preview, release) must never use it, so they are not merged automatically (AR-012).
- 1.6 (2026-11-13): Reports avoid technical details the user does not need (hashes, metrics, file names, internals) and state verification in plain words (AR-011).
- 1.5 (2026-11-13): Run proposals: each ID line says what will be done and what it gives, not only the problem; also for single-ID groups (AR-010).
- 1.4 (2026-11-12): Inventory first makes sure every remote branch is visible (AR-006). Template templates/archive-branches.yml for tagging branches before deletion when the agent cannot create tags (AR-007). Proposals to the rules get the ID prefix AR- (AR-008). Changelog moved to CHANGELOG.md and the rule-maintenance workflow to MAINTAINING.md, so AGENTS.md is shorter (AR-009).
- 1.3 (2026-11-12): Safety principle at the top: nothing may be lost, irreversible actions need an explicit yes, unclear answers mean the safest option (AR-004). On conflicts, safe and independent changes required by the rules are done directly; the rest waits for the adaptation plan (AR-005).
- 1.2 (2026-11-12): Exception for the agent-rules repo itself (AR-003); the confirmation line also states the version the repo followed before (AR-002); adaptation plan items are referred to as "punkt 1.1" in the chat (AR-001).
- 1.1 (2026-11-12):
  - Terms: global agent rules and project rules. Project rules live in the project's AGENTS.md below the reference (existing ones in HANDOFF.md may stay if linked); more specific project rules are kept; changes to them need approval.
  - Adaptation plan with numbered items that can be approved or stopped individually; conflicting project rules shown with a recommendation; recorded decisions are not raised again.
  - Inventory: fixed "Inventory" line, all branches (with enough history), PRs, Issues, publishing method, sensitive information and laws and regulations.
  - Documentation: HANDOFF.md is current state (short log allowed) with a Decisions section; other documents, decision documents and separate bug/feature lists may be linked; HANDOFF.md and the backlog in root or docs/.
  - Run groups: letters always from A for the latest list; parked items excluded from broad go-aheads; already done items reported separately; neutral model levels in saved documents.
  - Publishing: changes published and verified after a run by default; optional test builds approved with "Publicera"; no automatic merge where review is required.
  - Language: working documents accept Swedish and English without translation; existing product language is the project language.
  - New: one-time actions to remove recurring manual steps; laws and regulations (Sweden and EU); check tools and permissions at start; never claim more than verified; IDs in chat with a short explanation.
  - Rule changes go through a draft and a backlog (BACKLOG.md) and are published only on the user's explicit request; major versions only when existing content must be changed.
- 1.0 (2026-11-11): First version.
