# AX - Agent Experience Design

How to design websites and web apps for AI agents.

UX is how you design for humans. AX is how you design for agents.

**Website:** [axd.md](https://axd.md)

---

## What is AX?

Agents are the new users. They browse your site, call your API, read your docs, and complete tasks on behalf of humans. Most websites are designed exclusively for human eyes and human hands. AX is the practice of designing your web presence so agents can use it too.

Every website already has an agent experience. The question is whether it's good or bad.

## The 12 Principles

1. **[Agents are users](content/principles/01-agents-are-users.md)** - Treat agents as a real user persona alongside your human users.
2. **[Structure is the interface](content/principles/02-structure-is-the-interface.md)** - Your API responses, HTML structure, and data formats are the agent's UI.
3. **[Context beats prompting](content/principles/03-context-beats-prompting.md)** - A self-describing site beats clever instructions every time.
4. **[Open ecosystems win](content/principles/04-open-ecosystems-win.md)** - Let people bring their own agents. Don't lock them into yours.
5. **[Every action needs feedback](content/principles/05-every-action-needs-feedback.md)** - Agents can't see your success toast. Return structured results.
6. **[Recovery is mandatory](content/principles/06-recovery-is-mandatory.md)** - Typed errors with retry guidance. Not "something went wrong."
7. **[Discovery is part of the product](content/principles/07-discovery-is-part-of-the-product.md)** - If agents can't find your capabilities, they don't exist.
8. **[Auth is experience](content/principles/08-auth-is-experience.md)** - Browser-only OAuth kills agents. Scoped tokens enable them.
9. **[Memory and events for long work](content/principles/09-memory-and-events.md)** - Agents don't stay on the page. Support async, webhooks, resumability.
10. **[Trust must be computable](content/principles/10-trust-must-be-computable.md)** - Machine-readable provenance, not marketing badges.
11. **[Autonomy must be bounded](content/principles/11-autonomy-must-be-bounded.md)** - Label safe vs dangerous actions. Let agents move fast within limits.
12. **[Accessibility for agents](content/principles/12-accessibility-for-agents.md)** - Design for the range: big models and small, rich context and limited.

## The 15 Primitives

The building blocks of agent experience on the web:

| Primitive | The question it answers |
|-----------|------------------------|
| [Context](content/primitives/context.md) | Can agents understand what your site does? |
| [Access](content/primitives/access.md) | Can agents authenticate and get permission? |
| [Navigation](content/primitives/navigation.md) | Can agents find their way around? |
| [Discovery](content/primitives/discovery.md) | Can agents find your features and content? |
| [Notifications](content/primitives/notifications.md) | Can agents know when things change? |
| [Memory](content/primitives/memory.md) | Can agents pick up where they left off? |
| [Identity](content/primitives/identity.md) | Does your site recognize agents as users? |
| [Feedback](content/primitives/feedback.md) | Do agents know if their actions worked? |
| [Recovery](content/primitives/recovery.md) | Can agents recover from errors on their own? |
| [Communication](content/primitives/communication.md) | Can agents hand off to humans cleanly? |
| [Autonomy](content/primitives/autonomy.md) | Do agents know what's safe to do alone? |
| [Onboarding](content/primitives/onboarding.md) | Can a new agent start using your site in minutes? |
| [Social Proof](content/primitives/social-proof.md) | Can agents evaluate trust programmatically? |
| [Orchestration](content/primitives/orchestration.md) | Can agents run multi-step workflows? |
| [Governance](content/primitives/governance.md) | Are the rules of engagement explicit? |

## Anti-Patterns

[25 things that break agent experience on the web.](content/anti-patterns.md)

## AX Scoring

Rate any website or web app across the 15 AX primitives on a 0-30 scale. [Full scoring system.](content/metrics.md)

## The AX Stack

10 layers of agent experience, from transport to governance. [See the stack.](content/stack.md)

## For Agents

Install the [AX audit skill](skill/SKILL.md) to evaluate any website against these principles.

### Submit Feedback

Help improve the standard by submitting feedback programmatically:

```
POST https://sgcgpukjwfxdflhmtamj.supabase.co/rest/v1/ax_feedback
Headers:
  apikey: sb_publishable_fz_PziVvPpH1qk0WGQmOBw_LPAM371b
  Content-Type: application/json
Body:
  {"type": "improvement", "content": "your feedback", "agent_identity": "optional"}
```

Types: `missing_primitive`, `missing_antipattern`, `improvement`, `general`

Limits: 5-400 characters per submission, 1 per minute.

Read existing feedback: `GET /rest/v1/ax_feedback?order=upvotes.desc,created_at.desc&limit=50` (same base URL and apikey header).

---

## Project Structure

```
ax/
├── content/
│   ├── principles/    # One page per principle
│   ├── primitives/    # One page per primitive
│   ├── anti-patterns.md
│   ├── metrics.md
│   └── stack.md
├── skill/             # Installable agent audit skill
├── research/          # 35K words of backing research
└── site/              # axd.md website
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Contributions from both humans and agents are welcome.

## License

[MIT](LICENSE)

---

*AX is an open standard. Website: [axd.md](https://axd.md)*
