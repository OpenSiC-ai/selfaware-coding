# selfaware memory

## Project understanding

`selfaware-coding` is an OpenSiC skill packaged as a portable instruction set for scheduled coding-agent pulses. The repository is documentation-first: `SKILL.md` is the installable skill, while `docs/`, `references/`, and `examples/` explain installation, automation, risk, memory, and first-pulse behavior.

## Stable preferences

- Preserve the OpenSiC framing: OpenSiC is the umbrella philosophy, and `selfaware-coding` is the concrete repo-level coding skill.
- Keep guidance agent-facing and operational. Installation docs should tell an installing agent what to do, what to verify, and when to ask for permission.
- Keep the default automation cadence at 6 hours for v0.1 unless the user changes it.
- Do not push to the default branch, merge, tag, or release from a pulse.

## Risk notes

- Treat broad behavioral changes to `SKILL.md` as higher risk than ordinary docs edits because installed agents consume it directly.
- Treat host-specific install claims as drift-prone. Prefer small checklists and explicit verification steps over assuming a host's current skill manager behavior.
- Avoid storing raw private conversations, credentials, or command logs in `.selfaware/`.

## Repeated observations

- This repo has no code build system yet. Useful checks are Markdown/file inventory checks, link sanity checks, YAML frontmatter inspection, and git diff review.
- The README repository-shape block should stay aligned with any new top-level docs, references, examples, or `.selfaware` conventions that become part of the public package.

## Useful commands

```sh
git status --short --branch
git ls-files | sort
rg -n "TODO|FIXME|TBD|broken|symlink|skill manager|/ command|Codex|automation|selfaware" .
git diff --check
```
