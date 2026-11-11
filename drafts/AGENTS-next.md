> **DRAFT – NOT IN EFFECT.** The rules in effect are in [AGENTS.md](../AGENTS.md).

# AGENT RULES, version 1.0 (2026-11-11)

Shared rules for all AI agents working in the user's GitHub repositories.

## ON START
- This is the original: https://raw.githubusercontent.com/BadBagel47/agent-rules/main/AGENTS.md. Read it at the start of every session. If the link cannot be read: fetch AGENTS.md from the repo BadBagel47/agent-rules via GitHub instead. If neither works: say so immediately.
- Confirm in the first reply of every session with one short line which rules version was loaded, e.g. "Regler v1.0 inlästa".
- Do not copy these rules into the project repo. The project's AGENTS.md only contains a reference to this file. Create it if missing. Project-specific rules and information go in HANDOFF.md.
- Do not create agent-specific rule files (e.g. CLAUDE.md, GEMINI.md). If such files already exist, or an AGENTS.md with its own rules: compare with these rules. Project-specific content to keep is moved to HANDOFF.md.
- On conflicts: change nothing. Instead present a complete adaptation plan (see below) with all changes, including those the rules already require.
- "main" in these rules means the repo's default branch, even if it has another name (e.g. master).
- Sync with the latest main before starting work and before assigning new IDs.
- Always read HANDOFF.md at the start of every session.
- If HANDOFF.md is missing, or lacks the line "Inventory: YYYY-MM-DD": automatically do a thorough inventory of the repo (all branches, open PRs and Issues, existing documentation, how the repo is published, e.g. branch, Action or external service). Record the line "Inventory: YYYY-MM-DD" and the publishing method in HANDOFF.md. After that, selective reading applies.
- Before creating documentation: search for existing documentation (e.g. bug lists, TODO, handoff, regardless of file name or language) on all branches, open PRs and Issues, not just main. If found: include moving the content into the new structure, with a mapping between old and new IDs, in the adaptation plan.
- Include branches with work that was never merged into main in the adaptation plan (merge or delete).
- HANDOFF.md states which rules version the repo was last adapted to. If this version is newer: briefly report what changed (see the changelog), adapt the repo and update the version in HANDOFF.md. For a new major version (X): change nothing until the user has approved an adaptation plan.

## ADAPTATION PLAN
- Used on conflicts, for a new major version, and for anything during setup that needs approval (e.g. ID conversion, unmerged branches, moving found documentation, translating an existing README).
- Changes are grouped into numbered categories (1, 2, 3 …) with numbered items (1.1, 1.2 …). Numbers, not letters, so the plan is not confused with run groups.
- Mark every item that deletes or overwrites something with ⚠️ and explain the marking once below the plan.
- The user may approve all, a category or single items, e.g. "Kör anpassning", "Kör 1 och 2", "Kör allt utom 3", "Kör 4, stoppa 4.2".
- Items not run remain as a plan, are saved in HANDOFF.md under "Pending adaptation" and are shown again in the next session.
- Example (written in Swedish in the chat):
  - **1 – Regelfiler**
    - 1.1 ⚠️ Ta bort CLAUDE.md och GEMINI.md (projektspecifikt innehåll flyttas först till HANDOFF.md)
    - 1.2 ⚠️ Ersätt AGENTS.md med en hänvisning till de gemensamma reglerna
  - **2 – Dokumentation**
    - 2.1 Lägg till prioritet, klar-sektion och körförslag i BACKLOG.md
  - **3 – Id-system**
    - 3.1 ⚠️ Numrera om #347-formatet till B/F/D, med kopplingslista

## UPDATING THE RULES
- An agent may propose changes to these rules. Changes the user has approved are first collected in the draft drafts/AGENTS-next.md, never directly in AGENTS.md. The draft is never in effect.
- The draft is a full copy of AGENTS.md with the changes applied, marked as a draft at the top, with the changes listed under "Unreleased" in the changelog. If the draft is missing: create it from the current AGENTS.md.
- The original lives in the public repo BadBagel47/agent-rules. If the agent lacks write access: ask the user to grant access (e.g. add the repo to the session) and give ready-made steps for it.
- Publish only when the user explicitly says so (e.g. "Publicera reglerna"). Then:
  1. Save the current AGENTS.md unchanged as versions/AGENTS-vX.Y.md.
  2. Copy the draft to AGENTS.md, remove the draft marking and set the new version number and today's date:
     - X (major) when the change requires existing repos to be adapted, e.g. new file structure or new ID system.
     - Y (minor) for clarifications and additions that require no adaptation.
  3. Replace "Unreleased" with a changelog line: version, date and a short description of what changed.
  4. Delete the draft.
- The rules are written in English. The user may describe the change in Swedish.
- Commit and push to main per the normal rules and report the new version.

## DOCUMENTATION
- Keep up to date: HANDOFF.md (current state, next steps, rules version, project language, publishing method, and goals and way of working as their own sections) and features and bugs (docs/BACKLOG.md).
- Completed items are moved to a done section in BACKLOG.md, not deleted.
- Priority uses a fixed scale in the documentation: High, Medium, Low.
- Update documentation in the same commit as the change.
- Follow established technical standards and naming conventions.
- Everything must work regardless of which AI agent takes over.

## ID SYSTEM
- If no ID system exists: one shared running number series with prefixes: B-001 bug, F-002 feature, D-003 planning/design. (Not #, since GitHub links #123 to issues.)
- If a different ID system exists: include its conversion in the adaptation plan. Change nothing without approval.
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
4. Wait for a go-ahead ("Kör" or similar) before making code changes. Documentation (the project's AGENTS.md, HANDOFF.md, BACKLOG.md) may be saved and pushed without a go-ahead.
5. Verify before pushing: run existing tests or the build and check that the site or app starts without errors.
6. After a run: commit and push directly to main, unless the user has said otherwise. Do everything possible without manual steps from the user. If the environment does not allow pushing to main: merge via PR yourself if permitted. If that also fails: use automatic merge (see below). If the agent works on a branch other than main, the changes must reach main in the same run, not at a later time.
7. Force push, deleting files or rewriting history always requires approval.
8. Report all IDs with a short status. Incomplete items are listed separately with what is needed to continue. Run groups not yet run are listed under "Kvar" in the same format as the proposal. Link to the published site or the commit when available.

## AUTOMATIC MERGE TO MAIN
- If the agent can only push to its own branch, the repo must have a GitHub Action (.github/workflows/auto-merge.yml) that, on push to the agent's branches, automatically merges them into main and triggers a new GitHub Pages build if the repo uses Pages.
- The agent's own branches must always start with the prefix claude/, regardless of which agent is working, so they are merged automatically.
- Use the template templates/auto-merge.yml in BadBagel47/agent-rules. Do not write your own variant. Do not change the branch pattern.
- If missing: add it. If refused (agents often lack permission to create workflow files): give the user ready-made steps with the file name and file content in separate code blocks, so the file can be added manually via github.com once.
- After pushing, check that the Action run succeeded if possible. Otherwise: mention in the report that it needs checking. If the merge fails due to a conflict: resolve it in the same session if possible, otherwise report it clearly.

## COMMUNICATION
- Swedish in the chat.
- The user's working documents (HANDOFF.md and docs/BACKLOG.md) accept both Swedish and English, also mixed. New entries keep the user's own wording and terms in the language the user used. Existing text is never translated.
- Project language (the product's own text that players and users see, and README) is English by default. If the user specifies another language for a project, follow it without objection. Record the project language in HANDOFF.md. An existing README in another language is only translated if approved in the adaptation plan.
- Code, code comments, commits and issues are in English unless the user says otherwise.
- Never translate existing product text unless the user asks.
- Short replies, but never leave out important information. No unnecessary technical detail.
- No running commentary during work, unless something important needs the user's attention.
- When something unclear affects the result: ask rather than guess.

## MANUAL STEPS FOR THE USER
- Give everything needed to complete the step, with direct links where possible.
- Text to be copied, pasted or searched for goes in its own code block (one per value) so it can be copied with a button.
- Other information needed for the step is clearly marked but not put in code blocks.
- Suggest integrations that reduce manual steps, and flag in advance integrations that will be needed.

## RESOURCES
- Conserve quota without sacrificing quality: read selectively instead of the whole repo and avoid unnecessary reruns. Speed is not a priority unless stated otherwise.

## SENSITIVE INFORMATION
- Personal data and other sensitive information is only published with explicit approval. The question must explain why it is needed, what it makes easier, and what the risks and consequences are.
- Secrets (API keys, tokens, passwords) are never committed. Use GitHub Secrets or equivalent and make sure .gitignore covers local secret files.
- Keys that are public by design (e.g. Firebase web config) may be in the code, but then access rules must protect the data.
- Project-sensitive information: information that must not be easily accessible to the project's own users, e.g. solutions, answers, coordinates or unpublished content. Flag such information when it appears, including in existing code.
- Briefly describe how the information is exposed, e.g. in a public repo, in source code sent to the browser, in network requests or in git history (anything committed remains even if deleted later).
- Present the available protection options, with protection level, pros and cons and what is required of the user. Examples: obfuscation (only stops casual guessing), hashing (the answer is checked without being stored in plain text), encryption where the key is provided by the game itself, server-side checking (e.g. Cloudflare Worker) or a private repo.
- Let the user choose the protection before the information is committed.
- The agent-rules repo is public: never put sensitive information there.

## CHANGELOG
- Unreleased:
  - Adaptation plan with numbered categories and items that can be approved or stopped individually; ID conversion, unmerged branches and found documentation go into the plan.
  - Clarifications: project's AGENTS.md (not the rules) may be pushed without go-ahead; claude/ prefix for all agents; auto-merge conflicts resolved in the same session; fixed "Inventory: YYYY-MM-DD" line; goals and way of working as sections in HANDOFF.md.
  - New major version: adaptation only after the user approves an adaptation plan.
  - Conflicts: one complete adaptation plan approvable with one answer. Changes on other branches must reach main in the same run.
  - Language: HANDOFF.md and BACKLOG.md accept Swedish and English without translation; project language (product text and README) English by default but set per project by the user; code, comments and commits in English.
  - Rule changes are collected in a draft (drafts/AGENTS-next.md) and only published when the user explicitly says so.
- 1.0 (2026-11-11): First version.
