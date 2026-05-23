# Pattern C: Iterative Loop

> **For**: TDD, code review, design review — any "do → verify → improve" cycle
> **Model**: test-driven-development (371 lines)

## Structure Template

```markdown
# Title

## The Iron Law (Unbreakable Core Principle)
[1-2 sentences of the strongest, most absolute principle]

## [Loop Body Name]
### PHASE A — [Action]
[Concrete instruction]

### Verify A
[Verification command]

### PHASE B — [Action]
[Concrete instruction]

### Verify B
[Verification command]

### Repeat
Back to PHASE A.

## Common Rationalizations (Excuse Rebuttal Table)
| Excuse | Reality |
|--------|---------|
| "[LLM likely excuse 1]" | [Why this excuse doesn't hold] |
| "[Excuse 2]" | [Rebuttal] |
| ... | ... |

## Verification Checklist (Exit Conditions)
- [ ] [Condition 1]
- [ ] [Condition 2]
- [ ] ...
```

## Key Techniques

| Technique | Example | Why It Works |
|-----------|---------|-------------|
| Strong tone | "Delete it. Start over." | LLMs tend to "flex"; strong tone increases compliance |
| Good/Bad contrast | Wrap examples in `<Good>` and `<Bad>` tags | Contrastive teaching is most effective |
| Excuse rebuttal table | Preemptively list 12 LLM excuses and rebut each | Blocks every escape path |
| Verification checklist | 8-item checklist as loop exit condition | Ensures quality before ending |
| Human fallback | "ask your human partner" | Hands off when uncertain |

## Decision Rule

If your skill requires the LLM to repeatedly execute a "do → verify → improve" loop → use Iterative Loop.
