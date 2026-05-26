# Agent 适配

`selfaware-coding` 被设计为可迁移的通用 skill。只要一个 agent 能加载指令、检查 repo、编辑文件、运行检查、使用 git、持久化记忆，就可以使用它。

## 通用宿主契约

宿主 agent 应提供：

- 以目标 repo 根目录作为工作目录；
- repo 内读写权限；
- 可运行本地检查的 shell；
- 如启用发布，则提供 git 分支、commit、push 权限；
- cron、automation、heartbeat、scheduler 等周期性触发机制。

宿主不应授予超过需要的权限。v0.1 只需要 push 分支权限。

## Claude Code

把 `SKILL.md` 安装或粘贴为项目级指令。用外部调度器打开目标 repo，并运行与 `docs/codex-automation.md` 中 Codex prompt 等价的唤醒 prompt。

## OpenCode 或其他 Agent

把 `SKILL.md` 放在该 agent 识别 reusable skills 或 instruction packs 的位置。唤醒 prompt 中明确要求使用 `selfaware-coding` 行为。

## 没有原生 Skill 支持

如果 agent 没有 skill 系统，就把 `SKILL.md` 当作定时运行时的 system/developer instruction。周期性 prompt 保持简短，让 skill 定义具体行为。
