# Package Readiness Checklist

Use before committing or publishing package changes to `selfaware-coding`.

## Scope

- Keep `SKILL.md` focused on runtime behavior for a scheduled pulse.
- Keep detailed self-update execution steps in `references/self-update-protocol.md`, not in `SKILL.md`.
- Keep installation details in `references/self-install.md`, `references/codex-automation.md`, and adapter docs unless the skill itself must know them.
- Preserve the branch safety rule: pulses may push `selfaware/*` branches, but must not push the default branch, merge, tag, or release.
- Preserve the OpenSiC framing: OpenSiC is the umbrella layer; `selfaware-coding` is the concrete repo-maintenance skill.

## File Inventory

- `SKILL.md` has valid YAML frontmatter and clear operating instructions.
- `VERSION` matches `SKILL.md` frontmatter.
- `SELFUPDATE_MANIFEST.json` matches the version and checksums for core managed files.
- `references/self-update-protocol.md` matches the self-update behavior summarized by `SKILL.md` and `docs/self-update.md`.
- `CHANGELOG.md` has an entry for the version being released.
- `README.md` and `README.zh.md` link to the install, automation, philosophy, glossary, and risk docs.
- English and Chinese docs stay paired when a concept is user-facing in both languages.
- `references/memory-format.md` matches the `.selfaware/` files the skill writes.
- `references/language-resolution.md` matches the language behavior summarized by `SKILL.md` and install docs.
- `examples/first-pulse.md` stays aligned with the current output contract in `SKILL.md`.

## Checks

Run the lightweight checks that fit this docs-only repository:

```sh
git status --short --branch
git ls-files | sort
rg -n "TODO|FIXME|TBD|broken|symlink|skill manager|/ command|Codex|automation|selfaware" .
rg -n "version:|Current version|当前版本|CHANGELOG|VERSION|v[0-9]+\\.[0-9]+\\.[0-9]+" SKILL.md README.md README.zh.md CHANGELOG.md VERSION
shasum -a 256 SKILL.md VERSION references/agent-adapters.md references/codex-automation.md references/self-install.md references/self-update-protocol.md references/risk-policy.md references/language-resolution.md references/memory-format.md
git diff --check
```

Before pushing, inspect the diff manually. Confirm no secrets, local-only logs, or host-specific paths leaked into public files.

For a public release, tag the release commit and publish the tag, replacing `vX.Y.Z` with the release version:

```sh
git tag -a vX.Y.Z -m "selfaware-coding vX.Y.Z"
git push origin vX.Y.Z
```

Then create a GitHub Release from the tag using the matching `CHANGELOG.md` entry.
