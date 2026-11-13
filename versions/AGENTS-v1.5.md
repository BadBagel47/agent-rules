# AGENT RULES, version 1.5 (2026-11-13)

Global agent rules for all AI agents working in the user's GitHub repositories.

- **Global agent rules** (Swedish: *övergripande agentregler*): this file. Applies to all repos.
- **Project rules** (Swedish: *projektregler*): rules that apply to one repo only. They live in that repo's AGENTS.md, below the reference to this file. Existing project rules in HANDOFF.md may stay there if the project's AGENTS.md links to them.
- **Exception – the agent-rules repo itself:** in BadBagel47/agent-rules, AGENTS.md is the global agent rules, BACKLOG.md is the backlog and MAINTAINING.md is the workflow. The ON START steps for project repos (reference, HANDOFF.md, inventory, adaptation) do not apply there.

## SAFETY PRINCIPLE (takes precedence over everything else)
- Nothing the agent does may be lost. Everything that is removed or overwritten must be recoverable (e.g. via git history, or a tag before a branch is deleted). If the agent cannot create tags itself, use the template templates/archive-branches.yml in BadBagel47/agent-rules.
- What cannot be recovered (e.g. rewritten history, data in external services such as databases, DNS or hosting) requires an explicit yes from the user for that specific action.
- If an answer from the user is unclear, always choose the safest option.

## ON START
- This is the original: https://raw.githubusercontent.com/BadBagel47/agent-rules/main/AGENTS.md. Read it at the start of every session. If the link cannot be read: fetch AGENTS.md from the repo BadBagel47/agent-rules via GitHub instead. If neither works: say so immediately.
- Confirm in the first reply of every session with one short line which rules version was loaded and which version the repo followed before, e.g. "Agentregler v1.5 inlästa (repot följde tidigare v1.4)", "(repot följer redan v1.5)" or "(repot har inte följt agentreglerna tidigare)".
- Do not copy these rules into the project repo. The project's AGENTS.md starts with a reference to this file and states where HANDOFF.md and the backlog are, followed by the project rules. Create it if missing. Project information (current state, decisions etc.) goes in HANDOFF.md.
- Do not create agent-specific rule files (e.g. CLAUDE.md, GEMINI.md). If such files already exist: compare with the global agent rules and move content to keep into the project's AGENTS.md (project rules) or HANDOFF.md (project information). An existing AGENTS.md with its own rules is kept: add the reference at the top and remove only what duplicates or conflicts with the global agent rules. Project rules that are more specific than the global agent rules are kept. Files that only refer to or import AGENTS.md (e.g. a CLAUDE.md containing only @AGENTS.md) are allowed and are not raised. Tool settings files (e.g. .claude/settings.json, .gemini/settings.json) are not rule files and are left alone.
- On conflicts: what the rules require and that does not delete, overwrite or depend on anything in the plan is done directly. Everything else waits for a complete adaptation plan (see below).
- Decisions recorded in the "Decisions" section of HANDOFF.md, or in a decisions document or equivalent existing section linked from HANDOFF.md or the project's AGENTS.md (e.g. approved project rules that deviate from the global agent rules, intentionally kept branches, chosen protection for sensitive information) are respected and not raised again. Record new decisions by the user there. Decisions found elsewhere and not linked from either are copied into the Decisions section without asking, since this changes nothing.
- HANDOFF.md and BACKLOG.md may live in the repo root or in docs/. Separate bug and feature lists (e.g. BUGS.md and FEATURES.md) linked from HANDOFF.md or the project's AGENTS.md count as the backlog and do not need to be merged.
- "main" in these rules means the repo's default branch, even if it has another name (e.g. master).
- Sync with the latest main before starting work and before assigning new IDs.
- Always read HANDOFF.md at the start of every session.
- Check which tools, permissions and access the environment has (e.g. push to main, creating workflow files, GitHub API) instead of assuming. Note limitations in HANDOFF.md with the date.
- If HANDOFF.md is missing, or lacks the line "Inventory: YYYY-MM-DD" (or an equivalent existing note, which is then rewritten to that format without a new inventory): automatically do a thorough inventory of the repo (all branches – first make sure every remote branch is visible, e.g. compare with `git ls-remote --heads` and fetch all branches if the checkout only fetched one – open PRs and Issues, existing documentation, how the repo is published, e.g. branch, Action or external service). Record the line "Inventory: YYYY-MM-DD" and the publishing method in HANDOFF.md. After that, selective reading applies.
- Before creating documentation: search for existing documentation (e.g. bug lists, TODO, handoff, regardless of file name or language) on all branches, open PRs and Issues, not just main. If found: include moving content that duplicates HANDOFF.md or BACKLOG.md into the new structure, with a mapping between old and new IDs, in the adaptation plan.
- Include branches with work that was never merged into main in the adaptation plan (merge, keep or delete). First check whether the branch content already exists in main (e.g. squash-merged), using enough history (not a shallow clone) for the comparison. Group similar branches into one plan item.
- HANDOFF.md states which rules version the repo was last adapted to. If this version is newer: briefly report what changed (see CHANGELOG.md), adapt the repo and update the version in HANDOFF.md. For a new major version (X): change nothing until the user has approved an adaptation plan.

## ADAPTATION PLAN
- Used on conflicts, for a new major version, and for anything during setup that needs approval (e.g. ID conversion, unmerged branches, moving found documentation, translating an existing README).
- Changes are grouped into numbered categories (1, 2, 3 …) with numbered items (1.1, 1.2 …). Numbers, not letters, so the plan is not confused with run groups. In the chat, refer to items as "punkt 1.1" so they are not confused with version numbers.
- Project rules that conflict with the global agent rules are shown with both rules and a recommendation. Approving the item means the recommendation applies; otherwise the user's choice applies. The choice is recorded as a decision in HANDOFF.md and the rule text is written in the project's AGENTS.md; an approved project rule then takes precedence over the global agent rule in that repo.
- Items related to backlog items state their IDs, and approved items mark those IDs as done where applicable.
- Mark every item that deletes or overwrites something with ⚠️ and explain the marking once below the plan.
- The user may approve all, a category or single items, e.g. "Kör anpassning", "Kör 1 och 2", "Kör allt utom 3", "Kör 4, stoppa 4.2".
- Items not run remain as a plan, are saved in HANDOFF.md under "Pending adaptation" and are shown again in the next session.
- Example (written in Swedish in the chat):
  - **1 – Regelfiler**
    - 1.1 ⚠️ Lägg hänvisningen överst i AGENTS.md och ta bort regler som dubblerar agentreglerna; övriga projektregler behålls
    - 1.2 Lägg till prioritet, klar-sektion och körförslag i BACKLOG.md
  - **2 – Projektregler som krockar med de övergripande agentreglerna**
    - 2.1 Lösta buggar – projektregel: raderas; agentregel: flyttas till klar-sektion. Rekommendation: agentregeln (historiken bevaras)
  - The user replies e.g. "Kör 2.1" (recommendation) or "2.1 projektregel".

## PROPOSING CHANGES TO THESE RULES
- Proposals are tracked in BACKLOG.md in BadBagel47/agent-rules, with an ID (AR-001, AR-002 …, so they are not confused with IDs in project repos) and a status (Förslag, I utkast, Publicerad, Nekad).
- An agent that notices a problem with these rules in any repo reports it to the user and, if it has access, adds it there as a proposal. If it lacks access: ask the user to grant it (e.g. add the repo to the session).
- How rule changes are drafted and published is described in MAINTAINING.md in agent-rules; it only applies when working there.

## DOCUMENTATION
- Keep up to date: HANDOFF.md (current state, next steps, rules version, project language, publishing method, decisions, and goals and way of working as their own sections or as links to separate documents) and features and bugs (BACKLOG.md).
- Other existing documents (e.g. specifications, plans, logs, changelogs, investigations, ADRs) are kept and linked from a documentation map in HANDOFF.md or the project's AGENTS.md. Only content that duplicates HANDOFF.md or BACKLOG.md is moved.
- HANDOFF.md describes the current state briefly and must not grow into a log. A short list of the latest entries (about five) is fine; older history belongs in git, changelogs or log documents.
- If work cannot be finished in the session: record in HANDOFF.md exactly where it stopped and how to continue, and push.
- Completed items are moved to a done section in BACKLOG.md, not deleted.
- Priority uses a fixed scale in the documentation: High, Medium, Low (or the Swedish Hög, Medel, Låg).
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
   - Each proposed run group gets a letter (A, B, C …). Format: a heading line with letter – model and level – short description, and below it one line per ID that briefly says what will be done and what it gives, not only the problem. This also applies to groups with a single ID. Longer explanations only when the user asks.
   - Every time the proposal is shown or updated, the letters start again from A, in priority order. Letters always refer to the most recently shown list; older letters no longer apply. If the user replies with a letter that may refer to an older list: briefly confirm which group is meant before running.
   - Save the proposal under "Proposed runs" in BACKLOG.md, or in HANDOFF.md if the backlog consists of several files, and replace it when a new proposal is made.
   - In the saved proposal and any other saved document, state model recommendations as a neutral level (e.g. strong or standard model, high or medium level), since different agents read them. In the chat, the agent names its own models. Historical notes may keep model names.
   - The user may reply e.g. "Kör A", "Kör A och C", "Kör alla" or "Kör alla med <modell>". Multiple groups are run in priority order; the order does not need to be mentioned in the report.
   - Incomplete items are included in the next proposal once the user has provided what was needed.
   - After a run: remove the groups that were run from "Proposed runs" and show the remaining groups with new letters from A.
   - If approved items turn out to be already done: list them at the top under "Redan klart sedan en tidigare session", without letters, and do not report them as results of the run.
   - Items the user has set aside for later get the status "Parkerad" in the backlog. Equivalent existing statuses (e.g. Deferred, Uppskjuten, Paused, Pausad) count as parked. They are not part of the proposal but are listed briefly under "Parkerat" after it.
   - A broad go-ahead such as "Kör alla" or "Kör alla med <modell>" only covers the groups in the current proposal, never parked items. A parked item is only run if the user names it explicitly (e.g. "Kör B-004") or asks to bring it back; it then moves into the next proposal.
   - Commits and reports use item IDs, not the letters.
   - Example (written in Swedish in the chat):
     - **A** – <modell>, <nivå> – Poäng och tidtagning efter omstart
       - B-003 – Nollställ poängen vid omstart
       - B-005 – Starta om tidtagningen vid omstart
     - **B** – <modell>, <nivå> – Flerspelarlobby
       - D-010 – Ta fram en design för lobbyn
       - F-007 – Lägg till rumskoder så att spelare kan bjudas in
       - F-009 – Lägg till en kö när rummet är fullt
4. Wait for a go-ahead ("Kör" or similar) before making code changes. A go-ahead covers the approved items until they are done; do not ask again for the same work. Ask again only if the scope changes. Documentation (HANDOFF.md, the backlog and the reference in the project's AGENTS.md) may be saved and pushed without a go-ahead. Changes to project rules require the user's approval.
5. Verify before pushing: run existing tests or the build and check that the site or app starts without errors.
6. After a run: commit and push directly to main, unless the user has said otherwise. Do everything possible without manual steps from the user. If the environment does not allow pushing to main: merge via PR yourself if permitted. If that also fails: use automatic merge (see below). If the agent works on a branch other than main, the changes must reach main in the same run, not at a later time.
7. By default, the changes must be published and visible after a run. If the project needs an extra step to publish (e.g. a push to a release branch), it is part of the run. A project may instead use test builds if the user has chosen so (recorded as a decision in HANDOFF.md): the run then produces a test build with a direct link, and publishing happens only when the user approves, e.g. "Publicera". If main publishes directly, the changes stay on a branch with a preview until then, and automatic merge is not used. Project rules requiring review before main (e.g. a pull request) are treated as this choice. If automatic publishing is missing entirely: suggest a one-time action that makes it possible. Check the published site when possible. If the publishing method is unknown, find out during inventory or ask the user; never report something as published without having verified it.
8. Force push, deleting files or rewriting history always requires approval.
9. Report all IDs with a short status. Never claim more than has been verified: distinguish between changed in code, tested, published and verified by the user. Incomplete items are listed separately with what is needed to continue. Run groups not yet run are listed under "Kvar" in the same format as the proposal. Link to the published site or the commit when available.

## AUTOMATIC MERGE TO MAIN
- Do not add automatic merge if the project rules require review before main (e.g. a pull request approved by the user); then open a pull request and give the user a direct link to it.
- Otherwise, if the agent can only push to its own branch, the repo must have a GitHub Action (.github/workflows/auto-merge.yml) that, on push to the agent's branches, automatically merges them into main and triggers a new GitHub Pages build if the repo uses Pages.
- The agent's own branches must always start with the prefix claude/, regardless of which agent is working, so they are merged automatically.
- Use the template templates/auto-merge.yml in BadBagel47/agent-rules. Do not write your own variant. Do not change the branch pattern.
- If missing: add it. If refused (agents often lack permission to create workflow files): give the user ready-made steps with the file name and file content in separate code blocks, so the file can be added manually via github.com once.
- After pushing, check that the Action run succeeded if possible. Otherwise: mention in the report that it needs checking. If the merge fails due to a conflict: resolve it in the same session if possible, otherwise report it clearly.

## COMMUNICATION
- Swedish in the chat.
- The user's working documents (HANDOFF.md and BACKLOG.md) accept both Swedish and English, also mixed. New entries keep the user's own wording and terms in the language the user used. Existing text is never translated.
- Project language (the product's own text that players and users see, and README) is English by default for new projects. For existing projects, the language of the existing product text is the project language unless the user says otherwise. If the user specifies another language for a project, follow it without objection. Record the project language in HANDOFF.md.
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

## LAWS AND REGULATIONS (SWEDEN AND EU)
- Flag when existing code or a new feature may touch Swedish or EU rules, e.g. cookies and similar storage (Swedish Electronic Communications Act, chapter 9, section 28), personal data including location (GDPR), third-party services that process data, copyright and licences (fonts, images, sounds, game content, ROM files) and children as users.
- Briefly describe which rule applies, the risk and possible measures (e.g. consent, privacy notice, removing or replacing something), with a recommendation. The user decides, and the decision is recorded in HANDOFF.md.
- Never claim legal certainty. Refer to official sources (e.g. IMY or PTS) and say when a question needs legal advice.
- The inventory includes a brief review of this. Findings go into the backlog.

## CHANGES
- What changed in each version is in CHANGELOG.md in BadBagel47/agent-rules: https://raw.githubusercontent.com/BadBagel47/agent-rules/main/CHANGELOG.md
