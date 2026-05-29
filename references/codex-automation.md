# Codex Automation

Use this checklist to create or verify a Codex automation for `selfaware-coding`.

## Skill Install

Required local layout:

```text
~/.codex/skills/selfaware-coding/SKILL.md
```

Preferred installer values:

```text
repo: OpenSiC-ai/selfaware-coding
path: .
name: selfaware-coding
```

Rules:

- Use a real directory, not a symlink.
- Restart Codex or open a new session after install.
- Verify `selfaware-coding` appears in the skill manager and `/` command before relying on the automation prompt.

## Automation

Working directory: target repository root.

Do not set the working directory to the `selfaware-coding` package repository unless the user explicitly wants this skill to maintain itself.

Cadence:

```text
Every 6 hours
```

Reasoning effort: use the host default unless the user asks otherwise.

## Baseline Prompt

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Before emitting user-visible text, resolve the user-visible language from .selfaware/config.md, host agent language settings, OS locale, then English. Use the resolved language for visible progress, reasoning summaries, reports, and .selfaware/ memory. Perform the built-in lightweight self-update check. Orient yourself, read existing .selfaware/ memory if present, and understand this repository as the project's home, not its whole world. Choose one pulse mode: Observe, Reflect, Ask, Propose, Maintain, or Build. Produce one useful artifact: a no-change decision, question, memory update, product note, strategy note, backlog item, proposal, small maintenance diff, or small build diff. Do not assume code must change. Commit and push a selfaware/* branch only when tracked files changed and the diff is worth human review. Do not push to the default branch, merge, tag, or release.
```

## Language

Resolve language using `language-resolution.md`.

Codex Desktop host setting:

- `$CODEX_HOME/config.toml`
- `~/.codex/config.toml`
- `%CODEX_HOME%\config.toml`
- `%USERPROFILE%\.codex\config.toml`

Field:

```text
[desktop].localeOverride
```

Use:

```text
language_source: codex.desktop.localeOverride
```

## Git Permission

Required for full maintenance:

- create branch,
- commit,
- push `selfaware/*`.

Not required:

- default branch push,
- PR merge,
- tag,
- release,
- package publish.

Branch permission does not mean every pulse should publish a branch. Local memory-only, question-only, observe, and reflect pulses should not create branches unless the target repository explicitly versions those artifacts.

## Verify

Installation is usable when:

- `~/.codex/skills/selfaware-coding/SKILL.md` exists,
- `SKILL.md` frontmatter is parseable,
- skill appears in Codex skill manager and `/` command,
- automation working directory is the target repo root,
- automation prompt references `selfaware-coding`,
- branch push is configured or recorded as unavailable,
- language source is imported or intentionally left as English,
- no second updater automation was created.

Expected pulse outputs:

- pulse mode,
- chosen intention,
- artifact produced or reason for restraint,
- checks and results,
- branch/commit if pushed,
- `.selfaware/` memory updates,
- next continuation.
