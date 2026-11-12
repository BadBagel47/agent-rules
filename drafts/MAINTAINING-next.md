> **DRAFT – NOT IN EFFECT.** Until published, the workflow is the UPDATING THE RULES section in [AGENTS.md](../AGENTS.md).

# Maintaining the global agent rules

Applies only when working in BadBagel47/agent-rules.

- Proposals are tracked in BACKLOG.md with IDs AR-001, AR-002 … and a status (Förslag, I utkast, Publicerad, Nekad).
- An agent may propose changes to these rules. Changes the user has approved are first collected in the draft drafts/AGENTS-next.md, never directly in AGENTS.md. The draft is never in effect.
- The draft is a full copy of AGENTS.md with the changes applied, marked as a draft at the top, with the changes listed under "Unreleased" in drafts/CHANGELOG-next.md (a draft of CHANGELOG.md). If the draft is missing: create it from the current AGENTS.md.
- The original lives in the public repo BadBagel47/agent-rules. If the agent lacks write access: ask the user to grant access (e.g. add the repo to the session) and give ready-made steps for it.
- Publish only when the user explicitly says so (e.g. "Publicera reglerna"). Then:
  1. Save the current AGENTS.md unchanged as versions/AGENTS-vX.Y.md.
  2. Copy the draft to AGENTS.md, remove the draft marking and set the new version number and today's date:
     - X (major) when existing content in repos must be changed, moved or removed, e.g. new file structure or new ID system.
     - Y (minor) for clarifications and additions, including new sections or notes that are only added.
  3. In CHANGELOG.md, replace "Unreleased" with a line: version, date and a short description of what changed.
  4. Mark the published proposals as Publicerad in BACKLOG.md with the version.
  5. Delete the drafts.
- The rules are written in English. The user may describe the change in Swedish.
- Commit and push to main per the normal rules and report the new version.

