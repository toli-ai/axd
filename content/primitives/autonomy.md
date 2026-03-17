# Autonomy

How much can an agent do without asking permission?

---

Autonomy is the boundary between what an agent can do on its own and what requires human approval. Get this wrong in either direction and you have a problem. Too much autonomy and agents make irreversible mistakes without oversight. Too little and every action stalls on a human approval queue, defeating the purpose of having an agent at all.

The key insight is that not all actions carry the same risk. Reading a product listing is safe. Deleting a production database is not. Autonomy should be graduated - automatically approved for low-risk operations, gated for destructive or expensive ones. The system needs to classify actions by consequence so agents can operate at full speed on safe tasks while pausing for human judgment on dangerous ones.

When autonomy boundaries are unclear, agents either over-ask (requesting approval to read a file) or over-act (sending customer emails without review). Both erode trust. A system with explicit autonomy levels trains agents to operate confidently within their lane and escalate reliably when they hit the boundary.

**What this means for your site:**

- Label every action with a risk level. Read operations are `safe`. Creates might be `moderate`. Deletes and financial transactions are `dangerous`. Make these levels part of your API metadata.
- Define approval modes per risk level. Safe actions auto-execute. Moderate actions log for review. Dangerous actions require explicit human approval before proceeding.
- Set autonomy budgets. An agent can spend up to $50 in API calls without approval, or create up to 10 records per hour. Budgets prevent runaway operations without blocking every individual action.
- Provide safe defaults. If the autonomy policy is unclear for a given action, the default should be "ask" - not "proceed."
- Make override mechanisms available. A human should be able to expand or restrict an agent's autonomy in real time without redeploying the system.

**Good example:** An API marks each endpoint with `risk: "safe"`, `risk: "moderate"`, or `risk: "dangerous"`. The agent's runtime auto-executes safe calls, queues moderate ones for async review, and blocks dangerous calls until a human approves via a confirmation endpoint.

**Bad example:** All actions are treated identically. Reading a user profile and deleting a user account go through the same flow with no distinction. Either everything requires approval (agent crawls) or nothing does (agent runs unchecked).
