# Communication

How do agents exchange information with humans and other agents?

---

Agents don't work alone. They delegate to sub-agents, hand off tasks to humans, receive instructions from orchestrators, and report results back to callers. Communication is the structure of these exchanges - not just sending messages, but packaging information so the recipient can act on it without a follow-up.

The most common communication failure is freeform delegation. One agent tells another "handle the billing issue" with no output format, no acceptance criteria, no deadline, and no blockers protocol. The receiving agent interprets the task however it wants, produces output in an unexpected format, and the calling agent can't use the result. Every handoff needs a contract: what exactly to do, what to return, what format to use, and what to do if stuck.

Human-agent communication has its own failure modes. An agent that dumps a raw data structure on a human is communicating in the wrong language. An agent that sends a three-paragraph summary when the human asked a yes-or-no question is wasting attention. Communication means matching the message to the recipient - structured data for agents, concise natural language for humans, and explicit ask format for escalations.

**What this means for your site:**

- Define handoff schemas for agent-to-agent delegation. Include: task description, expected output format, acceptance criteria, deadline, and what to do if blocked.
- Provide message templates for common exchanges. "Request approval for X" should have a structured format with the action, the risk level, the deadline, and the approve/deny mechanism.
- Support channel metadata. When an agent needs to communicate, it should know: what formats are accepted, what the latency expectations are, and whether the recipient is a human or another agent.
- Include summarization endpoints for long content. If an agent needs to relay complex results to a human, a summary endpoint or field prevents context overload.
- Make escalation paths explicit. When an agent can't resolve something, the communication channel to a human should be defined - not improvised.

**Good example:** A sub-agent handoff includes `{"task": "verify order totals", "input": "/orders?status=pending", "output_format": "json", "output_path": "/results/order-verification", "acceptance": "all totals match or discrepancies flagged", "if_blocked": "report to orchestrator with error details"}`.

**Bad example:** An agent sends another agent a plain text message: "Can you check the orders? Something seems off." No structure, no output format, no criteria. The receiving agent guesses at what to check and how to report back.
