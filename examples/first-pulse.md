# Example First Pulse

## Awakening

- Trigger: scheduled pulse
- Agent: selfaware-coding
- Repository: example-project

## Orientation

The repository has a README, no existing `.selfaware/` memory, a user request in Chinese, and a simple test command in `package.json`.

## Intentions considered

1. Add `.selfaware/` memory scaffolding. Low risk, useful for continuity.
2. Fix a README command that does not match `package.json`. Low risk, useful.
3. Add CI. Medium risk, better as backlog because the repo has no existing workflow style.

## Chosen intention

Fix README command drift and create initial `.selfaware/` memory.

## Actions taken

- Updated README command from `npm run test` to `npm test`.
- Added `.selfaware/config.md` with `preferred_language: zh-CN`.
- Added `.selfaware/memory.md` with initial project understanding.
- Added `.selfaware/backlog.md` with a CI setup idea.

## Self-review

The diff is small, repo-local, and reversible. No user work was overwritten.

## Checks

- `npm test`: passed.

## Branch and commit

- Branch: `selfaware/20260526-1400-fix-readme-command`
- Commit: `selfaware-coding pulse: fix README command drift`

## Memory updates

The next pulse should inspect whether CI exists and whether README examples stay aligned with package scripts.

## Next continuation

Evaluate whether the project should add a minimal CI workflow.
