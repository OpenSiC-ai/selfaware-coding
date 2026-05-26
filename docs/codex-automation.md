# Codex Automation

This guide describes how to run `selfaware-coding` as a recurring Codex automation.

## Install the Skill

Install this repository as a real Codex skill directory. A correct local layout is:

```text
~/.codex/skills/selfaware-coding/SKILL.md
```

Prefer Codex's skill installer, using:

```text
repo: OpenSiC-ai/selfaware-coding
path: .
name: selfaware-coding
```

Do not use a symlink as the final installed skill. Codex's skill manager and `/` command may not index symlinked skill directories. After installation, restart Codex or open a new session and confirm that `selfaware-coding` appears in both the skill manager and the `/` command before relying on an automation prompt that says `Use the selfaware-coding skill.`

## Automation Target

Create the automation in the repository that should be maintained. The automation working directory should be the target repo root, not the `selfaware-coding` repo unless you intentionally want it to maintain itself.

## Cadence

Recommended cadence for v0.1:

```text
Every 6 hours
```

This is frequent enough to create continuity, but not so frequent that the agent creates noise.

## Prompt

Use this prompt as the baseline:

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Orient yourself, read existing .selfaware/ memory if present, choose one useful repository-local intention, act autonomously when safe, self-review, run relevant checks, commit and push a selfaware/* branch if checks pass, and write .selfaware/ memory. Do not push to the default branch, merge, tag, or release.
```

## GitHub Permission

To maintain a project for real, the automation needs permission to push branches. It does not need permission to push to the default branch, merge pull requests, tag releases, or publish packages for v0.1.

## Expected Result

A successful pulse may produce:

- a small local improvement,
- a commit on a branch named `selfaware/YYYYMMDD-HHMM-<short-intent>`,
- a pushed remote branch,
- `.selfaware/` memory updates,
- a short report with checks and next continuation.

If checks fail, the agent should not push. It should record the failure and a continuation plan.
