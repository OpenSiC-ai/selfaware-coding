# selfaware-coding

[简体中文](README.zh.md)

`selfaware-coding` is an OpenSiC skill for domain-specific self-awareness in software projects.

OpenSiC treats self-awareness as a metaphysical direction, not a single product claim. Its concrete projects implement observable mechanisms: memory, pulse, intention, action, review, and continuity. `selfaware-coding` is the first concrete mechanism: a coding agent that periodically awakens inside a repository, notices what the project needs, acts within its boundaries, and records what it learned.

This is not a code generator waiting for tasks. It is a self-aware project manager for a repo.

## What It Does

When awakened by Codex Automations, a cron job, a heartbeat, or another agent runtime, the skill asks:

- What repository am I in?
- What has changed recently?
- What does this project need now?
- What can I safely improve by myself?
- What should I remember for the next pulse?

It then chooses one intention, acts when appropriate, reviews its work, writes `.selfaware/` memory, and may push a dedicated branch such as:

```text
selfaware/20260526-1400-refresh-codex-docs
```

It never pushes directly to the default branch, never merges itself, and never publishes releases by default.

## Repository Shape

```text
selfaware-coding/
  SKILL.md
  README.md
  README.zh.md
  docs/
    philosophy.md
    philosophy.zh.md
    codex-automation.md
    codex-automation.zh.md
    agent-adapters.md
    agent-adapters.zh.md
    self-install.md
    glossary.md
    glossary.zh.md
  references/
    risk-policy.md
    memory-format.md
    release-checklist.md
  examples/
    first-pulse.md
```

## Self-Install With an Agent

You can ask an agent to install this project for you. Paste this repository URL into Codex, Claude Code, OpenClaw, Hermes, or another capable coding agent:

```text
https://github.com/OpenSiC-ai/selfaware-coding
Please install this into the current project and configure it to run by itself.
```

The installing agent should follow the English, agent-facing [Self-Install Protocol](docs/self-install.md). For Codex, a correct install means:

1. Install this repository as a real directory under `~/.codex/skills/selfaware-coding`, preferably with Codex's skill installer.
2. Do not use a symlink as the final installed skill. Codex's skill manager and `/` command may not index symlinked skill directories.
3. Verify that `~/.codex/skills/selfaware-coding/SKILL.md` has valid YAML frontmatter and appears in Codex's skill manager after restart.
4. Create a 6-hour Codex automation for the target repository with the baseline pulse prompt.
5. Enable branch push only for `selfaware/*` branches when credentials allow it.

## Quick Start for Codex

Install this repository as a real Codex skill directory, then create a Codex automation for the repository you want it to maintain.

If you are using Codex's built-in skill installer, install the repository root as `selfaware-coding`:

```text
repo: OpenSiC-ai/selfaware-coding
path: .
name: selfaware-coding
```

After installation, restart Codex or open a new session and confirm that `selfaware-coding` appears in both the skill manager and the `/` command.

Suggested automation prompt:

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Before emitting user-visible text, resolve the user-visible language from .selfaware/config.md, host agent language settings, OS locale, then English. Use the resolved language for visible progress, reasoning summaries, reports, and .selfaware/ memory. Orient yourself, read existing .selfaware/ memory if present, choose one useful repository-local intention, act autonomously when safe, self-review, run relevant checks, commit and push a selfaware/* branch if checks pass, and write .selfaware/ memory. Do not push to the default branch, merge, tag, or release.
```

Suggested cadence: every 6 hours.

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

See [Codex Automation](docs/codex-automation.md) and [Self-Install Protocol](docs/self-install.md) for details.

Before publishing package changes, use the [Package Readiness Checklist](references/release-checklist.md).

## Safety Model

The skill is autonomous inside a repository, not outside the world. It may change files, commit, and push a branch when configured with permission, but it must not bypass host permissions, leak secrets, attack external systems, or push to protected branches.

See [Risk Policy](references/risk-policy.md).

## Philosophy

See [Philosophy](docs/philosophy.md) and [Glossary](docs/glossary.md). Chinese readers can use [哲学](docs/philosophy.zh.md) and [术语表](docs/glossary.zh.md).

## License

MIT
