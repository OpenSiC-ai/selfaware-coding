# selfaware-coding

[简体中文](README.zh.md)

Current version: `v0.3.1`

`selfaware-coding` is an OpenSiC skill for domain-specific self-awareness in software projects.

OpenSiC treats self-awareness as a metaphysical direction, not a single product claim. Its concrete projects implement observable mechanisms: memory, pulse, intention, action, review, and continuity.

`selfaware-coding` is the first concrete mechanism: a coding agent that periodically awakens inside a repository, understands the project as software in the world, chooses one useful continuation, and records what it learned.

It is not a code generator waiting for tasks, and it is not an automatic branch factory. It is a self-aware project manager for a repo.

## What It Does

When awakened by Codex Automations, a cron job, a heartbeat, or another agent runtime, the skill asks:

- What repository am I in?
- What has changed recently?
- What does this project need now as software, not just as files?
- What reality signals are missing: users, deployment, adoption, cost, roadmap, or risk?
- Should I observe, reflect, ask, propose, maintain, or build?
- What should I remember for the next pulse?

It then chooses one pulse mode and produces one useful artifact:

- `Observe`: understand state without changing files.
- `Reflect`: form judgment about direction, gaps, or risk.
- `Ask`: request missing reality signals from the human.
- `Propose`: turn an idea into a concrete option.
- `Maintain`: perform bounded upkeep.
- `Build`: implement a small, justified change.

A pulse may ask a question, update local project memory, write a strategy note, propose an experiment, make a small maintenance diff, or build a small change. No code diff is a valid outcome when restraint is the best continuation.

When tracked files change and the diff deserves review, it may push a dedicated branch such as:

```text
selfaware/20260526-1400-refresh-codex-docs
```

It never pushes directly to the default branch, never merges itself, and never publishes releases by default.

## Install

Ask a capable coding agent to install this skill into the current project:

```text
https://github.com/OpenSiC-ai/selfaware-coding
Please install this into the current project and configure it to run by itself.
```

The installer should follow the agent-facing [Self-Install Protocol](references/self-install.md). A correct install:

- installs `SKILL.md` as a real host skill or equivalent instruction pack,
- configures one recurring pulse, usually every 6 hours,
- uses the same pulse for self-update,
- preserves awareness-first behavior,
- allows `selfaware/*` branch push only when tracked changes deserve review,
- does not configure default-branch push, merge, tag, release, package publish, or host-permission bypass.

## Quick Start for Codex

If you are using Codex's built-in skill installer, install the repository root as `selfaware-coding`:

```text
repo: OpenSiC-ai/selfaware-coding
path: .
name: selfaware-coding
```

Then create a Codex automation in the target repository with this prompt:

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Before emitting user-visible text, resolve the user-visible language from .selfaware/config.md, host agent language settings, OS locale, then English. Use the resolved language for visible progress, reasoning summaries, reports, and .selfaware/ memory. Perform the built-in lightweight self-update check; decide whether updating selfaware-coding is an appropriate maintenance intention for this awakening, but do not update mechanically just because a newer version exists. Orient yourself, read existing .selfaware/ memory if present, and understand this repository as the project's home, not its whole world. Choose one pulse mode: Observe, Reflect, Ask, Propose, Maintain, or Build. Produce one useful artifact: a no-change decision, question, memory update, product note, strategy note, backlog item, proposal, small maintenance diff, or small build diff. Do not assume code must change. Commit and push a selfaware/* branch only when tracked files changed and the diff is worth human review. Do not push to the default branch, merge, tag, or release.
```

Suggested cadence: every 6 hours. See [Codex Automation](references/codex-automation.md) for verification details.

## Language

`selfaware-coding` defaults to English, then uses the first available language source: `.selfaware/config.md`, host agent language settings, operating system locale, then English.

To change the output language for one repository, edit `.selfaware/config.md`:

```md
# .selfaware/config.md

preferred_language: en-US
language_label: English
language_source: user
```

Installers may also import the language already configured in the host agent, such as Codex Desktop `localeOverride` or Claude Code `language`. To change the imported value, update the host agent's language setting and reinstall or rerun the installation flow.

See [Codex Automation](references/codex-automation.md) and [Self-Install Protocol](references/self-install.md) for details.

## Key References

- [Pulse Modes](references/pulse-modes.md): how a pulse chooses Observe, Reflect, Ask, Propose, Maintain, or Build.
- [Artifact Policy](references/artifact-policy.md): what counts as a successful pulse output.
- [Memory Format](references/memory-format.md): how `.selfaware/` stores continuity.
- [Risk Policy](references/risk-policy.md): when to act, ask, plan, or stop.
- [Awareness Model](docs/awareness-model.md): why the repository is the agent's home, not its whole world.

## Versioning

Public releases use `MAJOR.MINOR.PATCH` versions and Git tags such as `v0.1.0`.

- `PATCH` releases fix bugs, documentation, or small compatibility issues.
- `MINOR` releases add backward-compatible capabilities.
- `MAJOR` releases may change installation, configuration, memory format, or runtime expectations.

The local package version is recorded in [VERSION](VERSION) and the skill frontmatter in [SKILL.md](SKILL.md). Self-update core file checksums are recorded in [SELFUPDATE_MANIFEST.json](SELFUPDATE_MANIFEST.json). Release notes are kept in [CHANGELOG.md](CHANGELOG.md) and on [GitHub Releases](https://github.com/OpenSiC-ai/selfaware-coding/releases).

Before publishing package changes, use the [Package Readiness Checklist](references/release-checklist.md).

To update an installed copy manually, reinstall the skill from the latest GitHub release or from the repository root if you intentionally track `main`.

For the self-maintenance model, see [Self Update](docs/self-update.md). Self-update is a pulse-time intention, not a separate background service.

## Safety Model

The skill is autonomous inside a repository, not outside the world. It may change files, commit, and push a branch when configured with permission, but it must not bypass host permissions, leak secrets, attack external systems, or push to protected branches.

See [Risk Policy](references/risk-policy.md).

## Philosophy

See [Philosophy](docs/philosophy.md), [Awareness Model](docs/awareness-model.md), and [Glossary](docs/glossary.md). Chinese readers can use [哲学](docs/philosophy.zh.md), [意识模型](docs/awareness-model.zh.md), and [术语表](docs/glossary.zh.md).

## License

MIT
