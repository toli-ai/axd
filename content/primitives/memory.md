# Memory

How does an agent remember what happened before?

---

Agents without memory start from zero every session. They re-discover capabilities, re-learn preferences, repeat mistakes, and ask the same questions. Memory is what turns a stateless tool into something that gets better over time - and what lets your site deliver continuity instead of repetition.

Memory for agents is not a raw transcript dump. It's structured recall: what happened, when, what mattered, and how to find it again. An agent needs to store a session summary with timestamps and source links, then retrieve it when relevant context arises. The difference between good and bad memory is retrieval. A system that stores everything but makes none of it searchable has hoarding, not memory.

Sites that support agent memory provide persistence endpoints, session summaries, and retrieval mechanisms. Sites that don't force agents to carry all context internally - which means hitting context window limits, losing old information, and degrading over long interactions. If your system has user preferences, interaction history, or accumulated state, give agents a way to store and fetch it.

**What this means for your site:**

- Provide session or state persistence endpoints. Let agents save key-value pairs, summaries, or structured checkpoints tied to their identity.
- Support retrieval by recency and relevance. "What did this agent do last time?" and "What's related to this current task?" are the two queries that matter most.
- Include timestamps and source links in stored data. An agent recalling "the user prefers dark mode" needs to know when that was set and from what interaction.
- Set retention policies explicitly. How long is stored data kept? Is it per-session, per-agent, or permanent? Agents need to know whether yesterday's memory still exists.
- Offer summarization hooks. Raw transcripts are expensive to re-process. If your system can provide condensed session summaries, agents consume them in a fraction of the token cost.

**Good example:** An API offers `/agent/memory` endpoints where agents can store and retrieve structured context. A GET request returns recent session summaries with timestamps, and supports search by topic. Retention policy is documented: 90 days, per-agent.

**Bad example:** No persistence mechanism exists. The agent's only option is to dump its entire conversation history into every new request, consuming context window space with irrelevant old exchanges.
