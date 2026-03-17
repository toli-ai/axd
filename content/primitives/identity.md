# Identity

Who is this agent, and how is it recognized across interactions?

---

Identity is how agents are named, scoped, and tracked. Every action an agent takes should be attributable to a specific identity - not to "the API" or "some automation." Without identity, you can't audit what happened, you can't scope permissions, and you can't distinguish between an agent that's authorized and one that's impersonating.

For human users, identity is an account with a name, email, and avatar. For agents, identity is a service principal, an agent ID, or a session label that ties actions to a specific actor with a specific role in a specific workspace. The important part is persistence and attribution. When an agent modifies a record, the audit trail should show which agent, under what authority, in what context - not just "modified by API."

Identity also enables multi-agent coordination. When three agents operate in the same system, they need to recognize each other, understand their respective roles, and avoid stepping on each other's work. An identity-less system treats all agents as the same anonymous actor, which makes coordination impossible and debugging a nightmare.

**What this means for your site:**

- Assign distinct identities to agent sessions. Each agent should have a unique ID, not share a generic service account.
- Include role and workspace scope in the identity object. "Agent-47, role: order-processor, workspace: fulfillment-east" is useful. "API user" is not.
- Log the agent identity on every mutation. Audit trails should answer "who did this and why" for every state change.
- Support identity verification for inter-agent communication. When one agent claims to be a specific actor, the receiving system should be able to verify that claim.
- Return the current identity in API responses. An agent should be able to call a `/whoami` endpoint to confirm its identity, permissions, and session scope.

**Good example:** Each agent session gets a unique ID like `agent:order-bot:workspace-east`. Every API call logs this identity. A `/me` endpoint returns the agent's ID, role, permissions, and session metadata. Other agents can verify identity through signed tokens.

**Bad example:** All agents authenticate with the same API key. Audit logs show "api-user" for every action. When something goes wrong, there's no way to determine which agent caused it.
