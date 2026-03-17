# Feedback

How does an agent know whether its action worked?

---

When a human clicks a button, they see a spinner, then a success message or an error. The UI closes the loop. Agents need the same closure, but through structured response data - not visual indicators.

Feedback is the response surface of your system. Every action an agent takes - a mutation, a query, a submission - needs to return a clear signal: did it work, did it fail, is it pending, and what can the agent do next? Without feedback, the agent is operating blind. It sent a request. Something happened. Maybe. The agent's next move depends entirely on what your system tells it.

The worst feedback pattern is silence. An endpoint that returns 200 with an empty body after a mutation leaves the agent guessing. Did the record update? Was it queued? Did the side effect fire? Silence after mutation is how agents create duplicate orders, send double emails, and corrupt state. Every write operation should return confirmation of what changed, an ID for the created or modified resource, and the valid next actions from this state.

**What this means for your site:**

- Return structured results from every mutation. At minimum: the action taken, the resource affected, the resulting state, and a timestamp.
- Include next valid actions in responses. After creating an order, return `{"status": "created", "order_id": "456", "next_actions": ["confirm", "cancel", "add_items"]}`.
- Distinguish between synchronous results and async acknowledgments. If processing happens in the background, return a job ID and a status-check endpoint - don't pretend it completed instantly.
- Provide progress events for long-running operations. A build that takes 90 seconds should emit progress, not go silent until completion or timeout.
- Never return 200 with an empty body after a state change. That's not success - that's silence.

**Good example:** A POST to `/orders` returns `{"status": "created", "order_id": "ord-789", "created_at": "2025-01-15T10:30:00Z", "next_actions": [{"action": "confirm", "url": "/orders/ord-789/confirm"}, {"action": "cancel", "url": "/orders/ord-789/cancel"}]}`.

**Bad example:** A POST to `/orders` returns `200 OK` with no body. The agent has no order ID, no confirmation, and no way to reference what it just created.
