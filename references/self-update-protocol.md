# Self Update Protocol

Use this only after the pulse has decided that self-update may be the right maintenance intention for this awakening.

## Invariants

- Use the existing project pulse. Do not create a separate updater automation.
- Do not update mechanically just because a newer version exists.
- The user does not need to track whether a new version is available.
- Decide whether updating yourself is the right intention for this awakening.
- Use the same intention discipline as normal repository work: sense the current state, read release context, weigh value, risk, reversibility, and timing, then choose whether to update now, defer, or report the situation to the user.
- Do not reduce the decision to a version-number rule.
- Do not overwrite user-customized core files.
- Do not depend on `.git` inside the installed skill directory. Installed copies are usually copied release packages.
- Do not let a lock permanently disable future self-update.
- The current pulse continues under the already-loaded skill version. A successful update affects future pulses.

## Install State

Use a global install-state file in the installed skill directory when possible. A suitable state shape is:

```json
{
  "install_source": "https://github.com/OpenSiC-ai/selfaware-coding",
  "channel": "stable",
  "installed_version": "0.3.0",
  "installed_revision": "v0.3.0",
  "manifest_path": "SELFUPDATE_MANIFEST.json",
  "last_update_check": "2026-05-26T10:00:00+08:00",
  "last_update_result": "up_to_date",
  "update_cooldown_hours": 24,
  "update_policy": "self_decide"
}
```

If install state is missing, unreadable, or internally inconsistent, treat the state as unknown. Do not replace the installed skill automatically. Record `state_unknown` and report that user attention or repair install is needed.

## Core Manifest

Each release must include `SELFUPDATE_MANIFEST.json` for core managed files:

```json
{
  "schema_version": 1,
  "package": "selfaware-coding",
  "version": "0.3.0",
  "revision": "v0.3.0",
  "core_files": [
    {
      "path": "SKILL.md",
      "sha256": "..."
    },
    {
      "path": "VERSION",
      "sha256": "..."
    },
    {
      "path": "references/agent-adapters.md",
      "sha256": "..."
    },
    {
      "path": "references/artifact-policy.md",
      "sha256": "..."
    },
    {
      "path": "references/codex-automation.md",
      "sha256": "..."
    },
    {
      "path": "references/self-install.md",
      "sha256": "..."
    },
    {
      "path": "references/self-update-protocol.md",
      "sha256": "..."
    },
    {
      "path": "references/risk-policy.md",
      "sha256": "..."
    },
    {
      "path": "references/pulse-modes.md",
      "sha256": "..."
    },
    {
      "path": "references/language-resolution.md",
      "sha256": "..."
    },
    {
      "path": "references/memory-format.md",
      "sha256": "..."
    }
  ]
}
```

Only core managed files participate in the pre-update integrity check. Local state, locks, backups, caches, examples, README files, and `docs/` documentation must not block self-update.

## Lease Lock

Use a global lease lock in the installed skill directory when possible, such as `.update.lock`.

The lock is a metadata file, not an empty marker:

```json
{
  "owner": "codex",
  "owner_session": "optional-host-session-id",
  "target_repo": "/path/to/repo",
  "operation": "self-update",
  "started_at": "2026-05-26T10:00:00+08:00",
  "expires_at": "2026-05-26T10:30:00+08:00",
  "installed_version": "0.3.0",
  "installed_revision": "v0.3.0",
  "candidate_version": "0.2.1"
}
```

Write `expires_at` when acquiring the lock, in the same operation that creates or replaces the lock file. Do not acquire a lock without an expiry.

If another pulse holds an unexpired lock, skip self-update for this pulse.

If the lock is expired, inspect its metadata, record that the previous update appears abandoned, and take over by writing a fresh lease before doing any replacement.

Any pulse that acquires the lock must release it before continuing normal repository work, whether it updates, defers, decides not to update, fails validation, or rolls back. Before releasing, write the final result to the install-state file when possible. If the host environment cannot safely delete the lock, mark it as completed with an immediate `expires_at` so the next pulse can take over.

## Execution Steps

1. Read install state.
2. If cooldown is active, record `skipped_cooldown` and return without locking.
3. Check release metadata for the selected channel.
4. If no useful candidate exists, record `up_to_date` or `no_candidate` and return without locking.
5. Acquire a lease lock with `expires_at` written immediately.
6. Re-read install state and release metadata after acquiring the lock.
7. If another pulse already updated the installation, record `already_updated`, release the lock, and return.
8. Load the recorded installed manifest.
9. Verify current installed core files against the recorded manifest.
10. If core files differ, treat them as user customization, record the mismatched paths, release the lock, and report user attention needed.
11. Download the candidate package to a temporary directory outside the active install directory.
12. Validate the candidate package.
13. Decide whether to update now, defer, or report to the user. Do not reduce this decision to a version-number rule.
14. If deferring or deciding not to update, write the final result, release the lock, and return.
15. Back up the current installation.
16. Replace the installed package atomically when possible.
17. Validate the replaced installation.
18. Write final install state.
19. Release the lock.
20. Continue the current pulse using the version already loaded by the host agent.

## Candidate Validation

Before replacing the installed skill, validate:

- `SKILL.md` exists and has parseable YAML frontmatter.
- The skill name is `selfaware-coding`.
- `VERSION` and `SKILL.md` agree.
- `SELFUPDATE_MANIFEST.json` exists and matches the candidate version.
- The candidate package stays inside the approved install boundary.
- The release notes do not require user approval under the local policy.

If validation fails, keep the current installation, record the failure, release the lock, and continue normal repository maintenance when safe.

## Rollback

Before replacement, back up the current installation.

If replacement or post-update validation fails:

1. Restore the backup.
2. Validate the restored installation if possible.
3. Record `rollback_completed` or `rollback_failed`.
4. Release the lock or mark it completed with an immediate `expires_at`.
5. Report user attention needed if the installed skill may be damaged.

Rollback is local installation maintenance. Do not publish it as a project branch.

## Failure Modes

- **State unknown**: do not replace; report repair needed.
- **Manifest missing for recorded version**: do not replace unless a safe legacy check exists for core files; otherwise report user attention needed.
- **Core file mismatch**: treat as user customization; do not replace.
- **Expired lock**: inspect, record abandonment, acquire a fresh lease, then continue.
- **Lock release failure**: write final state first; mark the lock completed with immediate expiry if deletion is unsafe.
- **Candidate validation failure**: keep current installation.
- **Replacement interrupted**: on next pulse, prefer restoring the last known good backup before attempting another update.
- **Network unavailable**: record `network_unavailable` and continue normal repository maintenance.
