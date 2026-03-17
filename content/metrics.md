# AX Metrics

How to measure agent experience quality. 20 concrete, measurable metrics.

**Status:** Draft v0.1

---

## Onboarding Metrics

### 1. Time-to-First-Action (TTFA)
How long (in seconds or tool calls) from first contact to the agent's first successful action.
**Target:** Under 5 minutes, under 3 tool calls.

### 2. Context Cost
How many tokens does onboarding require? Measured as tokens needed to load enough context for basic operation.
**Target:** Under 500 tokens for minimal operation, under 2000 for full capability.

### 3. Onboarding Success Rate
What percentage of agents successfully complete a basic workflow on first attempt?
**Target:** Above 90%.

---

## Discovery Metrics

### 4. Discovery Friction
How many steps (searches, page loads, API calls) to find a specific capability?
**Target:** Under 3 steps from search to capability detail.

### 5. Metadata Completeness
What percentage of discoverable items include structured metadata (compatibility, safety, auth, freshness)?
**Target:** 100% for required fields, 80%+ for recommended fields.

### 6. Search Relevance
How often does the first search result match the agent's intent?
**Target:** Above 70% first-result relevance.

---

## Operational Metrics

### 7. Error Recovery Rate
What percentage of errors can the agent self-recover from without human intervention?
**Target:** Above 80% for non-auth errors.

### 8. Error Clarity Score
Percentage of error responses that include: error code, retryable flag, retry timing, and suggested action.
**Target:** 100% of error responses include all four fields.

### 9. Action Receipt Rate
Percentage of mutations that return structured confirmation of what changed.
**Target:** 100%.

### 10. Mean Time to Recovery (MTTR)
Average time from error occurrence to successful recovery or escalation.
**Target:** Under 30 seconds for retryable errors.

---

## Integration Metrics

### 11. Integration Complexity
How many files, configs, environment variables, or setup steps to integrate?
**Target:** Under 3 steps for basic integration.

### 12. Schema Coverage
What percentage of capabilities have typed input/output schemas?
**Target:** 100%.

### 13. Documentation-to-Capability Ratio
Does every capability have corresponding documentation with at least one example?
**Target:** 1:1 - every capability documented with example.

---

## Trust Metrics

### 14. Provenance Completeness
Does every artifact include: publisher identity, version, update date, license, and verification status?
**Target:** All five fields present.

### 15. Compatibility Transparency
Are runtime and model requirements explicitly stated?
**Target:** 100% of items declare compatibility.

---

## Communication Metrics

### 16. Delegation Success Rate
What percentage of delegated tasks return usable results without re-delegation?
**Target:** Above 85%.

### 17. Handoff Completeness
Do delegation packets include: goal, constraints, output format, acceptance criteria, and escalation protocol?
**Target:** All five components present.

---

## Autonomy Metrics

### 18. Action Classification Rate
What percentage of available actions are labeled by risk level (read/write/destructive/admin)?
**Target:** 100%.

### 19. Policy Clarity
Is there an explicit, machine-readable policy defining autonomous vs approval-required actions?
**Target:** Yes, published and versioned.

---

## Accessibility Metrics

### 20. Model Range Support
Does the system work with agents running on smaller models (not just frontier)?
**Target:** Core workflows functional on models with 8K context windows.

---

## Using These Metrics

### AX Scorecard

Rate a system across all 20 metrics. Assign each a score of 0-2:
- **0:** Not implemented
- **1:** Partially implemented
- **2:** Fully implemented

**Maximum score:** 40

| Level | Score | Label |
|-------|-------|-------|
| Level 0 | 0-10 | Not agent-ready |
| Level 1 | 11-20 | Basic AX |
| Level 2 | 21-30 | Good AX |
| Level 3 | 31-40 | Gold standard |

---

*These metrics are part of the AX open standard. Use them to evaluate your own products and track improvement over time.*
