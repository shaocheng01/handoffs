---
name: zhengsc-save
description: Use when the user wants to archive the current task's progress before switching windows or ending a session (zhengsc-save / 归档 / 存档 / 写交接 / archive). Writes the handoff to .handoffs/<today>/.
---

# zhengsc-save · 归档当前任务进度

把当前任务进度存盘，供下次 `/zhengsc-receive` 衔接。**按当天日期建文件夹存放**。用户级 skill，跨所有项目通用；产出文件是项目级。

## 执行步骤

1. 回顾本次对话，**识别任务并起简短任务名**：优先 **kebab-case 英文**（如 `login-refactor`、`dark-mode-toggle`），简短中文亦可（如 `登录重构`）。避免空格、特殊字符、纯标点。
2. 取**今天的日期**（`YYYY-MM-DD`），写入**当前项目根目录**下 `.handoffs/<YYYY-MM-DD>/handoff-<任务名>.md`（目录不存在则创建）。
   - 例：`.handoffs/2026-06-23/handoff-dark-mode-toggle.md`
   - **同一天 + 同一任务名** → 视为同一任务，**更新**当天该文件（不新建）。
   - **不同任务**（同天或跨天）→ 各自文件，互不覆盖。
   - 跨天同一任务再次归档 → 落到新的日期文件夹（衔接时取最新）。
3. 内容按 [`references/handoff-template.md`](references/handoff-template.md) 的结构：目标 / 进度 / 下一步 / 关键决策 / 现状 / 涉及文件 / 坑。
4. 回报：「已归档到 `<项目根>/.handoffs/<YYYY-MM-DD>/handoff-<任务名>.md`」——**带项目根路径与日期**，并简述写了什么。

**只做归档这一件事**：不摘录长期记忆、不改业务代码（除非用户另要求）。长期记忆 / memory 的积累由项目自己的约定处理，本 skill 不涉及。

## 不要踩的坑
- 写到平铺 `.handoffs/handoff-*.md` → 一律写 `.handoffs/<日期>/`
- 任务名太长 / 含特殊字符 → 简短 kebab-case
- 日期文件夹格式 → 统一 `YYYY-MM-DD`

## 配套与跨平台
- 衔接用 `/zhengsc-receive`（另一个 skill）。
- 跨平台：Claude Code 用 `/zhengsc-save`，Codex 用 `$zhengsc-save` 或说 `zhengsc-save`（基于 [agentskills.io](https://agentskills.io) 开放标准）。
