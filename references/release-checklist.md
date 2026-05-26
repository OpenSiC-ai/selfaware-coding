# Package Readiness Checklist

Use this before committing or publishing changes to `selfaware-coding`.

## Scope

- Keep `SKILL.md` focused on runtime behavior for a scheduled pulse.
- Keep installation details in `docs/self-install.md`, `docs/codex-automation.md`, and adapter docs unless the skill itself must know them.
- Preserve the branch safety rule: pulses may push `selfaware/*` branches, but must not push the default branch, merge, tag, or release.
- Preserve the OpenSiC framing: OpenSiC is the umbrella layer; `selfaware-coding` is the concrete repo-maintenance skill.

## File Inventory

- `SKILL.md` has valid YAML frontmatter and clear operating instructions.
- `VERSION` matches `SKILL.md` frontmatter.
- `CHANGELOG.md` has an entry for the version being released.
- `README.md` and `README.zh.md` link to the install, automation, philosophy, glossary, and risk docs.
- English and Chinese docs stay paired when a concept is user-facing in both languages.
- `references/memory-format.md` matches the `.selfaware/` files the skill writes.
- `examples/first-pulse.md` stays aligned with the current output contract in `SKILL.md`.

## Checks

Run the lightweight checks that fit this docs-only repository:

```sh
git status --short --branch
git ls-files | sort
rg -n "TODO|FIXME|TBD|broken|symlink|skill manager|/ command|Codex|automation|selfaware" .
rg -n "version:|Current version|当前版本|CHANGELOG|VERSION|v[0-9]+\\.[0-9]+\\.[0-9]+" SKILL.md README.md README.zh.md CHANGELOG.md VERSION
git diff --check
```

Before pushing, inspect the diff manually and confirm no secrets, local-only logs, or host-specific paths leaked into public docs.

For a public release, tag the release commit and publish the tag:

```sh
git tag -a v0.1.0 -m "selfaware-coding v0.1.0"
git push origin v0.1.0
```

Then create a GitHub Release from the tag using the matching `CHANGELOG.md` entry.
