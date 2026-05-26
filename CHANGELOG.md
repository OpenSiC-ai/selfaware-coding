# Changelog

All notable public releases of `selfaware-coding` are documented here.

This project uses `MAJOR.MINOR.PATCH` versions:

- `PATCH` for bug fixes, documentation corrections, and small compatibility fixes.
- `MINOR` for new backward-compatible capabilities.
- `MAJOR` for breaking changes to installation, configuration, memory format, or runtime expectations.

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
