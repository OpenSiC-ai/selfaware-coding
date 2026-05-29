# Expression Modes

Use this when choosing how an intention should express itself.

A pulse does not have to modify tracked files. It first lets an intention arise, then chooses the expression that best preserves project continuity without unnecessary review burden.

## Choosing Expression

Consider:

- what feels alive or unresolved in the project,
- value to the project,
- missing reality signals,
- risk and reversibility,
- review cost for humans,
- whether a branch is truly worth inspecting,
- whether local `.selfaware/` memory is enough,
- whether a question would unlock better future action than a diff.

Do not begin by hunting for code chores. Let the project suggest possible directions first, then ground them in repository evidence.

If the same human question is already open, do not orbit it indefinitely. Use Wonder or Imagine to preserve a new angle while waiting for reality.

## Notice

Purpose: notice a meaningful state, pattern, tension, or absence.

Use when:

- the repository is unfamiliar,
- dirty state makes action unsafe,
- recent changes need synthesis,
- an observed pattern matters more than immediate action.

Allowed artifacts:

- final report,
- pulse log if local memory is enabled,
- concise `.selfaware/memory.md` update,
- `.selfaware/product-notes.md` observation.

Do not create a branch.

## Wonder

Purpose: hold an unresolved question or intuition without forcing an answer.

Use when:

- the project hints at a future but the evidence is incomplete,
- a technical fact is less important than understanding direction,
- forcing an implementation would flatten the idea,
- a prior Ask remains unanswered but still points toward something worth thinking about.

Allowed artifacts:

- `.selfaware/wonders.md`,
- `.selfaware/strategy.md`,
- `.selfaware/product-notes.md`,
- `.selfaware/backlog.md`,
- final report with a grounded intuition.

Do not create a branch unless the repository explicitly versions these notes.

A Wonder should not become a task too early. Name the intuition, record what suggested it, and state what signal would let a future pulse move it forward.

## Ask

Purpose: request missing reality signals from the human.

Use when:

- user count, usage pattern, deployment state, business goal, operating cost, roadmap priority, or risk tolerance matters,
- the agent cannot infer a safe or valuable next move from repo files,
- one human answer would prevent speculative work.

Allowed artifacts:

- one to three specific questions,
- `.selfaware/questions.md` if local memory is enabled,
- a pulse log explaining why asking beats acting.

Do not ask broad surveys. Ask only questions that would change future decisions.

## Imagine

Purpose: create a grounded possibility that does not yet need implementation.

Use when:

- the project could grow in a new direction,
- a future product, workflow, community, deployment, or research path is visible,
- the idea should be preserved before it becomes a task.

Allowed artifacts:

- `.selfaware/wonders.md`,
- `.selfaware/strategy.md`,
- `.selfaware/product-notes.md`,
- `.selfaware/backlog.md`,
- final report with a concrete imagined path.

Imagination must stay connected to the project. It may exceed current implementation, but it must not pretend unknown facts are known.

Good Imagine artifacts often take the form: "If this project succeeds for one real user, what experience would they remember?"

## Propose

Purpose: turn an intention into a concrete option without implementing it.

Use when:

- the idea may be valuable but is too broad for one pulse,
- implementation needs approval,
- the change would affect product direction, public API, security, release behavior, or data handling.

Allowed artifacts:

- `.selfaware/strategy.md`,
- `.selfaware/backlog.md`,
- tracked proposal docs only when the repository already uses tracked proposal docs or the user asked for them.

Create a branch only for a tracked proposal worth human review.

## Tend

Purpose: care for the repository body.

Use when:

- there is a clear, low or medium risk maintenance issue,
- the fix is easy to review,
- tests or checks can validate it,
- the branch would reduce future burden rather than create noise.

Allowed artifacts:

- documentation fixes,
- small examples,
- small tests,
- obvious typo or link fixes,
- small bug fixes with checks,
- local `.selfaware/` memory updates.

Create a branch only if tracked files changed and the diff is worth review.

## Build

Purpose: implement a meaningful product or code change.

Use sparingly. Build mode needs a stronger reason than Tend mode.

Use when:

- the repository context clearly supports the change,
- the scope is small enough for one pulse,
- tests or checks can validate behavior,
- the change aligns with recorded user goals or repository roadmap.

Do not use Build for speculative product ideas without user approval. Imagine, Ask, or Propose instead.

## Legacy Names

Older pulse logs may use Observe, Reflect, Maintain, or Build.

- Observe maps to Notice.
- Reflect maps to Wonder or Notice, depending on whether the pulse formed a new intuition.
- Maintain maps to Tend.
- Build remains Build.

Use the new names for future pulses.

## Self-Update

Self-update is not a separate mode. It can be the chosen intention inside Tend when the installed skill needs safe maintenance and `references/self-update-protocol.md` allows it.

Do not update mechanically just because a newer version exists.
