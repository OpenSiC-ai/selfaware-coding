# Memory Format

`selfaware-coding` stores memory in `.selfaware/` inside the target repository.

`.selfaware/` is local runtime state by default and should normally be ignored by git. Version documentation, templates, or examples instead. If `selfaware-coding` is maintaining its own repository, the same rule applies: keep the live `.selfaware/` directory local unless the project explicitly decides to publish that memory.

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

User-controlled preferences for future pulses. Keep it short, readable, and easy for any agent to parse.

Suggested format:

```md
# selfaware config

preferred_language: zh-CN
```

`preferred_language` controls user-facing pulse reports and `.selfaware/` memory files. It may be a BCP 47 tag such as `zh-CN`, `en-US`, or `ja-JP`, or a plain language name such as `Chinese`. If absent, the agent should infer the language from the latest user request, existing `.selfaware/` files, README language, or dominant project documentation.

Branch names, commit prefixes, commands, API names, and code identifiers should remain tool-friendly and may stay in ASCII English even when the preferred language is not English.

## memory.md

Long-term project manager memory. Keep it concise and useful.

Suggested sections:

```md
# selfaware memory

## Project understanding

## Stable preferences

## Risk notes

## Repeated observations

## Useful commands
```

## backlog.md

Ideas that were not acted on yet.

Suggested item format:

```md
- [ ] 2026-05-26: Standardize test setup. Reason: no CI was detected during pulse 2026-05-26-1400. Risk: medium.
```

## Pulse Log

Each pulse writes one file under `.selfaware/pulses/`.

Template:

```md
# Pulse YYYY-MM-DD HH:MM

## Awakening

- Trigger: scheduled pulse
- Agent: selfaware-coding
- Repository:

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

Do not store secrets, tokens, private raw conversations, or full sensitive logs. Store summaries that help future maintenance.
