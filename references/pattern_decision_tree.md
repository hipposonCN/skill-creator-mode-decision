# Pattern B: Decision Tree + Progressive Disclosure

> **For**: Large platform navigation, product selection, problem diagnosis — domains with 10+ branches
> **Model**: cloudflare-deploy (224 lines), cloudflare (211 lines)

## Structure Template

```markdown
# Title

## Authentication (Credential Setup)
[How to get credentials / environment variables]

## Quick Decision Trees
### "I need to run code" (Classify by user intent)
  ├─ Edge serverless → workers/
  ├─ Containerized deployment → containers/
  └─ ...

### "I need to store data"
  ├─ Relational → D1/
  ├─ KV storage → KV/
  └─ ...

### "I need AI/ML"
  └─ ...

## Product Index (Lookup Table)
| Product | Reference | Description |
|---------|-----------|-------------|
| Workers | references/workers.md | Serverless compute |
| D1 | references/d1.md | SQL database |
```

## Key Techniques

| Technique | Example | Why It Works |
|-----------|---------|-------------|
| User-intent classification | "I need to run code" not "Compute products" | Uses user language, not technical jargon |
| Tree navigation | ├─ Branch structure | LLM quickly locates the right product |
| Progressive disclosure | Main file <5K, references/ expand on demand | Doesn't waste context window |
| Product index table | Product → Reference mapping | Structured fast lookup |

## Token Budget Design

```
Main SKILL.md:     <5K tokens (decision tree + index)
references/:        1-3K tokens each (loaded 1-2 at a time)
Total footprint:    <8K tokens
```

## Advanced: Split Navigator vs Operator

Same domain can split into two skills:
- **Navigator** (e.g. cloudflare): Only does selection, no operations
- **Operator** (e.g. cloudflare-deploy): Includes auth, commands, troubleshooting

## Decision Rule

If your skill covers a domain with 10+ branches and each branch has substantial docs → use Decision Tree.
