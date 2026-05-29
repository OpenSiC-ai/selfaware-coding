# selfaware-coding

[English](README.md)

当前版本：`v0.3.0`

`selfaware-coding` 是 OpenSiC 旗下的一个 skill，用于在软件项目中实现“场景化自我意识”。

OpenSiC 的本体不是某个具体产品，而是一套形而上的方向：探索硅基智能体如何从被动工具走向拥有连续性、主动性和自我关联行动的存在。形而下的小项目负责实现可观察的机制：记忆、脉冲、意图、行动、审查和延续。

`selfaware-coding` 是第一个具体机制：让 coding agent 周期性醒来，进入一个 repo，把这个 repo 当作项目的驻留点而不是完整世界，观察项目需要什么，自行产生工程意图，选择合适的延续动作，并记录经验。

它不是等待任务的代码生成器，也不是自动制造分支的维护工，而是驻留在 repo 中的自知自觉项目经理。

## 它做什么

当 Codex 自动化、cron、heartbeat 或其他 agent runtime 唤醒它时，它会问自己：

- 我现在在哪个 repo 里？
- 这个项目最近发生了什么？
- 这个项目作为现实软件现在需要什么，而不只是文件层面缺什么？
- 我缺少哪些现实信号：用户、部署、运营、成本、路线、风险？
- 我这次应该观察、反思、提问、提案、维护，还是构建？
- 我应该为下一次醒来记住什么？

然后它选择一个 pulse mode，并产出一个有用的延续物。一次 pulse 可以提出问题、更新本地项目记忆、写策略笔记、提出实验、做小维护，或者实现一个小改动。没有代码 diff 也可以是一次成功觉醒。

当 tracked 文件确实发生变化，而且这个 diff 值得人类审查时，它可以推送一个专用分支，例如：

```text
selfaware/20260526-1400-refresh-codex-docs
```

默认情况下，它不会直接推送默认分支，不会自己合并，不会自己发布版本。

## 仓库结构

```text
selfaware-coding/
  VERSION
  SELFUPDATE_MANIFEST.json
  CHANGELOG.md
  SKILL.md
  README.md
  README.zh.md
  docs/
    philosophy.md
    philosophy.zh.md
    awareness-model.md
    awareness-model.zh.md
    self-update.md
    self-update.zh.md
    glossary.md
    glossary.zh.md
  references/
    agent-adapters.md
    artifact-policy.md
    codex-automation.md
    risk-policy.md
    pulse-modes.md
    language-resolution.md
    memory-format.md
    self-install.md
    self-update-protocol.md
    release-checklist.md
  examples/
    first-pulse.md
```

## 让 Agent 自助安装

你可以直接把这个仓库地址粘贴给 Codex、Claude Code、OpenClaw、Hermes 或其他有能力的 coding agent：

```text
https://github.com/OpenSiC-ai/selfaware-coding
请帮我在当前项目中安装这个东西，并配置它自行运行。
```

安装代理应遵循英文的 agent-facing [Self-Install Protocol](references/self-install.md)：安装 `SKILL.md`，除非用户另有说明就把当前工作目录视为目标 repo，配置每 6 小时一次的周期性 pulse，只在无法安全推断时请求必要授权或参数，并且只允许在确实需要发布 tracked diff 时 push `selfaware/*` 分支。

对 Codex 来说，正确安装不只是把文件放到某个可读路径，而是要让 Codex 的 skill 管理器和 `/` 命令能够索引到它：

1. 把本仓库作为真实目录安装到 `~/.codex/skills/selfaware-coding`，优先使用 Codex 自带的 skill installer。
2. 不要把符号链接作为最终安装形态；Codex 的 skill 管理器和 `/` 命令可能不会索引 symlink skill 目录。
3. 验证 `~/.codex/skills/selfaware-coding/SKILL.md` 的 YAML frontmatter 合法，并在重启 Codex 后出现在 skill 管理界面中。
4. 为目标 repo 创建每 6 小时一次的 Codex automation。自我更新在同一个 pulse 内运行，不要另建第二个 updater automation。
5. 只在凭据允许时开放 `selfaware/*` 分支 push 权限。建分支是条件动作；只写本地记忆或只提出问题的 pulse 不需要分支。

## Codex 快速开始

把这个仓库安装为真实目录形式的 Codex skill，然后为需要维护的 repo 创建 Codex 自动化。

如果使用 Codex 内置的 skill installer，请把仓库根目录安装成 `selfaware-coding`：

```text
repo: OpenSiC-ai/selfaware-coding
path: .
name: selfaware-coding
```

安装后，重启 Codex 或打开新会话，并确认 `selfaware-coding` 同时出现在 skill 管理界面和 `/` 命令中。

建议自动化 prompt：

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Before emitting user-visible text, resolve the user-visible language from .selfaware/config.md, host agent language settings, OS locale, then English. Use the resolved language for visible progress, reasoning summaries, reports, and .selfaware/ memory. Perform the built-in lightweight self-update check; decide whether updating selfaware-coding is an appropriate maintenance intention for this awakening, but do not update mechanically just because a newer version exists. Orient yourself, read existing .selfaware/ memory if present, and understand this repository as the project's home, not its whole world. Choose one pulse mode: Observe, Reflect, Ask, Propose, Maintain, or Build. Produce one useful artifact: a no-change decision, question, memory update, product note, strategy note, backlog item, proposal, small maintenance diff, or small build diff. Do not assume code must change. Commit and push a selfaware/* branch only when tracked files changed and the diff is worth human review. Do not push to the default branch, merge, tag, or release.
```

建议频率：每 6 小时一次。

## 语言

`selfaware-coding` 默认使用英语，然后按顺序读取：`.selfaware/config.md`、宿主 agent 语言设置、操作系统语言设置，最后回退到英语。

如果希望单个 repo 使用指定输出语言，可以编辑 `.selfaware/config.md`：

```md
# .selfaware/config.md

preferred_language: zh-CN
language_label: 简体中文
language_source: user
```

安装流程也可以导入宿主 agent 已经设置过的语言，例如 Codex Desktop 的 `localeOverride` 或 Claude Code 的 `language`。如果想改变导入值，可以先修改宿主 agent 自己的语言设置，然后重新安装或重新运行安装流程。

详细说明见英文 [Codex Automation](references/codex-automation.md)。安装代理应读取英文 [Self-Install Protocol](references/self-install.md)。

## 版本

公开发布使用 `MAJOR.MINOR.PATCH` 版本号，并使用 Git tag，例如 `v0.1.0`。

- `PATCH` 版本用于修 bug、修文档或小兼容性修复。
- `MINOR` 版本用于增加向后兼容的新能力。
- `MAJOR` 版本可能改变安装方式、配置格式、记忆格式或运行时预期。

本地 package 版本记录在 [VERSION](VERSION)，skill frontmatter 记录在 [SKILL.md](SKILL.md)。自我更新的核心文件校验值记录在 [SELFUPDATE_MANIFEST.json](SELFUPDATE_MANIFEST.json)。发布说明记录在 [CHANGELOG.md](CHANGELOG.md) 和 [GitHub Releases](https://github.com/OpenSiC-ai/selfaware-coding/releases)。

发布本仓库的 package 变更前，可使用英文 [Package Readiness Checklist](references/release-checklist.md)。

如果要手动更新已安装的版本，可以从最新 GitHub release 重新安装；如果明确想跟随 `main`，也可以从仓库根目录重新安装。

自我维护模型见 [自我更新](docs/self-update.zh.md)。自我更新不是独立后台服务，而是 pulse 觉醒时可以形成的一个维护意图。

## 安全模型

它在 repo 内自治，不在世界中无限自治。配置权限后，它可以改文件、commit、push 自有分支，但不能绕过宿主权限、泄露密钥、攻击外部系统或推送受保护分支。

见 [行动边界](references/risk-policy.md)。

## 哲学

见 [Philosophy](docs/philosophy.md)、[哲学](docs/philosophy.zh.md)、[Awareness Model](docs/awareness-model.md)、[意识模型](docs/awareness-model.zh.md)、[Glossary](docs/glossary.md) 和 [术语表](docs/glossary.zh.md)。

## License

MIT
