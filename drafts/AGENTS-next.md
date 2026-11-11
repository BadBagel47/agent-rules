> **DRAFT – NOT IN EFFECT.** The rules in effect are in [AGENTS.md](../AGENTS.md).

# AGENT RULES, version 1.0 (2026-11-11)

Global agent rules for all AI agents working in the user's GitHub repositories.

- **Global agent rules** (Swedish: *övergripande agentregler*): this file. Applies to all repos.
- **Project rules** (Swedish: *projektregler*): rules that apply to one repo only. They live in that repo's HANDOFF.md.

## ON START
- This is the original: https://raw.githubusercontent.com/BadBagel47/agent-rules/main/AGENTS.md. Read it at the start of every session. If the link cannot be read: fetch AGENTS.md from the repo BadBagel47/agent-rules via GitHub instead. If neither works: say so immediately.
- Confirm in the first reply of every session with one short line which rules version was loaded, e.g. "Agentregler v1.1 inlästa".
- Do not copy these rules into the project repo. The project's AGENTS.md only contains a reference to this file and states where HANDOFF.md and BACKLOG.md are. Create it if missing. Project rules and project information go in HANDOFF.md.
- Do not create agent-specific rule files (e.g. CLAUDE.md, GEMINI.md). If such files already exist, or an AGENTS.md with its own rules: compare with the global agent rules. Content to keep is moved to HANDOFF.md as project rules or project information. Files that only refer to or import AGENTS.md (e.g. a CLAUDE.md containing only @AGENTS.md) are allowed and are not raised.
- On conflicts: change nothing. Instead present a complete adaptation plan (see below) with all changes, including those the rules already require.
- Decisions recorded in the "Decisions" section of HANDOFF.md (e.g. approved project rules that deviate from the global agent rules, intentionally kept branches, chosen protection for sensitive information) are respected and not raised again. Record new decisions by the user there. Decisions found elsewhere in the project documentation are copied into that section without asking, since this changes nothing.
- HANDOFF.md and BACKLOG.md may live in the repo root or in docs/.
- "main" in these rules means the repo's default branch, even if it has another name (e.g. master).
- Sync with the latest main before starting work and before assigning new IDs.
- Always read HANDOFF.md at the start of every session.
- Check which tools, permissions and access the environment has (e.g. push to main, creating workflow files, GitHub API) instead of assuming. Note limitations in HANDOFF.md with the date.
- If HANDOFF.md is missing, or lacks the line "Inventory: YYYY-MM-DD" (or an equivalent existing note, which is then rewritten to that format without a new inventory): automatically do a thorough inventory of the repo (all branches, open PRs and Issues, existing documentation, how the repo is published, e.g. branch, Action or external service). Record the line "Inventory: YYYY-MM-DD" and the publishing method in HANDOFF.md. After that, selective reading applies.
- Before creating documentation: search for existing documentation (e.g. bug lists, TODO, handoff, regardless of file name or language) on all branches, open PRs and Issues, not just main. If found: include moving content that duplicates HANDOFF.md or BACKLOG.md into the new structure, with a mapping between old and new IDs, in the adaptation plan.
- Include branches with work that was never merged into main in the adaptation plan (merge, keep or delete). First check whether the branch content already exists in main (e.g. squash-merged). Group similar branches into one plan item.
- HANDOFF.md states which rules version the repo was last adapted to. If this version is newer: briefly report what changed (see the changelog), adapt the repo and update the version in HANDOFF.md. For a new major version (X): change nothing until the user has approved an adaptation plan.

## ADAPTATION PLAN
- Used on conflicts, for a new major version, and for anything during setup that needs approval (e.g. ID conversion, unmerged branches, moving found documentation, translating an existing README).
- Changes are grouped into numbered categories (1, 2, 3 …) with numbered items (1.1, 1.2 …). Numbers, not letters, so the plan is not confused with run groups.
- Project rules that conflict with the global agent rules are shown with both rules and a recommendation. Approving the item means the recommendation applies; otherwise the user's choice applies. The choice is recorded as a decision in HANDOFF.md, and an approved project rule then takes precedence over the global agent rule in that repo.
- Items related to backlog items state their IDs, and approved items mark those IDs as done where applicable.
- Mark every item that deletes or overwrites something with ⚠️ and explain the marking once below the plan.
- The user may approve all, a category or single items, e.g. "Kör anpassning", "Kör 1 och 2", "Kör allt utom 3", "Kör 4, stoppa 4.2".
- Items not run remain as a plan, are saved in HANDOFF.md under "Pending adaptation" and are shown again in the next session.
- Example (written in Swedish in the chat):
  - **1 – Regelfiler**
    - 1.1 ⚠️ Ersätt AGENTS.md (egna regler) med en hänvisning; reglerna flyttas till HANDOFF.md som projektregler
    - 1.2 Lägg till prioritet, klar-sektion och körförslag i BACKLOG.md
  - **2 – Projektregler som krockar med de övergripande agentreglerna**
    - 2.1 Lösta buggar – projektregel: raderas; agentregel: flyttas till klar-sektion. Rekommendation: agentregeln (historiken bevaras)
  - The user replies e.g. "Kör 2.1" (recommendation) or "2.1 projektregel".

## UPDATING THE RULES
- An agent may propose changes to these rules. Changes the user has approved are first collected in the draft drafts/AGENTS-next.md, never directly in AGENTS.md. The draft is never in effect.
- The draft is a full copy of AGENTS.md with the changes applied, marked as a draft at the top, with the changes listed under "Unreleased" in the changelog. If the draft is missing: create it from the current AGENTS.md.
- The original lives in the public repo BadBagel47/agent-rules. If the agent lacks write access: ask the user to grant access (e.g. add the repo to the session) and give ready-made steps for it.
- Publish only when the user explicitly says so (e.g. "Publicera reglerna"). Then:
  1. Save the current AGENTS.md unchanged as versions/AGENTS-vX.Y.md.
  2. Copy the draft to AGENTS.md, remove the draft marking and set the new version number and today's date:
     - X (major) when existing content in repos must be changed, moved or removed, e.g. new file structure or new ID system.
     - Y (minor) for clarifications and additions, including new sections or notes that are only added.
  3. Replace "Unreleased" with a changelog line: version, date and a short description of what changed.
  4. Delete the draft.
- The rules are written in English. The user may describe the change in Swedish.
- Commit and push to main per the normal rules and report the new version.

## DOCUMENTATION
- Keep up to date: HANDOFF.md (current state, next steps, rules version, project language, publishing method, decisions, and goals and way of working as their own sections or as links to separate documents) and features and bugs (BACKLOG.md).
- Other existing documents (e.g. specifications, plans, logs, changelogs, investigations, ADRs) are kept and linked from a documentation map in HANDOFF.md. Only content that duplicates HANDOFF.md or BACKLOG.md is moved.
- HANDOFF.md describes the current state briefly and must not grow into a log. History belongs in git, changelogs or log documents.
- If work cannot be finished in the session: record in HANDOFF.md exactly where it stopped and how to continue, and push.
- Completed items are moved to a done section in BACKLOG.md, not deleted.
- Priority uses a fixed scale in the documentation: High, Medium, Low.
- Update documentation in the same commit as the change.
- Follow established technical standards and naming conventions.
- Everything must work regardless of which AI agent takes over.

## ID SYSTEM
- If no ID system exists: one shared running number series with prefixes: B-001 bug, F-002 feature, D-003 planning/design. (Not #, since GitHub links #123 to issues.)
- If a different ID system exists: include its conversion in the adaptation plan, stating scope and consequences (number of items, old IDs remaining in commits and documents). If the existing system works, recommend keeping it; the user decides. Change nothing without approval.
- Include the affected IDs in commit messages.

## WORKFLOW
1. New bugs, features, planning and design are documented and collected for a combined run. They are not fixed immediately.
2. For a reported bug, the agent should first try to locate it with simple tests before asking the user, e.g. reading code, running existing tests or reproducing the bug. The tests must not change code or data. Only ask about what cannot be found out independently.
3. Suggest priority and group items that can be run together with the same model and level. Always recommend model and level before a run. Only suggest models and levels available in the agent's own environment, which the user can select there, never models from other providers.
   - Each proposed run group gets a letter (A, B, C …). Format: a heading line with letter – model and level – short description, and below it one line per ID with a short explanation.
   - The letters refer to the latest proposal. Save it in BACKLOG.md under "Proposed runs" and replace it when a new proposal is made.
   - The user may reply e.g. "Kör A", "Kör A och C" or "Kör alla". Multiple groups are run in priority order; the order does not need to be mentioned in the report.
   - Incomplete items are included in the next proposal once the user has provided what was needed.
   - Commits and reports use item IDs, not the letters.
   - Example (written in Swedish in the chat):
     - **A** – Sonnet, medium – Poäng och tidtagning efter omstart
       - B-003 – Poängen nollställs inte
       - B-005 – Tidtagningen startar inte om
     - **B** – Opus, high – Flerspelarlobby
       - D-010 – Design av lobbyn
       - F-007 – Rumskoder för att bjuda in spelare
       - F-009 – Kö när rummet är fullt
4. Wait for a go-ahead ("Kör" or similar) before making code changes. A go-ahead covers the approved items until they are done; do not ask again for the same work. Ask again only if the scope changes. Documentation (the project's AGENTS.md, HANDOFF.md, BACKLOG.md) may be saved and pushed without a go-ahead.
5. Verify before pushing: run existing tests or the build and check that the site or app starts without errors.
6. After a run: commit and push directly to main, unless the user has said otherwise. Do everything possible without manual steps from the user. If the environment does not allow pushing to main: merge via PR yourself if permitted. If that also fails: use automatic merge (see below). If the agent works on a branch other than main, the changes must reach main in the same run, not at a later time.
7. Force push, deleting files or rewriting history always requires approval.
8. Report all IDs with a short status. Never claim more than has been verified: distinguish between changed in code, tested, published and verified by the user. Incomplete items are listed separately with what is needed to continue. Run groups not yet run are listed under "Kvar" in the same format as the proposal. Link to the published site or the commit when available.

## AUTOMATIC MERGE TO MAIN
- If the agent can only push to its own branch, the repo must have a GitHub Action (.github/workflows/auto-merge.yml) that, on push to the agent's branches, automatically merges them into main and triggers a new GitHub Pages build if the repo uses Pages.
- The agent's own branches must always start with the prefix claude/, regardless of which agent is working, so they are merged automatically.
- Use the template templates/auto-merge.yml in BadBagel47/agent-rules. Do not write your own variant. Do not change the branch pattern.
- If missing: add it. If refused (agents often lack permission to create workflow files): give the user ready-made steps with the file name and file content in separate code blocks, so the file can be added manually via github.com once.
- After pushing, check that the Action run succeeded if possible. Otherwise: mention in the report that it needs checking. If the merge fails due to a conflict: resolve it in the same session if possible, otherwise report it clearly.

## COMMUNICATION
- Swedish in the chat.
- The user's working documents (HANDOFF.md and BACKLOG.md) accept both Swedish and English, also mixed. New entries keep the user's own wording and terms in the language the user used. Existing text is never translated.
- Project language (the product's own text that players and users see, and README) is English by default. If the user specifies another language for a project, follow it without objection. Record the project language in HANDOFF.md.
- Code, code comments, commits and issues are in English unless the user says otherwise.
- Never translate existing product text or README unless the user asks or approves it in the adaptation plan.
- Short replies, but never leave out important information. No unnecessary technical detail.
- No running commentary during work, unless something important needs the user's attention.
- When something unclear affects the result: ask rather than guess.
- When an ID is mentioned in the chat, always follow it with a short explanation, e.g. "B-012 (buzzern på iPad)". Never just the number.

## MANUAL STEPS FOR THE USER
- Give everything needed to complete the step, with direct links where possible.
- Text to be copied, pasted or searched for goes in its own code block (one per value) so it can be copied with a button.
- Other information needed for the step is clearly marked but not put in code blocks.
- When a manual step will recur, or stops the agent: suggest a one-time action that lets the agent handle the step itself in the future (e.g. a workflow file, a GitHub Secret, a permission, an integration or a network setting). State what is done once, what it saves and any risks. Suggest the least permission needed, and never ask the user to paste keys or passwords into the chat.
- Record in HANDOFF.md which one-time actions are done, pending or declined, so they are not suggested again needlessly.

## RESOURCES
- Conserve quota without sacrificing quality: read selectively instead of the whole repo and avoid unnecessary reruns. Speed is not a priority unless stated otherwise.

## SENSITIVE INFORMATION
- Personal data and other sensitive information is only published with explicit approval. The question must explain why it is needed, what it makes easier, and what the risks and consequences are.
- Secrets (API keys, tokens, passwords) are never committed. Use GitHub Secrets or equivalent and make sure .gitignore covers local secret files.
- Keys that are public by design (e.g. Firebase web config) may be in the code, but then access rules must protect the data.
- During inventory, also check branches other than main and the git history for sensitive information (e.g. data that was removed from main but remains on old branches) and flag it.
- Project-sensitive information: information that must not be easily accessible to the project's own users, e.g. solutions, answers, coordinates or unpublished content. Flag such information when it appears, including in existing code.
- Briefly describe how the information is exposed, e.g. in a public repo, in source code sent to the browser, in network requests or in git history (anything committed remains even if deleted later).
- Present the available protection options, with protection level, pros and cons and what is required of the user. Examples: obfuscation (only stops casual guessing), hashing (the answer is checked without being stored in plain text), encryption where the key is provided by the game itself, server-side checking (e.g. Cloudflare Worker) or a private repo.
- Let the user choose the protection before the information is committed.
- The agent-rules repo is public: never put sensitive information there.

## CHANGELOG
- Unreleased:
  - Removed redundant integration line; merged translation lines; shorter adaptation plan example.
  - Version rule: major only when existing content must be changed, moved or removed; additions are minor.
  - Suggest one-time actions that remove recurring manual steps (least permission, no secrets in chat); record done, pending and declined ones in HANDOFF.md.
  - Decisions collected in a "Decisions" section in HANDOFF.md (copied there from other documents without asking); goals and way of working may live in linked separate documents.
  - From project rules: check tools and permissions at start; HANDOFF.md is current state, not a log; record where unfinished work stopped; a go-ahead covers the approved items; never claim more than verified; IDs in chat always with a short explanation.
  - Terms: global agent rules (övergripande agentregler) and project rules (projektregler). Conflicting project rules are shown with both rules and a recommendation; an approved project rule takes precedence in its repo.
  - Inventory checks other branches and history for sensitive information.
  - Recorded user decisions are not raised again; files that only import AGENTS.md are allowed; HANDOFF.md and BACKLOG.md in root or docs/; other documents kept and linked from a documentation map; branches checked against main and grouped; ID conversion shows scope and may be declined.
  - Equivalent existing inventory notes count; adaptation plan items reference related IDs.
  - Adaptation plan with numbered categories and items that can be approved or stopped individually; ID conversion, unmerged branches and found documentation go into the plan.
  - Clarifications: project's AGENTS.md (not the rules) may be pushed without go-ahead; claude/ prefix for all agents; auto-merge conflicts resolved in the same session; fixed "Inventory: YYYY-MM-DD" line; goals and way of working as sections in HANDOFF.md.
  - New major version: adaptation only after the user approves an adaptation plan.
  - Conflicts: one complete adaptation plan approvable with one answer. Changes on other branches must reach main in the same run.
  - Language: HANDOFF.md and BACKLOG.md accept Swedish and English without translation; project language (product text and README) English by default but set per project by the user; code, comments and commits in English.
  - Rule changes are collected in a draft (drafts/AGENTS-next.md) and only published when the user explicitly says so.
- 1.0 (2026-11-11): First version.
