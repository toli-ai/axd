# Notifications

How does an agent learn that something changed, finished, or needs attention?

---

Agents don't sit in front of a screen watching for toast messages. They need programmatic notification surfaces - webhooks, event streams, task queues - that deliver state changes as structured data. Without notifications, agents are left polling endpoints in tight loops, wasting compute and still missing time-sensitive events.

A notification system for agents has different requirements than one for humans. Humans can triage a noisy inbox. Agents need every notification to be typed, prioritized, and deduplicated, or they'll process the same event five times, miss a critical alert buried in noise, or waste context window space parsing irrelevant updates. The payload is the interface - it needs to carry enough information for the agent to decide whether to act, defer, or ignore without making additional API calls.

When notifications are missing entirely, agents must invent their own awareness. They poll every endpoint they care about on a timer, compare state diffs, and hope nothing changed between intervals. This is fragile, expensive, and slow. The system knows when something changed - it should say so.

**What this means for your site:**

- Provide webhooks for state changes. Order completed, payment failed, new message received - anything an agent would care about should have a push mechanism.
- Include event type, priority level, dedupe key, and timestamp in every notification payload. Agents use these to filter, sort, and avoid duplicate processing.
- Add a `retry_schedule` or delivery guarantee. If the agent's endpoint is briefly down, retry with exponential backoff - don't silently drop the event.
- Sign webhook payloads so agents can verify authenticity. An unsigned webhook is a spoofing vector.
- Support suppression and filtering. Let agents subscribe to specific event types instead of receiving everything and discarding 90% of it.

**Good example:** A webhook fires on order status change with `{"event": "order.shipped", "order_id": "abc-123", "priority": "normal", "dedupe_key": "ship-abc-123-1", "timestamp": "2025-01-15T10:30:00Z", "details_url": "/orders/abc-123"}`. Signed with HMAC.

**Bad example:** The system sends an email notification with the subject "Something changed in your account." No webhook endpoint, no event stream, no way for an agent to receive it programmatically.
