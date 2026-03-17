---
name: ax-audit
description: >
  Evaluate any system, API, tool, or platform against AX (Agent Experience Design) 
  principles. Use when asked to audit agent experience, evaluate AX compliance, or
  improve how a product works for agents. Produces a scored report across all 15 
  AX primitives with specific, actionable recommendations.
---

# AX Audit Skill

Evaluate a system's agent experience quality against the AX standard.

## When to Use

- "Audit this API for agent experience"
- "How AX-compliant is this tool?"
- "What's the agent experience like for [product]?"
- "How can we improve AX for [system]?"
- Evaluating a new tool or platform before adopting it
- Reviewing your own product's agent-friendliness

## Process

### Step 1: Gather Information

Collect available information about the target system:
- API documentation (fetch if URL available)
- Tool descriptions or skill files
- Error responses (try a few calls if possible)
- Authentication flow
- Available metadata and discovery mechanisms

### Step 2: Score Each Primitive

Rate the system 0-2 on each of the 15 AX primitives:

| Score | Meaning |
|-------|---------|
| 0 | Not implemented or actively harmful |
| 1 | Partially implemented, room for improvement |
| 2 | Well implemented, meets AX standards |

**Primitives to evaluate:**

1. **Context** - Does the system help agents understand their environment?
2. **Access** - Is auth clear, scoped, and programmatic?
3. **Navigation** - Can agents traverse resources and workflows logically?
4. **Discovery** - Can agents find capabilities with structured metadata?
5. **Notifications** - Does the system surface state changes to agents?
6. **Memory** - Does the system support persistent state across sessions?
7. **Identity** - Are agent actions attributable and auditable?
8. **Feedback** - Do actions return structured results with next steps?
9. **Recovery** - Are errors typed, classified, and recoverable?
10. **Communication** - Does the system support structured delegation and handoff?
11. **Autonomy** - Are actions labeled by risk with clear approval policies?
12. **Onboarding** - Can a new agent start using this in under 5 minutes?
13. **Social Proof** - Are there computable trust signals?
14. **Orchestration** - Does the system support async workflows and coordination?
15. **Governance** - Are policies, audit trails, and boundaries explicit?

### Step 3: Identify Anti-Patterns

Check against the 25 known AX anti-patterns. Flag any that apply.

### Step 4: Generate Report

Output format:

```
## AX Audit Report: [System Name]

### Score: [X]/30

### Primitive Scores
| Primitive | Score | Notes |
|-----------|-------|-------|
| Context | 0/1/2 | ... |
| ... | ... | ... |

### AX Level
- 0-10: Not agent-ready
- 11-20: Basic AX
- 21-30: Good AX
- 31-40: Gold standard

### Anti-Patterns Detected
- [List any matches from the 25 anti-patterns]

### Top 3 Improvements
1. [Highest impact change]
2. [Second highest]
3. [Third highest]

### Detailed Findings
[Per-primitive analysis with specific examples and recommendations]
```

## Reference

The full AX standard is at [axd.md](https://axd.md).

- Full principles: `content/principles/` directory
- Full primitives: `content/primitives/` directory
- Anti-patterns: `content/anti-patterns.md`
- Metrics: `content/metrics.md`
