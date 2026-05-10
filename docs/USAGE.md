# Usage

## Working Order

Use the skill in this order:

1. Classify the task as `new skill`, `existing-skill refactor`, or `metadata repair`.
2. Read the active authorities:
   - applicable `AGENTS.md`
   - target `SKILL.md`
   - `agents/openai.yaml`
   - only the specific side materials that the current task actually needs
3. Identify the hot-path content that must remain in `SKILL.md`.
4. Decide whether any colder detail should move outward, stay in place, or be deleted.
5. Re-check that each critical section contains:
   - method
   - concrete action
   - scope boundary
6. Refresh `agents/openai.yaml` when the skill's trigger wording, scope, tone, or default prompt changed.
7. Validate the folder and do a final drift pass before handoff.

## Packaging Guidance

For a publishable repository, keep the packaging lightweight unless the skill itself already needs more structure.

- Required:
  - `AGENTS.md`
  - `SKILL.md`
  - `agents/openai.yaml`
  - `README.md`
  - `README.zh-CN.md`
- Recommended:
  - `LICENSE`
  - `.gitignore`
  - `docs/USAGE.md`
- Add local `AGENTS.md` when the published package has enough maintained files that stable read-order and maintenance routing are worth making explicit.

## Example Prompts

- `Use $skill-write-refactor to create a new Codex skill for MCP server authoring.`
- `Use $skill-write-refactor to tighten this bloated SKILL.md without changing its trigger boundary.`
- `Use $skill-write-refactor to split high-frequency guidance from long reference material and add read-when/skip-when routing.`
- `Use $skill-write-refactor to rewrite this skill description so it stops colliding with nearby overlapping skills.`
- `Use $skill-write-refactor to decide whether this growing skill now needs a local AGENTS.md index.`

## Verification Notes

The source skill mentions `quick_validate.py`, but repository packaging should not assume that helper exists in every install target.

- Run the local validator when it exists.
- If it does not exist, verify by checking file completeness, metadata alignment, and the final git diff.
- When packaging a repo, confirm that installation paths and README layout match the actual tree.
