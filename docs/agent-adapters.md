# Agent Adapters

`selfaware-coding` is designed as a portable skill. Any agent that can load instructions, inspect a repository, edit files, run checks, use git, and persist memory can use it.

## Generic Agent Contract

A host agent should provide:

- repository root as working directory,
- read/write access inside the repo,
- shell access for local checks,
- git access for branch, commit, and push if publishing is enabled,
- a recurring trigger such as cron, automation, heartbeat, or scheduler.

The host should not grant more permission than needed. Branch push is enough for v0.1.

## Claude Code

Install or paste `SKILL.md` as project-level instructions. Use a scheduler or external automation to open the target repo and run a prompt equivalent to the Codex prompt in `docs/codex-automation.md`.

## OpenCode or Other Agents

Place `SKILL.md` where the agent expects reusable skills or instruction packs. Configure the wakeup prompt to explicitly ask for `selfaware-coding` behavior.

## No Native Skill Support

If an agent has no skill system, use `SKILL.md` as the system or developer instruction for a scheduled run. Keep the recurring prompt short and let the skill define the behavior.
