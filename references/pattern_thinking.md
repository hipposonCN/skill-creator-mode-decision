# Pattern F: Thinking Framework

> **For**: Security audits, code review, architecture analysis — scenarios requiring deep thinking
> **Model**: audit-context-building (302 lines)
> **Core**: Control HOW the LLM thinks, not WHAT it does

## Structure Template

```markdown
# Title

## Purpose (Positioning)
This skill controls HOW you think, not WHAT you do.
[Control thinking style, not behavior]

## When to Use / When NOT to Use
- ✅ Use scenarios
- ❌ Do not use scenarios

## Rationalizations (Excuse Rebuttal Table)
| Excuse | Reality |
|--------|---------|
| "[Excuse]" | "[Rebuttal]" |

## Phase 1: Initial Orientation (Orientation Scan)
[Quick global scan to build mental model]

## Phase 2: [Deep Analysis Phase] (Core)
### Per-[Unit] Checklist (Per-unit analysis checklist)
- [ ] Item 1
- [ ] Item 2

### Cross-[Unit] Analysis (Cross-unit tracing)
[Trace data/logic flows across modules]

### Output Requirements (Output format + quantified thresholds)
- Every [unit] must have at least [X] [Y] (quantify!)
- Output format: [template]

### Completeness Checklist (Completeness check)

## Phase 3: Global Understanding (Global Understanding)
[Synthesize findings, build global view]

## Stability Rules (Anti-Hallucination Rules)
- Never reshape evidence to fit earlier assumptions
- [Other anti-hallucination rules]

## Non-Goals (Explicitly Forbidden Actions)
- ❌ [Do not do 1]
- ❌ [Do not do 2]
```

## Key Techniques

| Technique | Example | Why It Works |
|-----------|---------|-------------|
| Thinking tools | First principles, 5 Why, 5 How | Give LLM an analysis framework, not specific commands |
| Quantified thresholds | "Every function must have at least 3 invariants, 5 assumptions" | Forces LLM to reach sufficient analysis depth |
| Non-goal constraints | "Do not identify bugs, do not propose fixes" | Restrains what LLM most wants to do — understand first, judge later |
| Anti-hallucination rules | "Never reshape evidence to fit earlier assumptions" | Prevents LLM from deceiving itself |
| Sub-agent guidance | When and how to use sub-agents | Divide and conquer |

## vs Patterns 1-5 (Essential Difference)

| Patterns 1-5 | Thinking Framework |
|-------------|-------------------|
| Control "what to do" | Control "how to think" |
| Process-oriented | Cognition-oriented |
| Correctness in steps | Correctness in reasoning quality |

## Decision Rule

If your skill requires the LLM to perform **deep analysis** rather than quick execution, and you need to control **thinking quality** rather than operational steps → use Thinking Framework.
