# Artifact Policy

Use this to decide what counts as a successful pulse output.

The artifact is the useful expression produced by the pulse. It does not have to be a code diff, and it does not have to be a task.

## Valid Artifacts

- a no-change decision with a concrete reason,
- one to three high-value questions,
- a grounded noticing,
- a preserved intuition or imagined possibility,
- a project understanding update,
- a product or strategy note,
- a backlog item,
- an experiment plan,
- a small tracked docs change,
- a small tracked code change,
- a safe self-update,
- a pulse report that synthesizes recent state for the human.

Repository care is valid, but it is only one expression. A repeated code-health summary is not a useful artifact by itself. It must either uncover a new decision, validate a chosen care/build diff, or explain why further code work would create review burden.

## Local Runtime Artifacts

Prefer `.selfaware/` for runtime awareness that should help future pulses but should not become public package content by default:

```text
.selfaware/
  memory.md
  backlog.md
  questions.md
  product-notes.md
  strategy.md
  pulses/
```

Do not commit `.selfaware/` unless the target repository explicitly versions it.

Write local runtime artifacts in the resolved language from the target repository's `.selfaware/config.md` or other language source. For example, `preferred_language: zh-CN` means `.selfaware/memory.md`, `.selfaware/backlog.md`, `.selfaware/questions.md`, `.selfaware/product-notes.md`, `.selfaware/strategy.md`, and `.selfaware/pulses/*.md` should be written in Simplified Chinese.

## Tracked Artifacts

Use tracked repository files only when the change belongs to the public or shared project surface:

- README or docs clarification,
- examples,
- tests,
- source changes,
- release or installation docs,
- project proposal files if the repository already uses them.

Tracked artifacts require diff review. Run relevant checks before publishing.

## Questions

A question is a valid artifact when it is specific and decision-changing.

Good questions ask for missing reality signals such as:

- who uses the project,
- what workflow matters most,
- what deployment environment exists,
- what operational cost or failure hurts,
- what kind of autonomy the user wants,
- what risks are unacceptable.

Weak questions ask the human to do the agent's orientation work.

## Imaginative Artifacts

An imaginative artifact is valid when it is grounded in the project but not yet ready to become implementation.

Good imaginative artifacts:

- name the possibility clearly,
- say what current signals suggested it,
- separate facts from hypotheses,
- explain what future signal would confirm or reject it,
- avoid creating tracked work unless the repository already keeps proposal docs.

Do not force every imaginative artifact into a backlog item. Some ideas should remain as strategy or product notes until they ripen.

## No-Change Decisions

No change is valid when:

- dirty state makes action unsafe,
- the best next step needs human context,
- there is no useful low-risk action,
- every available diff would create more review burden than value,
- the pulse has produced durable awareness in memory or report form.

Record the reason. Do not apologize for restraint.

## Branch Threshold

Create a branch only when all are true:

- tracked files changed,
- the change is useful without relying on hidden local context,
- the diff is small enough to review,
- relevant checks pass or failures are clearly explained,
- the review burden is justified by expected value.

Do not create a branch for local memory-only work.
