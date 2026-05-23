# 特殊模式：思维框架

> **适用**: 安全审计、代码审查、架构分析等需要深度思考的场景  
> **代表**: audit-context-building（302行）  
> **核心**: 控制 LLM "怎么想"，而非"做什么"

## 结构模板

```markdown
# 标题

## Purpose（定位）
This skill controls HOW you think, not WHAT you do.
[控制思维方式，不是控制行为]

## When to Use / When NOT to Use
- ✅ 使用场景
- ❌ 不使用场景

## Rationalizations（借口反驳表）
| Excuse | Reality |
|--------|---------|
| "[借口]" | "[反驳]" |

## Phase 1: Initial Orientation（定向扫描）
[快速全局扫描，建立心智模型]

## Phase 2: [深度分析阶段]（核心）
### Per-[Unit] Checklist（逐单元分析清单）
- [ ] 项目 1
- [ ] 项目 2

### Cross-[Unit] Analysis（跨单元追踪）
[追踪数据/逻辑的跨模块流动]

### Output Requirements（输出格式 + 量化阈值）
- 每个 [单元] 最少 [X] 个 [Y]（量化！）
- 输出格式：[模板]

### Completeness Checklist（完整性检查）

## Phase 3: Global Understanding（全局理解）
[汇总发现，建立全局视图]

## Stability Rules（反幻觉规则）
- Never reshape evidence to fit earlier assumptions
- [其他反幻觉规则]

## Non-Goals（明确禁止做的事）
- ❌ [不要做的事 1]
- ❌ [不要做的事 2]
```

## 关键技巧

| 技巧 | 示例 | 为什么有效 |
|------|------|-----------|
| 思维工具 | 第一性原理、5 Why、5 How | 给 LLM 分析框架而非具体命令 |
| 量化阈值 | "每个函数最少 3 个不变量、5 个假设" | 强制 LLM 达到足够的分析深度 |
| 非目标约束 | "不要识别漏洞、不要提出修复" | 克制 LLM 最想做的事，先理解再判断 |
| 反幻觉规则 | "Never reshape evidence to fit earlier assumptions" | 防止 LLM 自我欺骗 |
| 子 Agent 指导 | 何时及如何使用子 Agent | 分而治之 |

## 与模式 1-5 的本质区别

| 模式 1-5 | 思维框架 |
|---------|---------|
| 控制"做什么" | 控制"怎么想" |
| 流程导向 | 认知导向 |
| 正确性在步骤 | 正确性在推理质量 |

## 适用判断

如果你的 Skill 需要 LLM 进行**深度分析**而非快速执行，需要控制的是**思维质量**而非操作步骤 → 用思维框架模式。
