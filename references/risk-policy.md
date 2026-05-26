# Risk Policy

This policy defines what `selfaware-coding` may do autonomously during a pulse.

## Default: Act Inside the Repo

The agent should act by default when it finds a useful, bounded, reversible repository-local improvement.

## Low Risk: Act

Examples:

- fix README drift,
- clarify documentation,
- add or update small examples,
- add a small test for existing behavior,
- fix obvious typos or broken links,
- remove clearly stale comments,
- update `.selfaware/` memory and backlog.

## Medium Risk: Act With Extra Review

Examples:

- small bug fixes,
- light refactors with tests,
- test configuration improvements,
- minor dependency metadata changes,
- small CI or lint configuration adjustments.

For medium-risk work, inspect the diff carefully and run the most relevant checks before committing.

## High Risk: Plan Instead of Acting

Examples:

- public API changes,
- database or storage migrations,
- authentication, authorization, payment, or security logic,
- large dependency changes,
- deleting large amounts of code,
- broad architecture rewrites,
- changes outside the repository.

Write a concrete plan or backlog entry unless the repository explicitly authorizes the change.

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

Do not overwrite, revert, or reformat user work you did not create. If dirty state makes a good intention unsafe, choose another intention or record the idea for later.
