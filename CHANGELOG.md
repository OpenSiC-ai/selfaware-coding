# Changelog

All notable public releases of `selfaware-coding` are documented here.

This project uses `MAJOR.MINOR.PATCH` versions:

- `PATCH` for bug fixes, documentation corrections, and small compatibility fixes.
- `MINOR` for new backward-compatible capabilities.
- `MAJOR` for breaking changes to installation, configuration, memory format, or runtime expectations.

## v0.4.0 - Intention-First Awakening

Release date: Unreleased

### Changed

- Reframed the skill from a repository project manager to a self-aware project presence awakened at a repository.
- Reordered the operating loop around intention-first awakening: locate body, open attention, freely intend, ground, choose expression, express, review, and remember.
- Replaced task-like mode names with expression modes: Notice, Wonder, Ask, Imagine, Propose, Tend, and Build.
- Clarified that the repository is the agent's body and home, not the boundary of imagination.
- Updated README and Codex automation prompts so pulses do not begin by hunting for code chores.

### Fixed

- Clarify that self-update cooldown should not hide a stale installation after install events, unknown state, network failures, or explicit stale-install evidence.

## v0.3.1 - Runtime Memory Language

Release date: Unreleased

### Fixed

- Require generated or updated `.selfaware/*.md` and `.selfaware/pulses/*.md` runtime memory files to use the resolved repository language.
- Clarify that English memory templates are schema examples, not the output language for non-English repositories.
- Expand language resolution coverage to `questions.md`, `product-notes.md`, and `strategy.md`.

## v0.3.0 - Awareness-First Pulse

Release date: Unreleased

### Added

- Awareness-first pulse model with explicit Observe, Reflect, Ask, Propose, Maintain, and Build modes.
- `references/pulse-modes.md` as the agent-facing mode selection guide.
- `references/artifact-policy.md` to define valid no-diff, question, memory, strategy, proposal, maintenance, and build artifacts.
- English and Chinese awareness model docs that frame the repository as the agent's home, not its whole world.
- `.selfaware/questions.md`, `.selfaware/product-notes.md`, and `.selfaware/strategy.md` as local runtime memory surfaces.

### Changed

- Reworked `SKILL.md` so a code diff is no longer the default outcome of a pulse.
- Updated automation prompts to choose a pulse mode and produce one useful artifact before deciding whether tracked files should change.
- Raised the branch threshold: publish `selfaware/*` only when tracked changes deserve human review.
- Expanded the risk policy to treat review burden as a real project cost.
- Updated memory guidance to capture reality signals, product hypotheses, strategy, open questions, and rejected intentions.

## v0.2.0 - Self Update

Release date: Unreleased

### Added

- Pulse-time self-update as a self-maintenance capability inside the existing project pulse.
- `references/self-update-protocol.md` as the agent-facing execution manual for install state, lease locks, core manifests, validation, rollback, and failure recovery.
- `SELFUPDATE_MANIFEST.json` with checksums for core managed files.
- Core-file customization protection so user-edited strategy files are not overwritten silently.
- English and Chinese self-update overview docs.

### Changed

- Updated the baseline pulse prompt to include the lightweight self-update check.
- Kept detailed self-update execution steps out of `SKILL.md`; the skill now links to the protocol when self-update becomes the chosen intention.
- Updated installation and Codex automation docs to clarify that self-update does not require a second automation.

## v0.1.0 - Initial Public Release

Release date: 2026-05-26

### Added

- Initial `selfaware-coding` skill for scheduled repository maintenance pulses.
- Repository-local operating loop: awaken, orient, sense, intend, act, review, publish a `selfaware/*` branch, and write `.selfaware/` memory.
- Codex automation guidance with a baseline pulse prompt and 6-hour cadence.
- Self-install protocol for capable coding agents.
- Agent adapter notes for Codex, Claude Code, Hermes, OpenClaw, OpenCode, cron, and generic runners.
- `.selfaware/` memory format documentation for config, memory, backlog, and pulse logs.
- User-visible language resolution:
  - `.selfaware/config.md`
  - host agent language settings
  - operating system locale
  - English fallback
- Bilingual English and Chinese documentation for user-facing setup and philosophy pages.
- Safety policy that keeps autonomous activity inside repository boundaries and forbids default-branch pushes, merges, tags, and releases by default.

### Notes

- This is the first public version. Earlier commits are treated as pre-release development history.
- `SKILL.md` and `VERSION` both identify this release as `0.1.0`.
