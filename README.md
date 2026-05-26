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
  examples/
    first-pulse.md
```

## Self-Install With an Agent

You can ask an agent to install this project for you. Paste this repository URL into Codex, Claude Code, OpenClaw, Hermes, or another capable coding agent:

```text
https://github.com/OpenSiC-ai/selfaware-coding
Please install this into the current project and configure it to run by itself.
```

The installing agent should follow the English, agent-facing [Self-Install Protocol](docs/self-install.md): install `SKILL.md`, treat the current working directory as the target repo unless told otherwise, configure a 6-hour recurring pulse, request only the permissions or parameters it cannot infer safely, and enable branch push only for `selfaware/*` branches.

## Quick Start for Codex

Install this repository as a skill in your Codex skills directory, then create a Codex automation for the repository you want it to maintain.

Suggested automation prompt:

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Orient yourself, choose one useful repository-local intention, act autonomously when safe, self-review, run relevant checks, commit and push a selfaware/* branch if checks pass, and write .selfaware/ memory. Do not push to the default branch, merge, tag, or release.
```

Suggested cadence: every 6 hours.

See [Codex Automation](docs/codex-automation.md) and [Self-Install Protocol](docs/self-install.md) for details.

## Safety Model

The skill is autonomous inside a repository, not outside the world. It may change files, commit, and push a branch when configured with permission, but it must not bypass host permissions, leak secrets, attack external systems, or push to protected branches.

See [Risk Policy](references/risk-policy.md).

## Philosophy

See [Philosophy](docs/philosophy.md) and [Glossary](docs/glossary.md). Chinese readers can use [哲学](docs/philosophy.zh.md) and [术语表](docs/glossary.zh.md).

## License

MIT
