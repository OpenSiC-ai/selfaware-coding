# Memory Format

Use `.selfaware/` in the target repository for local runtime memory.

Default policy: do not commit `.selfaware/` unless the target repository explicitly versions it.

## Directory

```text
.selfaware/
  config.md
  memory.md
  backlog.md
  questions.md
  product-notes.md
  strategy.md
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

## Reality signals

## Open questions

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

## questions.md

Purpose: decision-changing questions for the human.

Use when the pulse lacks reality signals that would change the right next move.

Suggested format:

```md
# selfaware questions

## Open

- [ ] YYYY-MM-DD: <specific question>. Why it matters: <decision this unlocks>.

## Answered

- [x] YYYY-MM-DD: <question>. Answer: <concise answer>. Impact: <what changed>.
```

Questions should be few and specific. Do not use this file as a generic survey.

## product-notes.md

Purpose: observations about the project as software in the world.

Useful sections:

```md
# product notes

## Users and workflows

## Deployment and operations

## Adoption signals

## Costs and constraints

## Product hypotheses
```

Store hypotheses as hypotheses. Do not present guesses as facts.

## strategy.md

Purpose: durable direction, tradeoffs, and proposed next moves.

Useful sections:

```md
# strategy

## Current thesis

## Near-term bets

## Rejected paths

## Experiments

## Decisions needed
```

Keep this concise. Link back to tracked docs when a strategy becomes public project direction.

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

## Pulse mode

## Chosen intention

## Artifact produced

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
