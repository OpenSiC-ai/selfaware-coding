# Agent Adapters

`selfaware-coding` is designed as a portable skill. Any agent that can load instructions, inspect a repository, edit files, run checks, use git, and persist memory can use it.

For self-service installation from a repository URL, follow [Self-Install Protocol](self-install.md).

## Generic Agent Contract

A host agent should provide:

- repository root as working directory,
- read/write access inside the repo,
- shell access for local checks,
- git access for branch, commit, and push if publishing is enabled,
- a recurring trigger such as cron, automation, heartbeat, or scheduler.

The host should not grant more permission than needed. Branch push is enough for v0.1.

## Language Import

During installation, adapters should resolve the user-visible language before creating the recurring pulse. Use this order: existing `.selfaware/config.md`, host agent language setting, operating system locale, then English. When a host or OS value is imported, write `.selfaware/config.md` with `preferred_language`, optional `language_label`, and `language_source`.

Users can override the language later by editing `.selfaware/config.md` in the target repository. They can also change the host agent language setting and rerun the installation flow.

## Codex

Install `SKILL.md` into the Codex skills directory, then create a Codex automation with the target repository as the working directory. Use the baseline prompt in `docs/codex-automation.md` and a 6-hour cadence.

Import language from `$CODEX_HOME/config.toml` or `~/.codex/config.toml`, field `[desktop].localeOverride`. On Windows, also check `%CODEX_HOME%\config.toml` and `%USERPROFILE%\.codex\config.toml`. Use `language_source: codex.desktop.localeOverride`.

If creating the automation or writing to the skills directory requires permission, ask the user for that permission directly and continue after approval.

## Claude Code

Install or paste `SKILL.md` as project-level instructions. If Claude Code has a reusable skill mechanism, use it. Otherwise, add the instruction pack to the target project and use an external scheduler to open the target repo and run the baseline pulse prompt.

Import language from `.claude/settings.local.json`, `.claude/settings.json`, then `~/.claude/settings.json`, field `language`. On Windows, the user file is usually `%USERPROFILE%\.claude\settings.json`. Use `language_source: claude.settings.language`.

Ask the user when project-level instruction files or global Claude configuration require write permission.

## OpenClaw

Install `SKILL.md` as an instruction pack available to the target OpenClaw project. Configure `HEARTBEAT.md` or the equivalent heartbeat mechanism to invoke the baseline pulse prompt every 6 hours.

Import language from `$OPENCLAW_CONFIG_PATH`, `~/.openclaw/openclaw.json`, or `~/.openclaw/openclaw.yaml`. On Windows, also check `%USERPROFILE%\.openclaw\openclaw.json` and `.yaml`. Candidate fields are `agents.defaults.language` and `agents.*.language`. Use `language_source: openclaw.agent.language`.

If OpenClaw requires a project-specific path, account, or heartbeat location, ask the user for that parameter. Do not guess paths outside the current project when they are not discoverable.

## Hermes

Install `SKILL.md` as the Hermes agent's reusable instruction, project policy, or workflow instruction pack. Bind the baseline pulse prompt to Hermes' scheduler, workflow, or recurring task mechanism with a 6-hour cadence.

Import language from `$HERMES_CONFIG_PATH` or `~/.hermes/config.yaml`, field `display.language`, or from `HERMES_LANGUAGE`. On Windows, also check `%USERPROFILE%\.hermes\config.yaml`. Use `language_source: hermes.display.language` or `hermes.env.HERMES_LANGUAGE`.

If the Hermes installation exposes multiple workspaces, projects, or deployment targets, ask the user which target should receive selfaware-coding.

## OpenCode or Other Agents

Place `SKILL.md` where the agent expects reusable skills or instruction packs. Configure the wakeup prompt to explicitly ask for `selfaware-coding` behavior.

For OpenCode, try `~/.config/opencode/opencode.json` and `~/.config/opencode/tui.json`; on Windows try `%XDG_CONFIG_HOME%\opencode\...`, `%APPDATA%\opencode\...`, and `%USERPROFILE%\.config\opencode\...`. If no clear language field exists, continue to OS locale.

## No Native Skill Support

If an agent has no skill system, use `SKILL.md` as the system or developer instruction for a scheduled run. Keep the recurring prompt short and let the skill define the behavior.
