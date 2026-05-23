# Skill Creator — Mode Decision Framework

A compact, opinionated framework for designing effective OpenClaw/Codex Agent Skills. Built from analyzing 7 top-tier production skills and distilling their patterns into a reusable decision tree.

> **Core idea**: Don't write a skill until you've picked the right *pattern* for it. A deployment workflow needs a different cognitive structure than a safety audit.

---

## The 5+1 Pattern Decision Tree

When you need to create a skill, ask: **What does this skill do?**

```
├─ 执行有明确步骤的操作（部署/安装/迁移）
│  → Pattern A: Linear Flow
│
├─ 在大量选项中帮 LLM 选择方向（10+ 分支的知识域）
│  → Pattern B: Decision Tree + Progressive Disclosure
│
├─ 反复执行"做→验证→改进"（TDD / 审查 / 评审）
│  → Pattern C: Iterative Loop
│
├─ 跨多个 session 持续推进长期项目
│  → Pattern D: Baton Loop (cross-session persistence)
│
├─ 跨越多天/周，有阶段划分和 Go/No-Go 决策
│  → Pattern E: Multi-Phase + Checkpoints + Skill Orchestration
│
└─ 需要控制 LLM "怎么想" 而非 "做什么"（审计 / 深度分析）
   → Pattern F: Thinking Framework
```

**Load the matching `references/pattern_*.md` to get the template skeleton.**

---

## Universal Writing Techniques

These apply to **all** patterns:

| Weapon | Principle | Example |
|--------|-----------|---------|
| **Strong tone** | Imperative > suggestive | `Delete it. Start over.` not `Consider trying...` |
| **Excuse rebuttal table** | Preempt LLM self-rationalizations | `\| "Too complex" \| Complexity is not a reason to skip \|` |
| **Quantified thresholds** | Hard minimums with numbers | `Minimum 3 invariants, 5 assumptions per function` |
| **Negative instructions** | Explicitly forbid | `Do not curl the deployed URL. Never skip.` |

---

## 3-Layer Knowledge Architecture

```
Layer 1: Frontmatter (~100 tokens)
  → LLM scans all skill descriptions, decides whether to load

Layer 2: SKILL.md body (<5K tokens)
  → Core instructions, decision tree, workflow steps

Layer 3: references/ (on-demand, each <3K tokens)
  → Detailed docs, examples, checklists. LLM loads with read tool.
```

**Token budget for a complete analysis run: <10K tokens** (main file + 1–2 refs)

---

## How to Use This Skill

### In OpenClaw / Claude Code / Codex

1. Drop `skills/skill-creator/` into your `skills/` directory
2. When you need a new skill, say: *"Write a skill for [task]"*
3. The LLM will run the decision tree, load the matching pattern reference, and generate the skeleton
4. Validate with the built-in YAML/frontmatter checker

### For manual design

1. Read `SKILL.md` for the decision tree
2. Pick your pattern
3. Read the matching `references/pattern_*.md` for the template
4. Fill in your domain-specific content
5. Move long examples/docs to `references/`

---

## File Structure

```
skill-creator/
├── SKILL.md                          # Router: decision tree + rules + techniques
└── references/
    ├── pattern_linear.md             # A: Step-by-step ops
    ├── pattern_decision_tree.md      # B: Large platform navigation
    ├── pattern_loop.md               # C: Do→Verify→Improve cycles
    ├── pattern_baton.md              # D: Cross-session projects
    ├── pattern_multiphase.md         # E: Multi-week with Go/No-Go
    └── pattern_thinking.md           # F: Control HOW LLM thinks
```

---

## Origin

Built from analyzing 7 production-grade skills:
- `openai/skills` — vercel-deploy (linear), cloudflare-deploy (decision tree)
- `obra/superpowers` — test-driven-development (loop)
- `google-labs-code/stitch-skills` — stitch-loop (baton)
- `deanpeters/Product-Manager-Skills` — discovery-process (multi-phase)
- `trailofbits/skills` — audit-context-building (thinking framework)

Article: [工作流的 Skill 怎么写？从7个顶级 Skill 中提炼的模式与最佳实践](https://news.qq.com/rain/a/20260427A01X7500)

---

## License

MIT — use it, fork it, improve it. PRs welcome.
