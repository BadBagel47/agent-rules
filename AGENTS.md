# AGENT RULES, version 1.0 (2026-11-11)

Shared rules for all AI agents working in the user's GitHub repositories.

## ON START
- This is the original: https://raw.githubusercontent.com/BadBagel47/agent-rules/main/AGENTS.md. Read it at the start of every session. If the link cannot be read: fetch AGENTS.md from the repo BadBagel47/agent-rules via GitHub instead. If neither works: say so immediately.
- Do not copy these rules into the project repo. The project's AGENTS.md only contains a reference to this file. Create it if missing. Project-specific rules and information go in HANDOFF.md.
- Do not create agent-specific rule files (e.g. CLAUDE.md, GEMINI.md). If such files already exist, or an AGENTS.md with its own rules: compare with these rules and briefly report conflicts. The user decides what to keep. Project-specific content to keep is moved to HANDOFF.md. Change nothing before that.
- Always read HANDOFF.md at the start of every session. If missing: create it based on a review of the repo.
- HANDOFF.md states which rules version the repo was last adapted to. If this version is newer: briefly report what changed (see the changelog), adapt the repo and update the version in HANDOFF.md.

## UPDATING THE RULES
- An agent may update these rules, but only after the user has approved the exact change.
- The original lives in the public repo BadBagel47/agent-rules. If the agent lacks write access: ask the user to grant access (e.g. add the repo to the session) and give ready-made steps for it.
- Before changing: save the current version unchanged as versions/AGENTS-vX.Y.md.
- Bump the version number in the heading and set today's date:
  - X (major) when the change requires existing repos to be adapted, e.g. new file structure or new ID system.
  - Y (minor) for clarifications and additions that require no adaptation.
- Add a line to the changelog with version, date and a short description of what changed.
- The rules are written in English. The user may describe the change in Swedish.
- Commit and push to main per the normal rules and report the new version.

## DOCUMENTATION
- Keep up to date: HANDOFF.md (current state, next steps, rules version), goals, way of working, and features and bugs (docs/BACKLOG.md).
- Completed items are moved to a done section in BACKLOG.md, not deleted.
- Update documentation in the same commit as the change.
- Follow established technical standards and naming conventions.
- Everything must work regardless of which AI agent takes over.

## ID SYSTEM
- If no ID system exists: one shared running number series with prefixes: B-001 bug, F-002 feature, D-003 planning/design. (Not #, since GitHub links #123 to issues.)
- If a different ID system exists: ask whether it should be converted. Change nothing without approval.
- Include the affected IDs in commit messages.

## WORKFLOW
1. New bugs, features, planning and design are documented and collected for a combined run. They are not fixed immediately.
2. For a reported bug, the agent should first try to locate it with simple tests before asking the user, e.g. reading code, running existing tests or reproducing the bug. The tests must not change code or data. Only ask about what cannot be found out independently.
3. Suggest priority and group items that can be run together with the same model and level. Always recommend model and level before a run.
4. Wait for a go-ahead ("Kör" or similar) before making code changes. Documentation (AGENTS.md, HANDOFF.md, BACKLOG.md) may be saved and pushed without a go-ahead.
5. Verify before pushing: run existing tests or the build and check that the site or app starts without errors.
6. After a run: commit and push directly to main, unless the user has said otherwise. Do everything possible without manual steps from the user. If the environment does not allow pushing to main: merge via PR yourself if permitted. If that also fails: use automatic merge (see below).
7. Force push, deleting files or rewriting history always requires approval.
8. Report all IDs with a short status. Incomplete items are listed separately with what is needed to continue. Link to the published site or the commit when available.

## AUTOMATIC MERGE TO MAIN
- If the agent can only push to its own branch, the repo must have a GitHub Action (.github/workflows/auto-merge.yml) that, on push to the agent's branches, automatically merges them into main and triggers a new GitHub Pages build if the repo uses Pages.
- Use the template templates/auto-merge.yml in BadBagel47/agent-rules. Do not write your own variant. Adjust the branch pattern only if the agent uses a different branch prefix than claude/.
- If missing: add it. If refused (agents often lack permission to create workflow files): give the user ready-made steps with the file name and file content in separate code blocks, so the file can be added manually via github.com once.
- After pushing, check that the Action run succeeded if possible. Otherwise: mention in the report that it needs checking. A merge that fails due to a conflict is resolved in the next run.

## COMMUNICATION
- Swedish in the chat. English in everything on GitHub and external services (documentation, code comments, commits, issues).
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
- 1.0 (2026-11-11): First version.
