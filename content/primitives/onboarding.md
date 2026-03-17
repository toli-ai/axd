# Onboarding

How does a new agent learn to use this system?

---

A human's first-run experience gets a setup wizard, tooltips, and a guided tour. An agent's first-run experience is usually a raw tool catalog and a prayer. Onboarding is how you take an agent from "I just connected to this system" to "I know what to do and how to do it" - without the agent having to fail its way through discovery.

Good onboarding is progressive disclosure. Don't dump 200 endpoints on the agent and hope it figures out which five matter. Start with a manifest: here's what this system does, here are the three most common workflows, here's a sandbox where you can try them safely. Let the agent build competence before it touches real data.

The sandbox is the critical piece most systems skip. Agents learn by doing, but doing in production on the first attempt is reckless. A sandbox or dry-run mode lets the agent execute a complete workflow - auth, query, mutate, verify - without real consequences. The agent learns the system's patterns, discovers its error formats, and builds confidence. When it moves to production, it already knows how the system behaves.

**What this means for your site:**

- Provide a starter manifest that lists the system's purpose, primary workflows, and prerequisite steps in order. Not a link to docs - the manifest itself.
- Offer a sandbox or dry-run mode where agents can execute actions without real side effects. Flag it clearly: `{"mode": "sandbox", "side_effects": false}`.
- Include example requests and responses for the most common workflows. Agents learn patterns from concrete examples faster than from abstract schema definitions.
- Use progressive disclosure. First call returns the basics. Deeper capabilities surface as the agent demonstrates understanding of the fundamentals.
- Provide a "hello world" flow - a minimal end-to-end task that confirms the agent is set up correctly. Auth works, permissions are right, the data format is understood.

**Good example:** A new agent connects and receives a manifest: "This is an order management system. Start with GET /orders to list orders. Try POST /orders/sandbox to create a test order. When ready, remove the /sandbox prefix for production." The agent runs the sandbox flow, sees the response structure, and transitions to real operations with confidence.

**Bad example:** A new agent connects and receives a list of 150 endpoints sorted alphabetically. No indication of where to start, no sandbox, no example flows. The agent picks an endpoint at random and gets a 403 because it hasn't called /init first.
