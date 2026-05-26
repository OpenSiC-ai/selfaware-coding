# Memory Format

Use `.selfaware/` in the target repository for local runtime memory.

Default policy: do not commit `.selfaware/` unless the target repository explicitly versions it.

## Directory

```text
.selfaware/
  config.md
  memory.md
  backlog.md
  pulses/
    YYYY-MM-DD-HHMM.md
```

## config.md

Purpose: user or installer preferences for future pulses.

Language fields are defined by `language-resolution.md`.

Minimal format:

```md
# selfaware config

preferred_language: zh-CN
language_label: 简体中文
language_source: user
```

Do not create `config.md` only from an LLM guess.

## memory.md

Purpose: stable project-manager memory.

Keep concise. Store durable observations, not diaries.

Suggested sections:

```md
# selfaware memory

## Project understanding

## Stable preferences

## Risk notes

## Repeated observations

## Useful commands
```

Update when a pulse learns something likely to matter in future pulses.

## backlog.md

Purpose: deferred intentions.

Item format:

```md
- [ ] YYYY-MM-DD: <idea>. Reason: <why it matters>. Risk: <low|medium|high>.
```

Use backlog when:

- the idea is useful but not chosen,
- the idea is too broad for this pulse,
- action is blocked by risk or dirty state,
- user attention is needed.

## Pulse Log

Write one file per pulse under `.selfaware/pulses/`.

Filename:

```text
YYYY-MM-DD-HHMM.md
```

Template:

```md
# Pulse YYYY-MM-DD HH:MM

## Awakening

- Trigger:
- Agent: selfaware-coding
- Repository:
- Language:

## Orientation

## Intentions considered

1.
2.
3.

## Chosen intention

## Actions taken

## Self-review

## Checks

## Branch and commit

## Memory updates

## Next continuation
```

## Privacy

Never store:

- secrets,
- tokens,
- private raw conversations,
- full sensitive logs,
- credentials,
- unnecessary personal data.

Store summaries sufficient for future maintenance.
