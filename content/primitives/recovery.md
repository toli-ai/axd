# Recovery

What does an agent do when something fails?

---

Agents hit errors constantly. Rate limits, expired tokens, validation failures, server timeouts, network blips. This is not edge-case territory - it's the normal operating texture of any agent doing real work. A site designed only for the happy path breaks agents on the first hiccup.

Recovery is what separates a stuck agent from one that self-heals. The difference is entirely in what your error responses communicate. A typed error with a retry hint, a fallback action, and a classification of severity lets the agent make a decision: retry, try something else, or escalate to a human. A generic "something went wrong" is a dead end.

Recovery also includes reversibility. When an agent takes an action that turns out to be wrong, can it undo it? If your system supports cancellation, rollback, or compensating transactions, surface those as explicit actions on the error or the original resource. An agent that knows it can undo a mistake operates with more confidence - and more safely - than one that treats every action as permanent.

**What this means for your site:**

- Every error response needs four fields: `error_code` (typed, machine-readable), `retryable` (boolean), `retry_after_seconds` (if retryable), and `human_required` (boolean, for escalation).
- Use HTTP status codes correctly. 429 for rate limits with a `Retry-After` header. 401 for expired auth. 422 for validation with per-field errors. Never 500 for client mistakes.
- Include fallback actions when the primary path fails. If an item is out of stock, suggest alternatives. If a write fails due to conflict, return the current state so the agent can merge.
- Flag irreversible actions before execution. If deleting a resource is permanent, the API schema or confirmation step should say so explicitly.
- Provide rollback or cancel endpoints for multi-step operations. If step 3 of 5 fails, the agent needs a way to undo steps 1 and 2.

**Good example:**
```json
{
  "error_code": "INVENTORY_CONFLICT",
  "message": "Item quantity changed since last read",
  "retryable": true,
  "retry_after_seconds": 0,
  "current_state": {"quantity": 3},
  "suggested_action": "re-read and retry with updated quantity",
  "human_required": false
}
```

**Bad example:**
```json
{"error": "Request failed. Please try again later."}
```
No code, no classification, no retry guidance. The agent retries blindly or gives up.
