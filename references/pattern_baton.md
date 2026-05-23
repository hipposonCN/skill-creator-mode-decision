# Pattern D: Baton Loop (Cross-Session Persistence)

> **For**: Multi-iteration long-term projects that need to persist across sessions
> **Model**: stitch-loop (203 lines)

## Structure Template

```markdown
# Title

## Overview (Baton Pattern Summary)
[One sentence: files are state, passed across sessions]

## The Baton System (File Protocol)
- `next-prompt.md`: Launch instructions for the next session
- `progress.md`: Current progress snapshot
- `decisions.md`: Key decision log

## Execution Protocol (6-Step Protocol)
### Step 1: Read the Baton
read next-prompt.md — get context

### Step 2: Consult Context Files
read related files and decision records

### Step 3: Generate (Execute Task)
Complete this session's work

### Step 4: Integrate (Merge Results)
Write output to working directory

### Step 5: Update Documentation
Update progress.md and decisions.md

### Step 6: Prepare the Next Baton ⚠️ (Critical!)
⚠️ CRITICAL: Forgetting to write the baton breaks the loop.
Write next-prompt.md as the launch instructions for the next session.
```

## Key Techniques

| Technique | Example | Why It Works |
|-----------|---------|-------------|
| File-as-state | `next-prompt.md` as the baton | LLM doesn't need to remember "where we left off" |
| Survival mechanism | Step 6 marked as Critical + MUST | Forgetting the baton kills the loop |
| File protocol | Each file has a clear responsibility | LLM only reads/writes per protocol |
| Orchestration-agnostic | CI/CD, human-in-the-loop, agent chains all work | Same skill adapts to multiple automation environments |

## vs Pattern C (Iterative Loop)

| Dimension | Iterative Loop (TDD) | Baton Loop (Stitch Loop) |
|-----------|---------------------|-------------------------|
| State storage | LLM conversation context | External file system |
| Cross-session | ❌ | ✅ |
| Loop exit | All checklist items ticked | Roadmap cleared |
| Duration | Single session (minutes~hours) | Long-term (days~weeks) |

## Decision Rule

If your skill needs to persist across multiple sessions, or requires multiple agents to collaborate → use Baton Loop.
