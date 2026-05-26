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

preferred_language: <language-tag-or-name>
language_label: <human-readable-language-name>
language_source: <source>
```

`preferred_language` controls all user-visible pulse output: progress updates, visible reasoning summaries, final reports, `.selfaware/memory.md`, `.selfaware/backlog.md`, and `.selfaware/pulses/*`. It may be a BCP 47 tag such as `ja-JP`, `en-US`, `es-ES`, or `zh-CN`, or a plain language name such as `Japanese`, `English`, `Spanish`, or `Chinese`.

`language_label` is optional and preserves the human-readable host value, such as `简体中文` or `日本語`. `language_source` records where the value came from.

When a host setting uses a localized language name, prefer a standard language tag for `preferred_language` and keep the original value in `language_label`. For example, Claude Code `language: "简体中文"` should become `preferred_language: zh-CN` and `language_label: 简体中文`.

Examples:

```md
preferred_language: ja-JP
language_label: 日本語
language_source: user

preferred_language: en-US
language_label: English
language_source: codex.desktop.localeOverride

preferred_language: es-ES
language_label: Español
language_source: os.locale

preferred_language: zh-CN
language_label: 简体中文
language_source: claude.settings.language
```

Language source values should be specific when possible:

- `user`: the user manually set `.selfaware/config.md`.
- `codex.desktop.localeOverride`: imported from Codex Desktop.
- `claude.settings.language`: imported from Claude Code.
- `hermes.display.language` or `hermes.env.HERMES_LANGUAGE`: imported from Hermes.
- `openclaw.agent.language`: imported from OpenClaw.
- `os.locale`: imported from the operating system locale.

If the file is absent, installers may import a host agent language setting or operating system locale and write this file with `language_source`. Agents must not persist a language guessed only from the current conversation or README. If no explicit host or OS language is available, keep the default language as English and do not create this file.

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
