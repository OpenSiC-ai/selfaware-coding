# Agent 适配

`selfaware-coding` 被设计为可迁移的通用 skill。只要一个 agent 能加载指令、检查 repo、编辑文件、运行检查、使用 git、持久化记忆，就可以使用它。

如果用户只提供仓库 URL 并要求安装，按 [自助安装协议](self-install.zh.md) 执行。

## 通用宿主契约

宿主 agent 应提供：

- 以目标 repo 根目录作为工作目录；
- repo 内读写权限；
- 可运行本地检查的 shell；
- 如启用发布，则提供 git 分支、commit、push 权限；
- cron、automation、heartbeat、scheduler 等周期性触发机制。

宿主不应授予超过需要的权限。v0.1 只需要 push 分支权限。

## Codex

把 `SKILL.md` 安装到 Codex skills 目录，然后创建以目标 repo 为工作目录的 Codex 自动化。使用 `docs/codex-automation.zh.md` 中的基础 prompt，并设置 6 小时频率。

如果创建自动化或写入 skills 目录需要权限，直接向用户请求该权限，获得批准后继续。

## Claude Code

把 `SKILL.md` 安装或粘贴为项目级指令。如果 Claude Code 有 reusable skill 机制，就使用该机制。否则把 instruction pack 加入目标项目，并用外部调度器打开目标 repo，运行基础 pulse prompt。

如果项目级指令文件或全局 Claude 配置需要写入权限，应向用户请求授权。

## OpenClaw

把 `SKILL.md` 安装为目标 OpenClaw 项目可用的 instruction pack。配置 `HEARTBEAT.md` 或等价 heartbeat 机制，每 6 小时调用基础 pulse prompt。

如果 OpenClaw 需要项目特定路径、账号或 heartbeat 位置，应向用户询问该参数。不要在无法发现时猜测当前项目之外的路径。

## Hermes

把 `SKILL.md` 安装为 Hermes agent 的 reusable instruction、project policy 或 workflow instruction pack。把基础 pulse prompt 绑定到 Hermes 的 scheduler、workflow 或 recurring task 机制，并设置 6 小时频率。

如果 Hermes 安装中存在多个 workspace、project 或 deployment target，应询问用户把 selfaware-coding 安装到哪个目标。

## OpenCode 或其他 Agent

把 `SKILL.md` 放在该 agent 识别 reusable skills 或 instruction packs 的位置。唤醒 prompt 中明确要求使用 `selfaware-coding` 行为。

## 没有原生 Skill 支持

如果 agent 没有 skill 系统，就把 `SKILL.md` 当作定时运行时的 system/developer instruction。周期性 prompt 保持简短，让 skill 定义具体行为。
