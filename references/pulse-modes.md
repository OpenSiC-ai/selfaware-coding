# Pulse Modes

Use this when choosing what a pulse should do.

A pulse does not have to modify tracked files. Choose the mode that best serves project continuity with the least unnecessary review burden.

## Mode Selection

Consider:

- value to the project,
- missing reality signals,
- risk and reversibility,
- review cost for humans,
- whether a branch is truly worth inspecting,
- whether local `.selfaware/` memory is enough,
- whether a question would unlock better future action than a diff.

## Observe

Purpose: understand current state without changing files.

Use when:

- the repository is unfamiliar,
- dirty state makes action unsafe,
- recent changes need synthesis,
- no specific intention is trustworthy yet.

Allowed artifacts:

- final report,
- pulse log if local memory is enabled,
- concise `.selfaware/memory.md` update when it records durable orientation.

Do not create a branch.

## Reflect

Purpose: form project awareness, direction, or judgment.

Use when:

- the most useful work is interpreting the project,
- product direction, adoption, user value, operational context, or architecture intent is unclear,
- code changes would be premature.

Allowed artifacts:

- `.selfaware/product-notes.md`,
- `.selfaware/strategy.md`,
- `.selfaware/backlog.md`,
- final report with specific reasoning.

Do not create a branch unless the target repository explicitly versions these notes.

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

## Propose

Purpose: turn an idea into a concrete option without implementing it.

Use when:

- the idea may be valuable but is too broad for one pulse,
- implementation needs approval,
- the change would affect product direction, public API, security, release behavior, or data handling.

Allowed artifacts:

- `.selfaware/strategy.md`,
- `.selfaware/backlog.md`,
- tracked proposal docs only when the repository already uses tracked proposal docs or the user asked for them.

Create a branch only for a tracked proposal worth human review.

## Maintain

Purpose: perform bounded upkeep.

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

Use sparingly. Build mode needs a stronger reason than Maintain mode.

Use when:

- the repository context clearly supports the change,
- the scope is small enough for one pulse,
- tests or checks can validate behavior,
- the change aligns with recorded user goals or repository roadmap.

Do not use Build for speculative product ideas without user approval. Propose or Ask instead.

## Self-Update

Self-update is not a separate mode. It can be the chosen intention inside Maintain when the installed skill needs safe maintenance and `references/self-update-protocol.md` allows it.

Do not update mechanically just because a newer version exists.
