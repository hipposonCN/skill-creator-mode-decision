# Pattern E: Multi-Phase + Checkpoints + Skill Orchestration

> **For**: Complex multi-week flows requiring Go/No-Go decisions at key nodes
> **Model**: discovery-process (502 lines) — orchestrates 10+ sub-skills

## Structure Template

```markdown
# Title

## Key Concepts (Core Concepts + Anti-Patterns)
[Define key terms + list common mistakes]

## Phase 1: [Phase Name]
### Activities (Which sub-skills to invoke)
- Skill A → what it does
- Skill B → what it does

### Outputs (Phase Deliverables)
- [Deliverable 1]
- [Deliverable 2]

### Decision Point 1 (Checkpoint)
**Go/No-Go Conditions**:
- YES → proceed to Phase 2
- NO → [+X days/weeks, re-execute this phase]

## Phase 2-6... (Repeat same structure)

## Complete Workflow (End-to-End Timeline)
```
Phase 1 (X days) → Phase 2 (Y days) → ... → Phase N
```

## Common Pitfalls
| Pitfall | Consequence | How to Avoid |
|---------|-------------|-------------|
| | | |

## References (Sub-Skill List)
- `skill-a`: purpose
- `skill-b`: purpose
```

## Key Techniques

| Technique | Example | Why It Works |
|-----------|---------|-------------|
| Unified phase template | Every Phase has Activities → Outputs → Decision Point | LLM quickly understands the structure |
| Decision checkpoint | "Saturated? YES → next phase, NO → +1 week" | Prevents blind progress |
| Skill orchestration | Dispatch 10+ sub-skills | Orchestrator pattern: big skill dispatches small skills |
| Time impact | Every NO path labeled "+2-3 days" | User understands delay cost |
| Interaction protocol separation | Reference `workshop-facilitation` for interaction style | Separation of concerns |

## Decision Rule

If your skill spans days/weeks, has clear phase divisions and Go/No-Go decision points → use Multi-Phase.
