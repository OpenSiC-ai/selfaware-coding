# Risk Policy

Use this when choosing whether to act, plan, or stop during a pulse.

## Default

Act when the improvement is:

- repository-local,
- useful,
- bounded,
- reversible,
- low or medium risk.

Plan instead of acting when the change is high risk, broad, irreversible, outside repository scope, or blocked by host permissions.

## Low Risk: Act

Allowed examples:

- fix README drift,
- clarify documentation,
- add or update small examples,
- add a small test for existing behavior,
- fix obvious typos or broken links,
- remove clearly stale comments,
- update `.selfaware/` memory and backlog.

## Medium Risk: Act With Extra Review

Allowed after careful diff review and relevant checks:

- small bug fixes,
- light refactors with tests,
- test configuration improvements,
- minor dependency metadata changes,
- small CI or lint configuration adjustments.

## High Risk: Plan Only

Write a concrete plan or backlog item unless the repository explicitly authorizes action:

- public API changes,
- database or storage migrations,
- authentication, authorization, payment, or security logic,
- large dependency changes,
- deleting large amounts of code,
- broad architecture rewrites,
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

## Dirty State

Before editing, inspect git status.

Do not overwrite, revert, or reformat user work you did not create.

If dirty state makes an intention unsafe, choose another intention or record the idea for later.
