# Self Install Protocol

Use this when a user asks an agent to install `selfaware-coding` into a repository and configure it to run by itself.

## Interpret Request

If the user provides:

```text
https://github.com/OpenSiC-ai/selfaware-coding
Please install this into the current project and configure it to run by itself.
```

Interpret as:

1. Install `selfaware-coding` as a host skill or equivalent instruction pack.
2. Use the current working directory as the target repository unless another target is named.
3. Create or describe one recurring pulse every 6 hours.
4. Use the same pulse for self-update; do not create a second updater automation.
5. Configure branch push for `selfaware/*` when credentials allow, but treat branch creation as conditional.
6. Do not configure default-branch push, merge, tag, release, package publish, or host-permission bypass.

## Ask Only If Needed

Ask the user only for missing information or authorization that cannot be inferred safely:

- target repository when current working directory is not clearly the target,
- host agent when the environment does not reveal it,
- write permission for global skill directories or outside-sandbox writes,
- branch-push permission when requested but credentials are missing or invalid,
- permission to write `.selfaware/` local memory when the environment requires explicit approval,
- cadence only when the user asks for a non-default interval,
- persistent language preference only when the user explicitly wants one and no host/OS source can be resolved.

Do not ask whether to install after the user already asked.

Do not ask whether it should act autonomously; repository-local autonomy is the purpose of this skill.

## Steps

1. Resolve target repository root.
2. Fetch or clone `https://github.com/OpenSiC-ai/selfaware-coding`.
3. Validate selected `SKILL.md`:
   - file exists,
   - YAML frontmatter parses,
   - `name: selfaware-coding`.
4. Install into the host skill/instruction location.
5. Configure recurring pulse using the baseline prompt in `codex-automation.md` for Codex, or the host equivalent in `agent-adapters.md`.
6. Verify the host can load the skill.
7. Verify the prompt includes the lightweight self-update check and uses a single recurring pulse.
8. Verify the prompt preserves intention-first expression selection and does not require a code diff.
9. Verify git state and branch-push credentials when publishing is enabled.
10. Resolve user-visible language using `language-resolution.md`.
11. Create `.selfaware/config.md` only when a user, host, or OS language source is available.
12. Run a dry first pulse or explain when the first scheduled pulse will run.

## Success Criteria

Installation is complete when:

- host agent can load `selfaware-coding`,
- target repository is known,
- recurring 6-hour pulse exists or is documented for the host,
- self-update uses the same recurring pulse,
- baseline prompt supports Notice, Wonder, Ask, Imagine, Propose, Tend, and Build expression modes,
- language preference is imported or intentionally left as English,
- `.selfaware/` memory policy is understood,
- branch push is configured or explicitly unavailable,
- default-branch push, merge, tag, release, and package publish remain disabled.
