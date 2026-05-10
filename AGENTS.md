# AGENTS.md

## Scope

This repository packages the `skill-write-refactor` Codex skill as a standalone public skill repo.

## Authorities

Read files in this order when working on the skill itself:

1. `AGENTS.md`
2. `SKILL.md`
3. `agents/openai.yaml`
4. `README.md` or `README.zh-CN.md` only when you need repo-level orientation, installation notes, or design rationale

## Read-When / Skip-When

- Read `SKILL.md` when changing trigger wording, routing logic, workflow steps, or hard/soft guidance.
- Skip `SKILL.md` only when the task is limited to repo metadata that cannot affect skill behavior.
- Read `agents/openai.yaml` when the skill name, display name, short description, or default prompt might drift from `SKILL.md`.
- Skip `agents/openai.yaml` when the task is purely documentation and the skill surface is unchanged.
- Read `README.md` when you need the English architecture, design rationale, or repo usage notes.
- Read `README.zh-CN.md` when you need the Chinese documentation or are keeping the localized docs aligned.

## Maintenance Rules

- Keep `SKILL.md` as the hot path. Do not duplicate its procedure here.
- Keep `agents/openai.yaml` aligned with the current trigger surface.
- Keep both README files aligned when repo structure, architecture, or usage guidance changes.
- Add `references/`, `scripts/`, or `assets/` only when colder material or deterministic helpers justify the split.
