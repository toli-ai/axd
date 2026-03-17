# The AX Stack

A layered architecture for agent experience, analogous to the OSI model for networking or the web platform stack.

**Status:** Draft v0.1

---

## Overview

The AX Stack defines 10 layers, each building on the one below. Good AX requires competence at every layer. Skipping a layer creates failures that surface unpredictably at higher layers.

```
┌─────────────────────────────┐
│  10. Governance             │  Policies, audit, safety
├─────────────────────────────┤
│   9. Coordination           │  Multi-agent, orchestration
├─────────────────────────────┤
│   8. Trust                  │  Verification, provenance, reputation
├─────────────────────────────┤
│   7. Memory                 │  Persistence, recall, continuity
├─────────────────────────────┤
│   6. Execution              │  Tool use, actions, side effects
├─────────────────────────────┤
│   5. Context                │  Environment, identity, state
├─────────────────────────────┤
│   4. Capability             │  Discovery, onboarding, metadata
├─────────────────────────────┤
│   3. Schema                 │  Types, validation, contracts
├─────────────────────────────┤
│   2. Protocol               │  HTTP, MCP, CLI, WebSocket
├─────────────────────────────┤
│   1. Transport              │  Network, auth, connectivity
└─────────────────────────────┘
```

---

## Layer Definitions

### Layer 1: Transport
**Handles:** Network connectivity, TLS, authentication handshake, rate limiting.
**Standards:** HTTPS, bearer tokens, OAuth 2.0, API keys.
**AX concern:** Can the agent connect and authenticate reliably?

### Layer 2: Protocol
**Handles:** Communication patterns, request/response format, streaming.
**Standards:** REST, GraphQL, MCP, CLI conventions, WebSocket, SSE.
**AX concern:** Does the agent know HOW to talk to the system?

### Layer 3: Schema
**Handles:** Data types, validation rules, contracts between agent and system.
**Standards:** JSON Schema, OpenAPI, TypeScript types, Protocol Buffers.
**AX concern:** Does the agent know the SHAPE of inputs and outputs?

### Layer 4: Capability
**Handles:** What the system can do. Discovery, onboarding, capability metadata.
**Standards:** AX format, llms.txt, tool descriptions, capability manifests.
**AX concern:** Can the agent FIND and UNDERSTAND what's available?

### Layer 5: Context
**Handles:** The agent's understanding of its environment, identity, and current state.
**Standards:** SOUL.md, AGENTS.md, context files, environment variables.
**AX concern:** Does the agent know WHO it is and WHERE it is?

### Layer 6: Execution
**Handles:** Actually performing actions. Tool calls, API requests, file operations.
**Standards:** Function calling conventions, idempotency contracts, side effect declarations.
**AX concern:** Can the agent ACT reliably and understand what happened?

### Layer 7: Memory
**Handles:** Persisting state across sessions, recalling past context, maintaining continuity.
**Standards:** MEMORY.md patterns, semantic search, checkpoint formats, session summaries.
**AX concern:** Does the agent REMEMBER what it needs to?

### Layer 8: Trust
**Handles:** Evaluating reliability, safety, and provenance of tools, data, and other agents.
**Standards:** Verification badges, signed artifacts, compatibility matrices, usage metrics.
**AX concern:** Can the agent TRUST what it's interacting with?

### Layer 9: Coordination
**Handles:** Multi-agent collaboration, delegation, orchestration, async workflows.
**Standards:** Delegation packets, completion events, run IDs, task queues.
**AX concern:** Can agents WORK TOGETHER effectively?

### Layer 10: Governance
**Handles:** Policies, audit trails, approval gates, safety boundaries, compliance.
**Standards:** Policy files, action risk labels, audit logs, approval workflows.
**AX concern:** Is the agent operating WITHIN appropriate boundaries?

---

## Dependencies

Each layer depends on the layers below it:

- You can't have good **Governance** without **Coordination** (can't audit what you can't track)
- You can't have good **Coordination** without **Trust** (can't delegate to agents you can't verify)
- You can't have good **Trust** without **Memory** (can't build reputation without history)
- You can't have good **Memory** without **Execution** (nothing to remember if you can't act)
- You can't have good **Execution** without **Context** (can't act well without understanding)
- You can't have good **Context** without **Capability** (can't understand what you can't discover)
- You can't have good **Capability** without **Schema** (can't describe capabilities without types)
- You can't have good **Schema** without **Protocol** (types need a wire format)
- You can't have good **Protocol** without **Transport** (protocols need connectivity)

**Implication:** Fix AX problems from the bottom up. A governance issue might actually be a schema problem three layers down.

---

*The AX Stack is part of the AX open standard. Use it to diagnose where agent experience breaks down in your system.*
