# handoffs

Claude Code/Codex 任务交接 skill —— 跨会话 / 跨窗口存档与恢复任务进度，预防上下文撑爆导致任务无法衔接问题。基于 [agentskills.io](https://agentskills.io) 开放标准。

## 包含

- **zhengsc-save** — 归档当前任务进度到 `.handoffs/<date>/`
- **zhengsc-receive** — 从最新归档衔接恢复任务

## 安装

把 `zhengsc-save` 和 `zhengsc-receive` 两个目录复制到 `~/.claude/skills/`：

```bash
cp -r zhengsc-save zhengsc-receive ~/.claude/skills/
```

## 用法

- `/zhengsc-save` —— 存档当前任务（也可说「归档」「存档」「写交接」）
- `/zhengsc-receive` —— 恢复任务（也可说「继续」「衔接」「接续」）

归档按 `.handoffs/<YYYY-MM-DD>/handoff-<任务名>.md` 组织，衔接时递归扫描取最新。

## 跨平台

Claude Code 用 `/zhengsc-save` / `/zhengsc-receive`；Codex 用 `$zhengsc-save` / `$zhengsc-receive` 或直接说名字。
