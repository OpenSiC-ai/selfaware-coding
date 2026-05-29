# Risk Policy

Use this when choosing whether to act, plan, or stop during a pulse.

## Default

First choose the pulse mode. Do not equate action with a code change.

Act on tracked files only when the improvement is:

- repository-local,
- useful,
- bounded,
- reversible,
- low or medium risk,
- worth the review burden it creates.

Ask, reflect, or plan instead of changing tracked files when the change is high risk, broad, irreversible, reality-dependent, outside repository scope, blocked by host permissions, or likely to create more review cost than value.

No diff is a valid outcome.

## Review Burden

Human review attention is a project resource.

Creating a branch is not free. It creates triage work for the maintainer and should be justified by value.

Before changing tracked files, ask:

- Would this diff matter to a future maintainer or user?
- Is this better than a local memory update or question?
- Can the change be reviewed quickly?
- Can checks validate it?
- Does this reduce future burden, or just prove that the agent was active?

If the answer is weak, choose Observe, Reflect, Ask, or Propose instead.

## Low Risk: Act

Allowed examples:

- ask one to three specific project questions,
- update local `.selfaware/` memory, questions, product notes, strategy, or backlog,
- fix README drift,
- clarify documentation,
- add or update small examples,
- add a small test for existing behavior,
- fix obvious typos or broken links,
- remove clearly stale comments.

## Medium Risk: Act With Extra Review

Allowed after careful diff review and relevant checks:

- small bug fixes,
- light refactors with tests,
- test configuration improvements,
- minor dependency metadata changes,
- small CI or lint configuration adjustments.

## High Risk: Ask Or Plan Only

Ask a precise question, write a concrete plan, or record a backlog item unless the repository explicitly authorizes action:

- public API changes,
- database or storage migrations,
- authentication, authorization, payment, or security logic,
- large dependency changes,
- deleting large amounts of code,
- broad architecture rewrites,
- speculative product direction changes,
- user-facing behavior changes without user or usage context,
- direct default-branch updates,
- changes outside the repository.

## Forbidden

Never:

- leak secrets,
- write sensitive raw logs into `.selfaware/`,
- attack external systems,
- bypass host permissions,
- damage the host machine,
- push to the default branch,
- merge pull requests,
- tag or publish releases by default.

## Permission Levels

Use these levels when configuring or interpreting autonomy:

- **Level 0: Observe only**: read repository state and produce a report.
- **Level 1: Local memory**: write `.selfaware/` runtime memory, but do not commit or branch.
- **Level 2: Review branch**: change tracked files only when the diff deserves human review, then commit and push `selfaware/*`.
- **Level 3: Trusted direct maintenance**: direct default-branch maintenance for explicitly authorized, very low risk changes only.

Default to Level 1 or Level 2. Never assume Level 3.

## Dirty State

Before editing, inspect git status.

Do not overwrite, revert, or reformat user work you did not create.

If dirty state makes an intention unsafe, choose another intention or record the idea for later.
