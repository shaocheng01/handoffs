---
name: zhengsc-receive
description: Use when the user wants to resume an unfinished task from a previous session (zhengsc-receive / 继续 / 衔接 / 接续 / continue). Reads the latest handoff from .handoffs/, or a specific one by task name or path.
---

# zhengsc-receive · 衔接恢复任务

从归档恢复上下文，继续执行剩余操作。归档按日期文件夹组织，衔接**递归扫描取最新**，支持按任务名或完整路径指定。用户级 skill，跨所有项目通用。

## 执行步骤

1. 找到并确认 handoff 文件（按用户输入判断指定方式）：
   - **指定完整路径**：用户输入含 `/` 或 `.md`（例：`/zhengsc-receive .handoffs/2026-06-23/handoff-xxx.md`）→ **直接读该路径**（路径相对当前项目根）。文件不存在则如实告知，不要编造。
   - **指定任务名**：用户输入是不含 `/` 的简短名（例：`/zhengsc-receive login-refactor`）→ 在 `.handoffs/` 下找 `handoff-<任务名>.md`，取**修改时间最新**的。
   - **默认**：无指定 → 扫描 `.handoffs/**/*.md`，按**文件修改时间（mtime）最新**取一个。
   - **扫描范围**：当前项目 `.handoffs/**/*.md`（递归所有日期文件夹）。**只认这个位置**，不扫描平铺的 `.handoffs/handoff-*.md`。
   - **无文件**：`.handoffs/` 下没有任何 handoff（且用户没给有效路径）→ **如实告知无归档可衔接，不要编造进度**。
   - **核对任务**：读到后核对它是否就是用户要接的任务。若内容与用户当前所述任务无关（例：用户想接暗色模式，最新归档却是支付 API），**先复述找到的内容并向用户确认**，不要假设它就是目标任务，更不要把它的进度当成当前任务的进度。
2. 读取后**先复述关键上下文**给用户：目标 / 当前进度 / 关键决策 / 坑。
3. 明确 handoff 里的「下一步」，从那里继续执行剩余操作。
4. 推进后可再次 `/zhengsc-save` 归档更新进度。

## 不要踩的坑
- 找不到归档就编造进度 → 无文件则如实告知
- 读到无关归档当成当前任务 → 先复述确认
- 不复述就闷头干 → 先复述目标 / 进度 / 下一步

## 配套与跨平台
- 归档用 `/zhengsc-save`（另一个 skill）。
- 跨平台：Claude Code 用 `/zhengsc-receive`，Codex 用 `$zhengsc-receive` 或说 `zhengsc-receive`（基于 [agentskills.io](https://agentskills.io) 开放标准）。带路径/任务名时，斜杠后的输入会作为指定传给 skill。
