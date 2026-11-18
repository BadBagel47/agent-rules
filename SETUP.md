# SETUP AND ADAPTATION

Part of the global agent rules (AGENTS.md). Read when AGENTS.md says so: first session in a repo, missing inventory, a new rules version, conflicts with project rules, or when automatic merge has to be set up.

## 1. The project's files
- Do not copy the rules into the project repo. The project's AGENTS.md starts with a reference to the global rules (with the fallback via GitHub), states where HANDOFF.md and the backlog are, and is followed by the project rules. Create it if missing. Project information (current state, decisions etc.) goes in HANDOFF.md.
- HANDOFF.md and BACKLOG.md may live in the repo root or in docs/. Separate bug and feature lists (e.g. BUGS.md and FEATURES.md) linked from HANDOFF.md or the project's AGENTS.md count as the backlog and are not merged.
- An existing AGENTS.md with its own rules is kept: add the reference at the top and remove only what duplicates or conflicts with the global rules. Project rules that are more specific are kept. Existing project rules in HANDOFF.md may stay there if the project's AGENTS.md links to them.
- Do not create agent-specific rule files (e.g. CLAUDE.md, GEMINI.md). If they exist with their own rules: move what should be kept to the project's AGENTS.md (rules) or HANDOFF.md (information). Files that only refer to or import AGENTS.md (e.g. a CLAUDE.md containing only @AGENTS.md) are fine and are not raised. Tool settings files (e.g. .claude/settings.json, .gemini/settings.json) are not rule files and are left alone.
- Other existing documents (specifications, plans, logs, changelogs, investigations, ADRs) are kept and linked from a documentation map in HANDOFF.md or the project's AGENTS.md. Only content that duplicates HANDOFF.md or the backlog is moved. Goals and way of working may stay in their own linked documents.
- Decisions found in documents not linked from HANDOFF.md or the project's AGENTS.md are copied into "Decisions" in HANDOFF.md without asking, since that changes nothing.
- Record the project language in HANDOFF.md: for an existing project, the language of the existing product text. Translating an existing README is only done if the user approves it in the adaptation plan.

## 2. Inventory
- If HANDOFF.md is missing or lacks the line "Inventory: YYYY-MM-DD": do a thorough inventory automatically. An equivalent existing note counts and is rewritten to that format without a new inventory.
- First make sure every remote branch is visible (e.g. compare with `git ls-remote --heads` and fetch all branches if the checkout fetched only one).
- Go through: all branches, open pull requests and Issues, existing documentation (bug lists, TODO, handoff, whatever the file name or language, not only on main), and how the repo is published (branch, Action or external service).
- Check branches other than main and the git history for sensitive information (e.g. data removed from main but left on old branches) and flag it. Do a brief review of laws and regulations; findings go into the backlog.
- Branches with work never merged into main: first check whether the content already exists in main (e.g. squash-merged), using enough history, not a shallow clone. Group similar branches. They go into the adaptation plan (merge, keep or delete).
- Record "Inventory: YYYY-MM-DD" and the publishing method in HANDOFF.md. After that, read selectively.

## 3. New rules version
- HANDOFF.md states which rules version the repo was last adapted to. If the rules are newer: report briefly what changed (CHANGELOG.md), adapt the repo and update the version.
- What the rules require and that does not delete, overwrite or depend on anything in an adaptation plan is done directly. Everything else waits for the plan.
- For a new major version (X): change nothing until the user has approved an adaptation plan.
- Web basics (WEB.md) change the product and are never applied without the user's go-ahead.

## 4. Adaptation plan
- Used for conflicts with project rules, a new major version and everything in setup that needs approval: ID conversion, unmerged branches, moving found documentation (with a mapping between old and new IDs), translating an existing README, web basics.
- Numbered categories (1, 2, 3 …) with numbered items (1.1, 1.2 …), so the plan is not confused with run groups. In the chat, call them "punkt 1.1" so they are not confused with version numbers.
- Mark every item that deletes or overwrites something with ⚠️ and explain the mark once below the plan.
- Project rules that conflict with the global rules are shown with both rules and a recommendation. Approving the item means the recommendation applies; otherwise the user's choice. The choice is recorded as a decision, and the rule text is written in the project's AGENTS.md.
- A different existing ID system: state scope and consequences of converting (number of items, old IDs left in commits and documents). If the existing system works, recommend keeping it. Change nothing without approval. (New series are never written with #, since GitHub links #123 to issues.)
- Items related to backlog items state their IDs; approved items mark them as done where applicable.
- The user approves all, a category or single items: "Kör anpassning", "Kör 1 och 2", "Kör allt utom 3", "Kör 4, stoppa 4.2", "Kör 2.1" (the recommendation) or "2.1 projektregel".
- Items not run are saved in HANDOFF.md under "Pending adaptation" and shown again next session. An item the user has parked is mentioned in one line and not raised again until the user asks.
- Example:
  - **1 – Regelfiler**
    - 1.1 ⚠️ Lägg hänvisningen överst i AGENTS.md och ta bort regler som dubblerar agentreglerna; övriga projektregler behålls
    - 1.2 Lägg till prioritet, klar-sektion och körförslag i BACKLOG.md
  - **2 – Projektregler som krockar med de övergripande agentreglerna**
    - 2.1 Lösta buggar – projektregel: raderas; agentregel: flyttas till klar-sektion. Rekommendation: agentregeln (historiken bevaras)

## 5. Automatic merge to main
- Needed when the agent can only push to its own branch. Not used when the project rules require the user's approval before main (then open a pull request and give the user a direct link) or when the project uses test builds. A pull request the agent may merge itself does not count as such a requirement.
- The repo gets the GitHub Action .github/workflows/auto-merge.yml from templates/auto-merge.yml in agent-rules. It merges the agent's claude/ branches into main, triggers a GitHub Pages build if the repo uses Pages, and skips commits marked [wip]. Do not write your own variant and do not change the branch pattern. A repo may extend the template with checks that must pass before the merge (e.g. tests), as long as the branch pattern and the [wip] skip remain; such extensions are kept. Otherwise, if the repo's file lacks something the template has: update it.
- If the agent is refused (agents often may not create workflow files): give the user ready-made steps with the file name and the file content in separate code blocks, so it can be added once via github.com.
- After pushing, check that the Action run succeeded, or say in the report that it needs checking.

## 6. Renamed repo
- Record the old name in the repo's HANDOFF.md ("tidigare X") so agents treat it as an alias, and update references in the current documents (HANDOFF.md, backlog) of repos that refer to it. Old commits and logs keep the old name.
