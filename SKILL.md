---
name: skill-write-refactor
description: Write or refactor Codex skills with focused content, routing-first structure, and maintenance-aware splits. Use when creating a new skill or tightening an existing one; rewriting SKILL.md frontmatter or trigger text; separating high-frequency operational guidance from low-frequency references; adding read-when/skip-when routing; evaluating whether AGENTS.md should act as an index for a growing skill document set; co-locating hard rules with soft preferences; or reducing skill bloat while preserving necessary repetition for binding.
---

# Skill Write Refactor

Write skills that stay easy to trigger, easy to route, and cheap to load. Keep `SKILL.md` on the hot path and add more files only when frequency, branching, or maintenance pressure justifies them.

## Why This Skill Exists

This skill exists to help the model understand the design purpose of a skill, not just mechanically edit one.

Use it to preserve a few core outcomes:

- the skill should be easy to trigger correctly
- the hot path should stay focused on high-frequency runtime guidance
- low-frequency detail should be routed instead of crowding the main file
- `AGENTS.md` can behave like an index-bearing control surface when needed
- repeated drift, scan cost, or ambiguity should lead to structural tightening instead of more loose prose

If a skill edit only changes wording but makes the design purpose less legible, the refactor is incomplete.

## Quick Start

1. Classify the work: new skill, existing-skill refactor, or narrow metadata repair.
2. Read the current authorities in order:
   - applicable `AGENTS.md`
   - target `SKILL.md`
   - `agents/openai.yaml`
   - only the specific references, scripts, or assets that matter
3. Define the high-frequency core:
   - trigger description
   - main workflow
   - read-when/skip-when routing
   - hard constraints and adjacent soft preferences
4. Split out low-frequency detail only when it makes the main skill easier to scan, trigger, or maintain.
5. Validate the folder after edits and refresh `agents/openai.yaml` if the UI metadata drifted.

## Route The Work

### New Skill

- Start from the trigger surface first. Write the frontmatter description before the body so the invocation boundary is explicit.
- Keep the first version single-file unless the task already has obvious low-frequency branches or reusable scripts.

### Existing Skill Refactor

- Preserve the skill name unless scope has materially changed.
- Keep the current trigger behavior unless there is a concrete reason to sharpen or narrow it.
- Remove template prose, dead references, and repeated exposition before inventing new structure.
- Move detail outward only after deciding what must stay hot in `SKILL.md`.

## Keep Content Focused

- Keep `SKILL.md` biased toward actions the skill should help with often.
- Write for the next agent run, not for a human reader learning the domain from scratch.
- Prefer short directives, routing bullets, and compact examples over long explanations.
- Put non-obvious procedure in the skill. Omit generic advice the model already knows.
- Allow small repetition when it improves binding on a critical behavior. Do not repeat for style.

## Bind Method To Action And Boundary

Do not stop at abstract methodology.

For every critical workflow block, include all three when they matter:

- the method or purpose: what the block is trying to achieve
- the concrete action: what the agent should actually do
- the boundary: what stays in scope, what must not be inferred loosely, or what requires escalation

If a section explains the idea but does not tell the reader what to do next, it is incomplete.
If a section tells the reader what to do but not where the boundary is, it is unsafe.

When writing the boundary, explicitly answer both:

- when this behavior should be used
- when this behavior should not be used, skipped, or escalated

If a boundary rule only says "do X" but not "do not do X when Y is true", it is still underspecified.

## Split High Frequency From Low Frequency

Treat `SKILL.md` as the hot path.

Keep in `SKILL.md`:
- frontmatter trigger description
- primary workflow
- read-when/skip-when routing
- invariants, edge-condition checks, and compact examples
- the minimum context needed to choose the right branch

Move to `references/` only when the content is real but colder:
- variant-specific guidance
- detailed examples
- long policy or style notes
- background theory
- large checklists that are not needed on every invocation

Use `scripts/` when the same deterministic helper would otherwise be rewritten repeatedly.
Use `assets/` only for output artifacts or templates, not for extra prose.

## Use AGENTS As An Index

Treat local `AGENTS.md` as an optional routing surface, not a default edit target.

Recommend lifting content into local `AGENTS.md` only when that content needs to stay useful even for runs that do not explicitly invoke the skill.

Use or update local `AGENTS.md` only when at least one of these is true:

- the user explicitly wants `AGENTS.md` created, changed, or kept in sync
- the skill directory already has a local `AGENTS.md` that serves as a routing/index surface and would become stale if the skill structure changes
- the user explicitly wants an index-bearing control surface for a multi-file skill
- some routing or operating guidance needs to be used frequently even when the skill itself is not explicitly invoked

If none of those are true, you may recommend a local `AGENTS.md`, but do not create or modify it by default.

When a skill grows beyond a single hot document and `AGENTS.md` is in play, use a local `AGENTS.md` as a routing index, not as a second full procedure.

Use local `AGENTS.md` to:
- declare the authoritative files
- define read order
- describe read-when/skip-when decisions
- point to summary headers or indexes for larger document sets
- surface only the small set of high-frequency rules or routing pointers that should still help when the skill is not explicitly loaded

Do not use local `AGENTS.md` to:
- restate the full skill body
- carry stale copies of rules that already live elsewhere
- replace the frontmatter trigger surface

If the skill stays small and single-file, skip local `AGENTS.md`.
If the user did not ask for `AGENTS.md` work and no local `AGENTS.md` exists yet, skip it by default and keep the refactor focused on the skill files themselves.

## Add Read-When / Skip-When Routing

Make optional material cheap to ignore.

For each non-core file, state:
- read when: the concrete condition that makes it relevant
- skip when: the condition that makes it unnecessary

Good routing language is explicit:
- Read `references/aws.md` when the user chose AWS.
- Skip `references/aws.md` for local-only frontend work.

Bad routing language is vague:
- Read this for more information.

## Co-Locate Hard And Soft Rules

Keep strict constraints and preferences in the same local section so the agent sees both at decision time.

Use a compact pattern:
- `Hard:` mandatory rule or invariant
- `Soft:` preferred default, heuristic, or bias

Example:
- `Hard:` Keep the frontmatter description aligned with the real trigger surface.
- `Soft:` Prefer shortening the body before creating another reference file.

Do not put hard rules in one file and the related preference in another unless the split is itself necessary and routed.

## Use Repetition Deliberately

Repeat a rule only when repetition improves compliance.

Allowed repetition:
- mention a critical boundary once in frontmatter trigger wording and once in the operational body
- restate a failure-prone constraint near the exact workflow step where it matters
- repeat a routing rule in a local index and in the file it governs when that prevents wrong reads

Avoid repetition when it only adds prose weight, duplicate examples, or parallel headings with the same meaning.

## Use Trigger-Style Attention Control

Treat the description line and the top of `SKILL.md` as attention controls.

Frontmatter description should:
- say what the skill does
- say when to use it
- include concrete trigger phrases or situations
- stay specific enough to beat nearby overlapping skills

The top of `SKILL.md` should:
- confirm the core job in 1-2 sentences
- surface the main routing decision quickly
- avoid deep background before the first action

If a skill is being triggered too broadly, narrow the description. If it is being missed, add concrete use cases and sharper verbs.

Place trigger-style reminders where they are most likely to pay off:

- high-value decision points
- easy-drift middle sections where the model often starts improvising
- easy-to-forget constraints that are frequently dropped in long edits
- globally drift-prone or globally forgettable rules that protect the whole structure

Do not scatter trigger language everywhere. Put it where attention is likely to decay and where one short reminder can redirect the next action.

## Use Maintenance Thresholds

Do not split early just because a split is possible. Split when maintenance pressure is real.

Useful thresholds:
- create `references/` when low-frequency detail is large enough that it obscures the hot path or when three or more distinct cold branches exist
- if multiple files now need stable read order or routing, consider recommending local `AGENTS.md`; create or modify it only when the user asked for that surface or when an existing local `AGENTS.md` must be kept in sync
- extract a `script/` when you have rewritten the same helper more than once or need deterministic behavior
- refresh `agents/openai.yaml` whenever `SKILL.md` changes the scope, tone, or trigger wording
- prune or merge files when a reference is rarely needed and no longer earns its cognitive overhead

Favor evidence over fixed counts. If the same confusion, drift, or scan cost appears repeatedly, the structure is too loose.

## Refactor Checklist

1. Re-state the real job of the skill in one sentence.
2. Tighten the frontmatter description until the trigger boundary is explicit.
3. Mark the hot-path content that must remain in `SKILL.md`.
4. Mark colder detail that can move outward or be deleted.
5. Add or sharpen read-when/skip-when routing.
6. Decide whether `AGENTS.md` is in scope for this refactor; if not explicitly requested and not already present, do not add it by default.
7. Check that each critical block includes method, concrete action, and scope boundary instead of only abstract guidance.
8. Co-locate hard rules and soft preferences near the decisions they govern.
9. Keep only deliberate repetition.
10. Validate the folder.

## Validate

- Run the skill initializer only for new skills, not refactors.
- Run `quick_validate.py` after edits.
- Update `agents/openai.yaml` if `display_name`, `short_description`, or `default_prompt` no longer match the skill.
- Forward-test only when the skill is complex enough that real usage could expose routing or binding failures.
