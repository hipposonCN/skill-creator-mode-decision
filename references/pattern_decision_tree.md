# 模式 2：决策树 + 按需加载（渐进式披露）

> **适用**: 大型平台选型、产品导航、问题诊断、知识域有 10+ 分支的场景  
> **代表**: cloudflare-deploy（224行）、cloudflare（211行）

## 结构模板

```markdown
# 标题

## Authentication（认证前置）
[如何获取凭证 / 环境变量]

## Quick Decision Trees（决策树）
### "I need to run code"（按用户意图分类）
  ├─ 边缘无服务器函数 → workers/
  ├─ 容器化部署 → containers/
  └─ ...

### "I need to store data"
  ├─ 关系型 → D1/
  ├─ KV 存储 → KV/
  └─ ...

### "I need AI/ML"
  └─ ...

## Product Index（产品索引表）
| Product | Reference | Description |
|---------|-----------|-------------|
| Workers | references/workers.md | Serverless compute |
| D1 | references/d1.md | SQL database |
```

## 关键技巧

| 技巧 | 示例 | 为什么有效 |
|------|------|-----------|
| 用户意图分类 | "I need to run code" 而非 "Compute products" | 用用户语言而非技术术语 |
| 树形导航 | ├─ 分支结构 | LLM 快速定位正确产品 |
| 渐进式披露 | 主文件 <5K，references/ 按需展开 | 不浪费上下文窗口 |
| 产品索引表 | Product → Reference 的映射表 | 结构化的快速查找 |

## Token 预算设计

```
主文件 SKILL.md:  <5K tokens（决策树 + 索引）
references/:      每个 1-3K tokens（按需加载 1-2 个）
总占用:           <8K tokens
```

## 进阶：拆分导航型 vs 操作型

同一个知识域可以拆成两个 Skill：
- **导航型**（如 cloudflare）：只做选型，不涉及操作
- **操作型**（如 cloudflare-deploy）：包含认证、命令、故障排除

## 适用判断

如果你的 Skill 覆盖的知识域有 10+ 个分支，且每个分支都有大量详细文档 → 用决策树模式。
