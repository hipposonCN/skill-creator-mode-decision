# Skill Creator — Mode Decision Framework

A compact, opinionated framework for designing effective OpenClaw / Codex / Claude Code Agent Skills. Built from analyzing 7 top-tier production skills and distilling their patterns into a reusable decision tree.

> **Core idea**: Don't write a skill until you've picked the right *pattern* for it. A deployment workflow needs a different cognitive structure than a safety audit.

---

## The 5+1 Pattern Decision Tree

When you need to create a skill, ask: **What does this skill do?**

```
├─ Execute a step-by-step operation (deploy / install / migrate)
│  → Pattern A: Linear Flow
│
├─ Help LLM choose among many options (platform with 10+ branches)
│  → Pattern B: Decision Tree + Progressive Disclosure
│
├─ Repeatedly execute "do → verify → improve" (TDD / review / audit)
│  → Pattern C: Iterative Loop
│
├─ Drive a long-term project across multiple sessions
│  → Pattern D: Baton Loop (cross-session persistence)
│
├─ Span days/weeks with stage gates and Go/No-Go decisions
│  → Pattern E: Multi-Phase + Checkpoints + Skill Orchestration
│
└─ Control HOW the LLM thinks, not WHAT it does (audit / deep analysis)
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

Article: [How to Write Agent Skills — Patterns & Best Practices from 7 Top-Tier Skills](https://news.qq.com/rain/a/20260427A01X7500)

---

## License

MIT — use it, fork it, improve it. PRs welcome.
