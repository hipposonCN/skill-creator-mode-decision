# 模式 4：接力棒循环（跨 Session 持久化）

> **适用**: 多次迭代的长期项目，需要跨多个 session 持续工作  
> **代表**: stitch-loop（203行）

## 结构模板

```markdown
# 标题

## Overview（接力棒模式概述）
[一句话解释：文件即状态，跨 session 传递]

## The Baton System（接力棒文件规范）
- `next-prompt.md`: 下一个 session 的启动指令
- `progress.md`: 当前进度
- `decisions.md`: 关键决策记录

## Execution Protocol（6 步执行协议）
### Step 1: Read the Baton（读接力棒）
read next-prompt.md — 获取上下文

### Step 2: Consult Context Files（查阅上下文）
read 相关文件和决策记录

### Step 3: Generate（执行任务）
完成本 session 的工作

### Step 4: Integrate（集成结果）
将产出写入工作目录

### Step 5: Update Documentation（更新文档）
更新 progress.md 和 decisions.md

### Step 6: Prepare the Next Baton ⚠️（写下一个接力棒 — 关键！）
⚠️ CRITICAL: 忘了写接力棒，循环就断了。
写入 next-prompt.md 作为下一个 session 的启动指令。
```

## 关键技巧

| 技巧 | 示例 | 为什么有效 |
|------|------|-----------|
| 文件即状态 | `next-prompt.md` 作为接力棒 | LLM 不需要记住"上次做到哪了" |
| 续命机制 | Step 6 标记为 Critical + MUST | 忘了写接力棒循环就断了 |
| 文件协议 | 每个文件有明确职责 | LLM 只需按协议读写文件 |
| 编排无关 | CI/CD、人在回路、Agent 链都能驱动 | 同一个 Skill 适配多种自动化环境 |

## 与模式 3 的区别

| 维度 | 循环迭代（TDD） | 接力棒循环（Stitch Loop） |
|------|----------------|-------------------------|
| 状态存储 | LLM 对话上下文 | 外部文件系统 |
| 跨 session | ❌ | ✅ |
| 循环退出 | Checklist 全部打勾 | 路线图清空 |
| 适用时长 | 单次会话（分钟~小时） | 长期项目（天~周） |

## 适用判断

如果你的 Skill 需要跨多个 session 持续工作，或者需要多个 Agent 协作 → 用接力棒模式。
