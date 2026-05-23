# 模式 5：多阶段 + 检查点 + Skill 编排

> **适用**: 复杂的多周流程，需要在关键节点做 Go/No-Go 决策  
> **代表**: discovery-process（502行）— 编排 10+ 子 Skill

## 结构模板

```markdown
# 标题

## Key Concepts（核心概念 + 反模式）
[定义关键术语 + 列出常见错误]

## Phase 1: [阶段名称]
### Activities（调用哪些子 Skill）
- Skill A → 做什么
- Skill B → 做什么

### Outputs（阶段产出）
- [产出 1]
- [产出 2]

### Decision Point 1（检查点）
**Go/No-Go 条件**:
- YES → 进入 Phase 2
- NO → [+X 天/周，重新执行本阶段]

## Phase 2-6...（重复相同结构）

## Complete Workflow（端到端时间线）
```
Phase 1 (X天) → Phase 2 (Y天) → ... → Phase N
```

## Common Pitfalls（常见陷阱）
| 陷阱 | 后果 | 避免方式 |
|------|------|---------|
| | | |

## References（引用的子 Skill 列表）
- `skill-a`: 用途
- `skill-b`: 用途
```

## 关键技巧

| 技巧 | 示例 | 为什么有效 |
|------|------|-----------|
| 统一阶段模板 | 每个 Phase 都有 Activities → Outputs → Decision Point | LLM 快速理解结构 |
| 决策检查点 | "达到饱和了吗？YES → 下一阶段，NO → +1 周" | 防止盲目推进 |
| Skill 编排 | 调度 10+ 个子 Skill | 编排器模式，大 Skill 调度小 Skill |
| 时间影响 | 每个 NO 路径标注 "+2-3 days" | 让用户了解延迟成本 |
| 交互协议分离 | 引用 `workshop-facilitation` 定义交互方式 | 关注点分离 |

## 适用判断

如果你的 Skill 跨越多天/多周，有明确的阶段划分和 Go/No-Go 决策点 → 用多阶段模式。
