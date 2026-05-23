# Pattern A: Linear Flow

> **For**: Deployment, installation, migration — any operation with clear steps
> **Model**: vercel-deploy (77 lines) — the smallest yet complete skill template

## Structure Template

```markdown
# Title

[One-sentence core principle + safety default]

## Prerequisites
- [Precondition 1]
- [Precondition 2]

## Quick Start (Main Flow)
### Step 1: [Action]
```bash
[Concrete command]
```

### Step 2: [Action]
[Concrete instruction]

### Step 3: [Action]
[Concrete instruction]

## Fallback (Degraded Path)
[Plan B when main flow fails]

## Troubleshooting
| Issue | Solution |
|-------|----------|
| [Problem 1] | [Solution] |
```

## Key Techniques

| Technique | Example | Why It Works |
|-----------|---------|-------------|
| Safety default | "Always deploy as preview, not production" | Prevents LLM from making dangerous moves |
| Concrete commands | Every step gives a copy-paste-able bash command | LLM doesn't have to guess |
| Timeout hint | "Use a 10 minute (600000ms) timeout" | Prevents LLM from hanging on timeout |
| Fallback path | CLI failure has a fallback script | Provides Plan B |
| Negative instruction | "Do not curl the deployed URL to verify" | Explicitly forbids wrong actions |

## Decision Rule

If your skill can be described as "First do A, then B, then C" → use Linear Flow.
