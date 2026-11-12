> **DRAFT – NOT IN EFFECT.** The changelog in effect is [CHANGELOG.md](../CHANGELOG.md) (not yet created; until then the changelog is at the end of AGENTS.md).

# Changelog – global agent rules

- Unreleased:
  - Changelog moved to CHANGELOG.md and the rule-maintenance workflow to MAINTAINING.md, so AGENTS.md is shorter to read in every session (F-009 → AR-009).
  - Proposals to the rules get their own ID prefix AR- (F-008 → AR-008).
  - Inventory first makes sure every remote branch is visible (B-006 → AR-006).
  - Template templates/archive-branches.yml for tagging branches before deletion when the agent cannot create tags (B-007 → AR-007).
- 1.3 (2026-11-12): Safety principle at the top: nothing may be lost, irreversible actions need an explicit yes, unclear answers mean the safest option (F-004). On conflicts, safe and independent changes required by the rules are done directly; the rest waits for the adaptation plan (B-005).
- 1.2 (2026-11-12): Exception for the agent-rules repo itself (B-003); the confirmation line also states the version the repo followed before (F-002); adaptation plan items are referred to as "punkt 1.1" in the chat (F-001).
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
