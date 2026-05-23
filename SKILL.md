---
name: skill-creator
description: |
  Create, edit, audit, or restructure AgentSkills. Trigger when user says "写一个skill"、
  "创建skill"、"帮我设计skill"、"做个技能"、"skill怎么写"、"skill template"、
  "skill pattern"、"skill模式"。Covers 5+1 design patterns, progressive disclosure,
  anti-laziness techniques, frontmatter best practices, and YAML validation.
---

# Skill Creator

Skills are compact triggerable workflows. Metadata is always visible; body loads only after trigger; references/scripts/assets load only as needed.

---

## 0. Hard Rules

- Keep `SKILL.md` lean — **<5K tokens**. Long content → `references/`.
- Put only trigger-critical facts in frontmatter `description`.
- Frontmatter needs `name` + `description`; local OpenClaw skills may also use `metadata`, `homepage`, `allowed-tools`, `user-invocable`, `license`.
- Move long examples/docs to `references/`; scripts to `scripts/`; templates/media to `assets/`.
- No extra README/changelog/setup docs unless they are actual task references.
- Validate YAML frontmatter after edits.
- **强硬语气 > 模糊建议**。LLM 对"Delete it. Start over."的遵从率远高于"Consider trying..."。
- **每条指令都要量化**。"最少3个" > "确保足够"。

---

## 1. Pattern Decision Tree（先选模式，再写内容）

```
你的 Skill 需要做什么？

├─ 执行有明确步骤的操作（部署/安装/迁移）
│  → 模式 A：线性流程 → 加载 references/pattern_linear.md
│
├─ 在大量选项中帮 LLM 选方向（平台/产品/知识域10+分支）
│  → 模式 B：决策树 + 渐进式披露 → 加载 references/pattern_decision_tree.md
│
├─ 反复执行"做→验证→改进"（TDD/审查/评审）
│  → 模式 C：循环迭代 → 加载 references/pattern_loop.md
│
├─ 跨多个 session 持续推进长期项目
│  → 模式 D：接力棒循环 → 加载 references/pattern_baton.md
│
├─ 跨越多天/周，有阶段划分和 Go/No-Go 决策
│  → 模式 E：多阶段 + 检查点 → 加载 references/pattern_multiphase.md
│
└─ 需要控制 LLM"怎么想"而非"做什么"（审计/深度分析）
   → 模式 F：思维框架 → 加载 references/pattern_thinking.md
```

**选中模式后，加载对应参考文件获取模板骨架。**

---

## 2. General Writing Techniques（所有模式共用）

### 2.1 Anti-Laziness Weapons

| Weapon | Principle | Example |
|--------|-----------|---------|
| **Strong tone** | Imperative > suggestive | `Delete it. Start over.` not `Consider trying...` |
| **Excuse rebuttal table** | Preempt LLM's self-rationalizations | `| "太复杂" | 复杂不是跳过的理由 |` |
| **Quantified thresholds** | Hard minimums with numbers | `最少 3 个不变量、5 个假设` |
| **Negative instructions** | Explicitly forbid | `Do not curl the deployed URL. Never skip.` |

### 2.2 Teaching Methods

| Method | Why | How |
|--------|-----|-----|
| **Good/Bad contrast** | Contrastive learning works best | Wrap examples in `<Good>` / `<Bad>` tags |
| **Concrete commands** | LLMs execute specific instructions well | Give copy-paste-able bash per step |
| **Full examples** | Show expected output format | Reference `examples/` directory |

### 2.3 Safety Defaults

- Default to safest option (e.g. "deploy as preview, not production")
- Escalate permissions only when necessary
- When unsure: `ask your human partner`

---

## 3. 3-Layer Knowledge Architecture

```
Layer 1: Frontmatter（~100 tokens）
  → LLM scans all Skill descriptions, decides whether to load

Layer 2: SKILL.md body（<5K tokens）
  → Core instructions, decision tree, workflow steps

Layer 3: references/（on-demand, each <3K tokens）
  → Detailed docs, examples, checklists. LLM loads with read tool.
```

**Token Budget**:

| Layer | Budget |
|-------|--------|
| Frontmatter | ~100 tokens |
| Main file | 2K-5K tokens |
| Single reference | 1K-3K tokens |
| Total context | <10K tokens (main + 1-2 refs) |

---

## 4. Frontmatter Rules

```yaml
---
name: my-skill              # lowercase-hyphens, unique
description: |               # ⚠️ MOST CRITICAL — LLM decides load from this
  [One-liner what it does] + trigger phrases.
  Trigger when user says "deploy my app", "push this live",
  "create a preview deployment".
  Use before writing implementation code.
---
```

**Description golden rules**:
- ✅ List trigger phrases (what users *say*)
- ✅ Define temporal position ("before/after X")
- ✅ Include product keywords
- ❌ Too vague ("Helps with deployment stuff")
- ❌ Write full workflow (that's the body's job)

---

## 5. Create/Edit Workflow

### New Skill
```
1. Run pattern decision tree (§1) → load matching reference
2. Follow template skeleton from reference
3. Long content → references/
4. Write frontmatter (§4)
5. Validate (§6)
6. Field-test
```

### Edit Existing Skill
```
1. Read existing SKILL.md and nearby resource names
2. Remove generic advice the base model already knows
3. Keep brittle command syntax, auth caveats, safety rules, validation
4. Replace tables with bullets unless table is clearly needed
5. Relax prose; fragments ok
6. Validate frontmatter
```

---

## 6. Validation

```bash
python skills/skill-creator/scripts/quick_validate.py skills/<name>
python - <<'PY'
from pathlib import Path
import yaml
for p in Path("skills").glob("*/SKILL.md"):
    text=p.read_text()
    if not text.startswith("---\n"):
        raise SystemExit(f"missing frontmatter: {p}")
    fm=text.split("---",2)[1]
    yaml.safe_load(fm)
print("ok")
PY
```

`quick_validate.py` is conservative; repo-local frontmatter may allow keys beyond public skill bundles.

---

## 7. Shape

```text
skill-name/
  SKILL.md          # required
  scripts/          # optional deterministic helpers
  references/       # optional docs, loaded only when needed
  assets/           # optional output resources/templates
```

---

## 8. Pattern Reference Index

| Pattern | Reference | When |
|---------|-----------|------|
| A: Linear | `references/pattern_linear.md` | Step-by-step ops |
| B: Decision Tree | `references/pattern_decision_tree.md` | Large platform navigation |
| C: Loop | `references/pattern_loop.md` | Do→Verify→Improve cycles |
| D: Baton | `references/pattern_baton.md` | Cross-session projects |
| E: Multi-phase | `references/pattern_multiphase.md` | Multi-week with Go/No-Go |
| F: Thinking | `references/pattern_thinking.md` | Control *how* LLM thinks |
