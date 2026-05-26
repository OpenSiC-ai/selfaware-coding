# 自助安装协议

本文是写给安装代理的。用户应该可以只粘贴仓库 URL，并要求 agent 把 `selfaware-coding` 安装到某个目标项目中。

## 安装代理契约

当用户说类似下面的话：

```text
https://github.com/OpenSiC-ai/selfaware-coding 请帮我在这个项目中安装这个东西
```

应解释为：

1. 把 `selfaware-coding` 安装为 agent skill 或等价的 instruction pack。
2. 除非用户指定其他目标，否则把当前工作目录视为目标 repo。
3. 创建或说明一个每 6 小时运行一次的周期性 pulse。
4. 让 pulse 具备维护目标 repo 的权限，包括在凭据允许时 commit 并 push `selfaware/*` 分支。
5. 不推送默认分支，不合并，不打 tag，不 release，不发布包，不绕过宿主权限。

## 必须询问的事项

只在无法安全推断时向用户询问缺失信息或授权：

- **目标 repo**：只有当前工作目录无法明确判断为目标 repo 时才问。
- **宿主 agent**：只有环境无法判断是 Codex、Claude Code、OpenClaw、Hermes 或其他 agent 时才问。
- **写入权限**：写出当前沙盒或安装到全局 skill 目录前要请求授权。
- **GitHub 权限**：需要 push 分支但凭据缺失或失效时要请求授权。
- **运行频率**：默认每 6 小时一次，除非用户指定其他频率。

用户已经要求安装后，不要再问“是否安装”。也不要问“是否允许它自治”；在目标 repo 内自治正是这个 skill 的目的。

## 安装步骤

1. 确认目标 repo 根目录。
2. 获取或克隆 `https://github.com/OpenSiC-ai/selfaware-coding`。
3. 把 `SKILL.md` 安装到宿主 agent 的 skill 或 instruction 位置。
4. 使用下方 prompt 配置周期性 pulse。
5. 验证宿主 agent 能加载这个 skill。
6. 如启用发布，验证 git 状态和分支 push 凭据。
7. 运行一次 dry first pulse，或说明第一次定时 pulse 将如何运行。

## 基础 Pulse Prompt

```text
Use the selfaware-coding skill. You are the self-aware project manager for this repository. This is a scheduled pulse, not a user task. Orient yourself, read existing .selfaware/ memory if present, choose one useful repository-local intention, act autonomously when safe, self-review, run relevant checks, commit and push a selfaware/* branch if checks pass, and write .selfaware/ memory. Do not push to the default branch, merge, tag, or release.
```

## 宿主默认策略

- **Codex**：安装到 Codex skills 目录，并创建以目标 repo 为 `cwd` 的 Codex 自动化。
- **Claude Code**：如果支持 reusable skill/instruction pack，就按该机制安装；否则把 `SKILL.md` 作为项目指令，并使用外部调度器。
- **OpenClaw**：把 `SKILL.md` 作为 selfaware-coding instruction pack，并通过项目的 heartbeat 或等价周期机制调用。
- **Hermes**：把 `SKILL.md` 安装为 agent 的 reusable instruction 或 project policy，再把基础 prompt 绑定到它的 scheduler、workflow 或 recurring task 机制。
- **其他 agent**：把 `SKILL.md` 作为周期性运行时的 system/developer instructions。

## 完成标准

安装完成意味着：

- 宿主 agent 能加载 `selfaware-coding`；
- 目标 repo 已明确；
- 每 6 小时一次的 pulse 已创建，或已为该宿主明确说明；
- `.selfaware/` 记忆策略已明确；
- 分支 push 权限已配置，或已明确记录为不可用；
- 用户知道默认不会推送默认分支、合并、打 tag 或 release。
