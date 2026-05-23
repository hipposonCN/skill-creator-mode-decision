---
name: skill-creator
description: |
  Create, edit, audit, or restructure AgentSkills. Trigger when user says
  "write a skill", "create a skill", "help me design a skill", "skill pattern",
  "skill template", "skill mode", "skill framework". Covers 5+1 design patterns,
  progressive disclosure, anti-laziness techniques, frontmatter best practices,
  and YAML validation.
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
- **Strong tone > weak suggestions**. LLMs comply with "Delete it. Start over." far more than "Consider trying...".
- **Every instruction must be quantified**. "Minimum 3" > "ensure enough".

---

## 1. Pattern Decision Tree (Pick the mode first, then write)

```
What does your skill do?

├─ Execute a step-by-step operation (deploy / install / migrate)
│  → Pattern A: Linear Flow → load references/pattern_linear.md
│
├─ Help LLM choose among many options (10+ branches)
│  → Pattern B: Decision Tree + Progressive Disclosure → load references/pattern_decision_tree.md
│
├─ Repeatedly execute "do → verify → improve" (TDD / review / audit)
│  → Pattern C: Iterative Loop → load references/pattern_loop.md
│
├─ Drive a long-term project across multiple sessions
│  → Pattern D: Baton Loop → load references/pattern_baton.md
│
├─ Span days/weeks with stage gates and Go/No-Go decisions
│  → Pattern E: Multi-Phase + Checkpoints → load references/pattern_multiphase.md
│
└─ Control HOW the LLM thinks, not WHAT it does (deep analysis / audit)
   → Pattern F: Thinking Framework → load references/pattern_thinking.md
```

**After selecting a pattern, load the matching reference file for the template skeleton.**

---

## 2. Universal Writing Techniques (Shared by all patterns)

### 2.1 Anti-Laziness Weapons

| Weapon | Principle | Example |
|--------|-----------|---------|
| **Strong tone** | Imperative > suggestive | `Delete it. Start over.` not `Consider trying...` |
| **Excuse rebuttal table** | Preempt LLM self-rationalizations | `\| "Too complex" \| Complexity is not a reason to skip \|` |
| **Quantified thresholds** | Hard minimums with numbers | `Minimum 3 invariants, 5 assumptions per function` |
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
Layer 1: Frontmatter (~100 tokens)
  → LLM scans all skill descriptions, decides whether to load

Layer 2: SKILL.md body (<5K tokens)
  → Core instructions, decision tree, workflow steps

Layer 3: references/ (on-demand, each <3K tokens)
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
description: |               # MOST CRITICAL — LLM decides load from this
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
