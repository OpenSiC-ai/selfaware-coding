# Self-Install Protocol

This document is written for installation agents. A user should be able to paste the repository URL and ask an agent to install `selfaware-coding` into a target project.

## Installer Contract

When a user says something like:

```text
https://github.com/OpenSiC-ai/selfaware-coding
Please install this into the current project and configure it to run by itself.
```

interpret it as:

1. Install `selfaware-coding` as an agent skill or equivalent instruction pack.
2. Configure the current repository as the target repository unless the user names another target.
3. Create or describe a recurring pulse that runs every 6 hours.
4. Give the pulse permission to maintain the target repo, including committing and pushing `selfaware/*` branches when credentials allow it.
5. Do not push to the default branch, merge, tag, release, publish packages, or bypass host permissions.

## Required Questions

Ask the user only for missing information or authorization that cannot be inferred safely:

- **Target repository**: ask only if the current working directory is not clearly the target repo.
- **Host agent**: ask only if the environment does not reveal whether this is Codex, Claude Code, OpenClaw, Hermes, or another agent.
- **Write permission**: ask before writing outside the current sandbox or installing into a global skill directory.
- **GitHub permission**: ask when branch push is requested but credentials are missing or invalid.
- **Cadence**: default to every 6 hours unless the user asks for a different interval.
- **Language**: ask only if the user wants persistent `.selfaware/` memory in a specific language and has not named it.

Do not ask whether to install the skill after the user has already asked for installation. Do not ask whether it should act autonomously; autonomy inside the target repo is the purpose of this skill.

## Installation Steps

1. Resolve the target repo root.
2. Fetch or clone `https://github.com/OpenSiC-ai/selfaware-coding`.
3. Validate that the selected `SKILL.md` has parseable YAML frontmatter.
4. Install the repository into the host agent's skill or instruction location.
5. Configure the recurring pulse using the prompt below.
6. Verify that the host agent can load the skill.
7. Verify git state and branch-push credentials if publishing is enabled.
8. Create `.selfaware/config.md` with `preferred_language` only when the user explicitly provides a persistent language preference.
9. Run a dry first pulse or explain how the first scheduled pulse will run.

## Baseline Pulse Prompt

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Orient yourself, read .selfaware/config.md and existing .selfaware/ memory if present, respect the configured preferred_language for user-facing reports and .selfaware/ memory, choose one useful repository-local intention, act autonomously when safe, self-review, run relevant checks, commit and push a selfaware/* branch if checks pass, and write .selfaware/ memory. Do not push to the default branch, merge, tag, or release.
```

## Host Defaults

- **Codex**: install into `~/.codex/skills/selfaware-coding` as a real directory, preferably through Codex's skill installer. Do not leave a symlink as the final installed skill because Codex's skill manager and `/` command may not index symlinked skill directories. Restart Codex or open a new session, confirm that `selfaware-coding` appears in the skill manager and `/` command, then create a Codex automation with the target repo as `cwd`.
- **Claude Code**: install as a reusable skill/instruction pack if supported; otherwise add `SKILL.md` as project instructions and use an external scheduler.
- **OpenClaw**: use `SKILL.md` as the selfaware-coding instruction pack and invoke it from the project's heartbeat or equivalent recurring mechanism.
- **Hermes**: install `SKILL.md` as the agent's reusable instruction or project policy, then bind the baseline prompt to its scheduler, workflow, or recurring task mechanism.
- **Other agents**: use `SKILL.md` as system/developer instructions for a recurring run.

## Success Criteria

An installation is complete when:

- the host agent can load `selfaware-coding`,
- Codex installations show `selfaware-coding` in the skill manager and `/` command after restart,
- the target repo is known,
- a recurring 6-hour pulse exists or is clearly documented for that host,
- language preference is configured only when the user explicitly provided one,
- `.selfaware/` memory policy is understood,
- branch-push permission is either configured or explicitly recorded as unavailable,
- the user knows that default-branch push, merge, tag, and release are disabled by default.
