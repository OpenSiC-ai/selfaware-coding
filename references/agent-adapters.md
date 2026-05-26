# Agent Adapters

Use this when installing `selfaware-coding` into a host agent other than the current one, or when checking whether an installation is complete.

## Generic Contract

Required host capabilities:

- load `SKILL.md` or equivalent instructions,
- run in the target repository root,
- read and write files inside the repository,
- run local shell checks,
- use git branch, commit, and push when publishing is enabled,
- run from a recurring trigger: cron, automation, heartbeat, scheduler, or equivalent,
- persist `.selfaware/` runtime memory in the target repository.

Minimum git permission: push branches under `selfaware/*`.

Do not require default-branch push, merge, tag, release, package publish, or broad host-machine access.

## Adapter Matrix

| Host | Install form | Recurring trigger | Language source |
| --- | --- | --- | --- |
| Codex | Real directory at `~/.codex/skills/selfaware-coding` | Codex automation | `codex.desktop.localeOverride` |
| Claude Code | Reusable skill if supported, else project instructions | External scheduler or host workflow | `claude.settings.language` |
| OpenClaw | Instruction pack | `HEARTBEAT.md` or equivalent | `openclaw.agent.language` |
| Hermes | Reusable instruction, project policy, or workflow instruction | Hermes scheduler/workflow | `hermes.display.language` or `hermes.env.HERMES_LANGUAGE` |
| OpenCode | Reusable skill/instruction path if available | External scheduler or host workflow | OS locale unless config exposes a language field |
| Generic | `SKILL.md` as system/developer instruction | Cron/automation/scheduler | `.selfaware/config.md`, host setting, OS locale, English |

## Codex

1. Install as a real directory, not a symlink:

   ```text
   ~/.codex/skills/selfaware-coding/SKILL.md
   ```

2. Prefer the Codex skill installer:

   ```text
   repo: OpenSiC-ai/selfaware-coding
   path: .
   name: selfaware-coding
   ```

3. Restart Codex or open a new session.
4. Verify `selfaware-coding` appears in the skill manager and `/` command.
5. Create the automation using `codex-automation.md`.
6. Resolve language using `language-resolution.md`.

Ask for permission only when writing to the skills directory, creating automation, or configuring branch push requires host approval.

## Claude Code

1. Use a reusable skill mechanism if available.
2. If no reusable skill mechanism exists, install `SKILL.md` as project instructions.
3. Configure an external scheduler or host workflow to open the target repository and run the baseline pulse prompt.
4. Resolve language from `.claude/settings.local.json`, `.claude/settings.json`, then `~/.claude/settings.json`; read `language`.
5. Use `language_source: claude.settings.language`.

Ask before writing project-level instruction files or global Claude configuration when permission is required.

## OpenClaw

1. Install `SKILL.md` as an instruction pack available to the target project.
2. Configure `HEARTBEAT.md` or equivalent heartbeat mechanism to run the baseline pulse prompt every 6 hours.
3. Resolve language from `$OPENCLAW_CONFIG_PATH`, `~/.openclaw/openclaw.json`, or `~/.openclaw/openclaw.yaml`.
4. Candidate fields: `agents.defaults.language`, `agents.*.language`.
5. Use `language_source: openclaw.agent.language`.

Ask only for project-specific path, account, or heartbeat location when not discoverable.

## Hermes

1. Install `SKILL.md` as reusable instruction, project policy, or workflow instruction pack.
2. Bind the baseline pulse prompt to Hermes scheduler, workflow, or recurring task.
3. Resolve language from `$HERMES_CONFIG_PATH`, `~/.hermes/config.yaml`, or `HERMES_LANGUAGE`.
4. Candidate field: `display.language`.
5. Use `language_source: hermes.display.language` or `hermes.env.HERMES_LANGUAGE`.

Ask which workspace/project/deployment target only when multiple targets exist and cannot be inferred.

## OpenCode Or Generic

1. Place `SKILL.md` where the host expects reusable skills or instruction packs.
2. Configure the wakeup prompt to explicitly invoke `selfaware-coding`.
3. Keep the recurring prompt short; let `SKILL.md` define behavior.
4. Resolve language using `language-resolution.md`.

For OpenCode language lookup, try:

- `~/.config/opencode/opencode.json`,
- `~/.config/opencode/tui.json`,
- `%XDG_CONFIG_HOME%\opencode\...`,
- `%APPDATA%\opencode\...`,
- `%USERPROFILE%\.config\opencode\...`.

If no clear language field exists, continue to OS locale.
