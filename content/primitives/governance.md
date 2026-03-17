# Governance

What rules constrain this agent, and who enforces them?

---

Governance is the set of rules, policies, and audit mechanisms that control what agents can do. It's not the same as access control - access determines whether an agent can reach an endpoint. Governance determines whether the agent should, and what happens when it does.

Every system that agents operate in has implicit rules. "Don't send more than 100 emails per hour." "Don't modify production data during business hours." "Escalate to a human before issuing refunds over $500." When these rules live only in documentation or tribal knowledge, agents violate them - not maliciously, but because no one told the machine about the constraint. Governance makes the implicit explicit: machine-readable policies that agents can evaluate before acting.

Audit trails are the other half. When something goes wrong - and in production systems, something always goes wrong - you need to answer: what happened, who did it, when, and under what authority. If agent actions aren't logged with identity, timestamp, and policy context, post-incident analysis is guesswork. Good governance means every significant action is traceable, and every policy violation is detectable.

**What this means for your site:**

- Publish machine-readable policy files that define what agents can do, what requires approval, and what is prohibited. Format these as structured data, not natural language paragraphs buried in docs.
- Label irreversible actions in your API schema. If DELETE is permanent, the endpoint metadata should say `reversible: false` so agents and governance layers can apply appropriate caution.
- Log every agent action with identity, timestamp, action type, and the policy that authorized it. "Agent X performed action Y at time Z under policy P" is the minimum audit record.
- Define escalation triggers. "Refunds over $500 require human approval" should be a policy rule the system enforces, not guidance the agent may or may not follow.
- Separate environment constraints. What an agent can do in staging versus production should be governed by policy, not by deploying different code. Same agent, different rules.
- Support policy updates without redeployment. Governance rules change. The system should load policies dynamically, not bake them into application code.

**Good example:** A policy file defines: `{"action": "issue_refund", "max_amount_auto": 500, "above_max": "require_approval", "approver": "finance-team", "audit": true, "reversible": false}`. The agent reads this, processes small refunds automatically, and queues large ones for human review. Every action is logged.

**Bad example:** The only governance is a wiki page titled "Agent Rules" that says "be careful with refunds." No machine-readable policy, no audit logging, no enforcement. When an agent issues a $5,000 refund automatically, no one knows until the monthly reconciliation.
