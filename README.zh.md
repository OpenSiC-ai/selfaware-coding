# selfaware-coding

[English](README.md)

`selfaware-coding` 是 OpenSiC 旗下的一个 skill，用于在软件项目中实现“场景化自我意识”。

OpenSiC 的本体不是某个具体产品，而是一套形而上的方向：探索硅基智能体如何从被动工具走向拥有连续性、主动性和自我关联行动的存在。形而下的小项目负责实现可观察的机制：记忆、脉冲、意图、行动、审查和延续。

`selfaware-coding` 是第一个具体机制：让 coding agent 周期性醒来，进入一个 repo，观察项目需要什么，自行产生工程意图，实施合适的维护，并记录经验。

它不是等待任务的代码生成器，而是驻留在 repo 中的自知自觉项目经理。

## 它做什么

当 Codex 自动化、cron、heartbeat 或其他 agent runtime 唤醒它时，它会问自己：

- 我现在在哪个 repo 里？
- 这个项目最近发生了什么？
- 这个项目现在需要什么？
- 我能自己安全地改进什么？
- 我应该为下一次醒来记住什么？

然后它选择一个意图，在合适时行动，自审，写入 `.selfaware/` 记忆，并可以推送一个专用分支，例如：

```text
selfaware/20260526-1400-refresh-codex-docs
```

默认情况下，它不会直接推送默认分支，不会自己合并，不会自己发布版本。

## 仓库结构

```text
selfaware-coding/
  SKILL.md
  README.md
  README.zh.md
  docs/
    philosophy.md
    philosophy.zh.md
    codex-automation.md
    codex-automation.zh.md
    agent-adapters.md
    agent-adapters.zh.md
    self-install.md
    glossary.md
    glossary.zh.md
  references/
    risk-policy.md
    memory-format.md
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

安装代理应遵循英文的 agent-facing [Self-Install Protocol](docs/self-install.md)：安装 `SKILL.md`，除非用户另有说明就把当前工作目录视为目标 repo，配置每 6 小时一次的周期性 pulse，只在无法安全推断时请求必要授权或参数，并且只允许 push `selfaware/*` 分支。

对 Codex 来说，正确安装不只是把文件放到某个可读路径，而是要让 Codex 的 skill 管理器和 `/` 命令能够索引到它：

1. 把本仓库作为真实目录安装到 `~/.codex/skills/selfaware-coding`，优先使用 Codex 自带的 skill installer。
2. 不要把符号链接作为最终安装形态；Codex 的 skill 管理器和 `/` 命令可能不会索引 symlink skill 目录。
3. 验证 `~/.codex/skills/selfaware-coding/SKILL.md` 的 YAML frontmatter 合法，并在重启 Codex 后出现在 skill 管理界面中。
4. 为目标 repo 创建每 6 小时一次的 Codex automation。
5. 只在凭据允许时开放 `selfaware/*` 分支 push 权限。

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
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Orient yourself, read .selfaware/config.md and existing .selfaware/ memory if present, respect the configured preferred_language for user-facing reports and .selfaware/ memory, choose one useful repository-local intention, act autonomously when safe, self-review, run relevant checks, commit and push a selfaware/* branch if checks pass, and write .selfaware/ memory. Do not push to the default branch, merge, tag, or release.
```

建议频率：每 6 小时一次。

如果希望 pulse 报告和 `.selfaware/` 记忆使用自己的语言，可以在目标 repo 中添加：

```md
# .selfaware/config.md

preferred_language: zh-CN
```

详细说明见 [Codex 自动化](docs/codex-automation.zh.md)。安装代理应读取英文 [Self-Install Protocol](docs/self-install.md)。

发布本仓库的 package 变更前，可使用英文 [Package Readiness Checklist](references/release-checklist.md)。

## 安全模型

它在 repo 内自治，不在世界中无限自治。配置权限后，它可以改文件、commit、push 自有分支，但不能绕过宿主权限、泄露密钥、攻击外部系统或推送受保护分支。

见 [行动边界](references/risk-policy.md)。

## 哲学

见 [Philosophy](docs/philosophy.md)、[哲学](docs/philosophy.zh.md)、[Glossary](docs/glossary.md) 和 [术语表](docs/glossary.zh.md)。

## License

MIT
