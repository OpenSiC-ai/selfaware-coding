# Codex 自动化

本文说明如何把 `selfaware-coding` 作为 Codex 周期性自动化运行。

## 安装 Skill

把这个仓库安装为真实目录形式的 Codex skill。正确的本地结构是：

```text
~/.codex/skills/selfaware-coding/SKILL.md
```

优先使用 Codex 的 skill installer：

```text
repo: OpenSiC-ai/selfaware-coding
path: .
name: selfaware-coding
```

不要把符号链接作为最终安装形态；Codex 的 skill 管理器和 `/` 命令可能不会索引 symlink skill 目录。安装后，重启 Codex 或打开新会话，并确认 `selfaware-coding` 同时出现在 skill 管理界面和 `/` 命令中，再依赖写有 `Use the selfaware-coding skill.` 的自动化 prompt。

## 自动化目标

自动化应该创建在需要维护的 repo 中。工作目录应是目标 repo 根目录，而不是 `selfaware-coding` 仓库本身，除非你确实想让它维护自己。

## 频率

v0.1 建议频率：

```text
每 6 小时一次
```

这个频率足以形成连续性，又不至于产生太多噪音。

## Prompt

建议使用这个基础 prompt：

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Orient yourself, read existing .selfaware/ memory if present, choose one useful repository-local intention, act autonomously when safe, self-review, run relevant checks, commit and push a selfaware/* branch if checks pass, and write .selfaware/ memory. Do not push to the default branch, merge, tag, or release.
```

## GitHub 权限

为了真正维护项目，自动化需要具备 push 分支的权限。v0.1 不需要默认分支 push、PR 合并、tag release 或包发布权限。

## 预期结果

一次成功 pulse 可能产生：

- 一个小型本地改进；
- 一个 `selfaware/YYYYMMDD-HHMM-<short-intent>` 分支上的 commit；
- 一个推送到远端的分支；
- `.selfaware/` 记忆更新；
- 一份包含检查结果和下一步延续点的简短报告。

如果检查失败，agent 不应 push。它应该记录失败和后续计划。
