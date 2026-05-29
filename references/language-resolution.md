# Language Resolution

Use this before emitting user-visible pulse output or writing `.selfaware/` runtime memory.

## Order

Resolve `preferred_language` in order:

1. `.selfaware/config.md` `preferred_language`.
2. Host agent language setting.
3. Operating system locale.
4. English.

Also record `resolved_language_source` when available.

## Output Scope

Use the resolved language for:

- progress updates,
- visible reasoning summaries,
- final pulse reports,
- `.selfaware/memory.md`,
- `.selfaware/backlog.md`,
- `.selfaware/questions.md`,
- `.selfaware/product-notes.md`,
- `.selfaware/strategy.md`,
- `.selfaware/pulses/*`.

Do not reveal hidden chain-of-thought. Only visible summaries and reports are language-controlled.

## Runtime Memory Language

All generated or updated `.selfaware/*.md` files and `.selfaware/pulses/*.md` pulse logs must use the resolved language from the target repository.

Examples and templates in this package are written in English because reusable agent-facing instructions stay portable. They are not the output language. Translate section headings and prose when writing runtime memory for a repository with a non-English `preferred_language`.

Keep only these literal:

- commands,
- file paths,
- code identifiers,
- API names,
- dependency names,
- branch names,
- commit hashes,
- raw tool output.

## Config Write Rules

Write `.selfaware/config.md` only when:

- the user explicitly sets a language preference, or
- an installation flow imports a host agent language setting, or
- an installation flow imports an operating system locale.

Do not persist a language guessed from the current conversation, README, or repository content.

If no host or OS language is resolved, default to English and do not create `.selfaware/config.md`.

Use this format:

```md
# selfaware config

preferred_language: zh-CN
language_label: 简体中文
language_source: codex.desktop.localeOverride
```

Normalize localized host values when practical:

- `简体中文` -> `preferred_language: zh-CN`, `language_label: 简体中文`
- `English` -> `preferred_language: en-US`, `language_label: English`
- `Español` -> `preferred_language: es-ES`, `language_label: Español`
- `Français` -> `preferred_language: fr-FR`, `language_label: Français`
- `Deutsch` -> `preferred_language: de-DE`, `language_label: Deutsch`

## Host Lookup

Codex Desktop:

- `$CODEX_HOME/config.toml`
- `~/.codex/config.toml`
- `%CODEX_HOME%\config.toml`
- `%USERPROFILE%\.codex\config.toml`
- field: `[desktop].localeOverride`
- source: `codex.desktop.localeOverride`

Claude Code:

- `.claude/settings.local.json`
- `.claude/settings.json`
- `~/.claude/settings.json`
- `%USERPROFILE%\.claude\settings.json`
- field: `language`
- source: `claude.settings.language`

Hermes:

- `$HERMES_CONFIG_PATH`
- `~/.hermes/config.yaml`
- `%USERPROFILE%\.hermes\config.yaml`
- env: `HERMES_LANGUAGE`
- field: `display.language`
- source: `hermes.display.language` or `hermes.env.HERMES_LANGUAGE`

OpenClaw:

- `$OPENCLAW_CONFIG_PATH`
- `~/.openclaw/openclaw.json`
- `~/.openclaw/openclaw.yaml`
- `%USERPROFILE%\.openclaw\openclaw.json`
- `%USERPROFILE%\.openclaw\openclaw.yaml`
- fields: `agents.defaults.language`, `agents.*.language`
- source: `openclaw.agent.language`

OpenCode:

- `~/.config/opencode/opencode.json`
- `~/.config/opencode/tui.json`
- `%XDG_CONFIG_HOME%\opencode\...`
- `%APPDATA%\opencode\...`
- `%USERPROFILE%\.config\opencode\...`
- if no clear field exists, continue to OS locale.

OS locale:

- macOS: `AppleLocale`, `AppleLanguages`
- Linux: `LC_ALL`, `LC_MESSAGES`, `LANG`, `locale`
- Windows: `Get-Culture`, `Get-UICulture`
- source: `os.locale`

## Do Not Translate

Keep these literal:

- commands,
- file paths,
- code identifiers,
- API names,
- dependency names,
- branch names,
- commit hashes,
- raw tool output.

Summarize or explain literal values in the resolved language when useful.
