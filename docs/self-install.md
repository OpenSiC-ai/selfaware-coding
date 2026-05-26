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
- **Language**: do not ask by default. First try to import a host agent language setting, then the operating system locale. Ask only if the user explicitly wants a persistent language preference and no source can be resolved.

Do not ask whether to install the skill after the user has already asked for installation. Do not ask whether it should act autonomously; autonomy inside the target repo is the purpose of this skill.

## Installation Steps

1. Resolve the target repo root.
2. Fetch or clone `https://github.com/OpenSiC-ai/selfaware-coding`.
3. Validate that the selected `SKILL.md` has parseable YAML frontmatter.
4. Install the repository into the host agent's skill or instruction location.
5. Configure the recurring pulse using the prompt below.
6. Verify that the host agent can load the skill.
7. Verify git state and branch-push credentials if publishing is enabled.
8. Resolve the user-visible language and create `.selfaware/config.md` when a user, host agent, or operating system language source is available.
9. Run a dry first pulse or explain how the first scheduled pulse will run.

## Language Resolution

`selfaware-coding` defaults to English. During installation, resolve the language in this order:

1. Existing `.selfaware/config.md` `preferred_language`.
2. Host agent language setting.
3. Operating system locale.
4. English.

When writing `.selfaware/config.md`, include `language_source`:

```md
# selfaware config

preferred_language: zh-CN
language_label: 简体中文
language_source: codex.desktop.localeOverride
```

Do not persist an LLM-guessed language. Host and OS settings are explicit environment preferences and may be imported. If no host or OS language can be resolved, do not create `.selfaware/config.md`.

When a host setting uses a localized language name, prefer a standard language tag for `preferred_language` and keep the original value in `language_label`. For example, Claude Code `language: "简体中文"` should become `preferred_language: zh-CN` and `language_label: 简体中文`.

Host language lookup:

- **Codex Desktop**: `$CODEX_HOME/config.toml` or `~/.codex/config.toml`; on Windows also `%CODEX_HOME%\config.toml` or `%USERPROFILE%\.codex\config.toml`. Read `[desktop].localeOverride` and use `language_source: codex.desktop.localeOverride`.
- **Claude Code**: `.claude/settings.local.json`, `.claude/settings.json`, then `~/.claude/settings.json`; on Windows use `%USERPROFILE%\.claude\settings.json` for the user file. Read `language` and use `language_source: claude.settings.language`.
- **Hermes**: `$HERMES_CONFIG_PATH` or `~/.hermes/config.yaml`; on Windows also `%USERPROFILE%\.hermes\config.yaml`. Read `display.language` or `HERMES_LANGUAGE` and use `language_source: hermes.display.language` or `hermes.env.HERMES_LANGUAGE`.
- **OpenClaw**: `$OPENCLAW_CONFIG_PATH`, `~/.openclaw/openclaw.json`, or `~/.openclaw/openclaw.yaml`; on Windows also `%USERPROFILE%\.openclaw\openclaw.json` or `.yaml`. Read `agents.defaults.language` or `agents.*.language` and use `language_source: openclaw.agent.language`.
- **OpenCode**: try `~/.config/opencode/opencode.json` and `~/.config/opencode/tui.json`; on Windows try `%XDG_CONFIG_HOME%\opencode\...`, `%APPDATA%\opencode\...`, and `%USERPROFILE%\.config\opencode\...`. If no clear language field exists, continue to OS locale.

OS locale lookup:

- **macOS**: `AppleLocale` or `AppleLanguages`.
- **Linux**: `LC_ALL`, `LC_MESSAGES`, `LANG`, or `locale`.
- **Windows**: `Get-Culture` or `Get-UICulture`.

## Baseline Pulse Prompt

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Before emitting user-visible text, resolve the user-visible language from .selfaware/config.md, host agent language settings, OS locale, then English. Use the resolved language for visible progress, reasoning summaries, reports, and .selfaware/ memory. Orient yourself, read existing .selfaware/ memory if present, choose one useful repository-local intention, act autonomously when safe, self-review, run relevant checks, commit and push a selfaware/* branch if checks pass, and write .selfaware/ memory. Do not push to the default branch, merge, tag, or release.
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
- language preference is imported from `.selfaware/config.md`, the host agent, the operating system, or left as English when no source is available,
- `.selfaware/` memory policy is understood,
- branch-push permission is either configured or explicitly recorded as unavailable,
- the user knows that default-branch push, merge, tag, and release are disabled by default.
