# 模式 1：线性流程

> **适用**: 部署、安装、迁移等有明确步骤的操作  
> **代表**: vercel-deploy（77行） — 最小但完整的 Skill 模板

## 结构模板

```markdown
# 标题

[一句话核心原则 + 安全默认值]

## Prerequisites（前置条件）
- [前置条件 1]
- [前置条件 2]

## Quick Start（主流程）
### Step 1: [动作]
```bash
[具体命令]
```

### Step 2: [动作]
[具体指令]

### Step 3: [动作]
[具体指令]

## Fallback（降级方案）
[主流程失败时的 B 计划]

## Troubleshooting（故障排除）
| Issue | Solution |
|-------|----------|
| [问题 1] | [解决方案] |
```

## 关键技巧

| 技巧 | 示例 | 为什么有效 |
|------|------|-----------|
| 安全默认值 | "Always deploy as preview, not production" | 防止 LLM 做出危险操作 |
| 具体命令 | 每步给出可直接执行的 bash 命令 | LLM 不需要猜测 |
| 超时提示 | "Use a 10 minute (600000ms) timeout" | 防止 LLM 因超时中断 |
| 降级方案 | CLI 失败有 Fallback 脚本 | 提供 B 计划 |
| 负面指令 | "Do not curl the deployed URL to verify" | 明确禁止不该做的事 |

## 适用判断

如果你的 Skill 可以用"先做 A，再做 B，最后做 C"描述 → 用线性模式。
