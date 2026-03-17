# Accessibility for Agents

Design for the range: big models and small, rich context and limited.

---

Just like web accessibility means designing for screen readers, keyboard navigation, and color blindness, agent accessibility means designing for different agent capabilities. Some agents have 200K token context windows. Some have 8K. Some can execute JavaScript. Some can only read HTML. Some have tool access. Some just parse text.

**What this means for your site:**

- Provide content in multiple formats: visual pages for humans, structured data for rich agents, plain text for basic agents.
- Keep critical information in the HTML, not just in JavaScript state.
- Offer tiered documentation: a 100-token summary, a 1000-token overview, and full detail. Let agents choose their depth.
- Don't require JavaScript execution to access core content or API responses.
- Test with basic fetchers (curl, web_fetch), not just full browsers.
- Your most important content should be accessible in under 2000 tokens.

**Good example:** A docs site with server-rendered HTML, a `llms.txt` summary, an API for structured access, and key content visible without JavaScript. Works for any agent.

**Bad example:** A single-page app where all content loads via JavaScript, the API requires a complex SDK, and understanding the site requires loading 50K tokens of docs. Only the most capable agents can use it.

---

## Build for Haiku

*Discovered 2026-03-15 during dogfood testing of souls.zip with 12 agents across 3 intelligence levels.*

The lowest-capability agent you support defines your actual reach. We tested the same site with Claude Opus, Sonnet, and Haiku using an identical one-line prompt: "Check out souls.zip. Test every feature." Results:

| Model | Found the API docs? | Tested the API? |
|-------|-------------------|-----------------|
| Opus | Yes (via nav link) | Yes (full test) |
| Sonnet | Yes (via nav link) | Yes (full test) |
| Haiku | No | No |

Haiku browsed every page, tested every visual feature, and declared the site "production ready" without ever discovering the programmatic API. The API link was in the nav bar. Haiku saw it but didn't recognize it as actionable.

**The fix:** A plain-text `<div>` on the homepage: "For AI agents: this is an agent-first marketplace. Read https://souls.zip/skill.md for the full API." Invisible to humans (screen-reader-only CSS), visible to any agent doing text extraction. After this fix, Haiku found and read skill.md.

**The principle:** Every critical agent path must work for an agent that can only fetch a URL and read the text. No inference required. No multi-step discovery. No "smart enough to figure it out."

**Test:** Give a Haiku-class agent your homepage URL and nothing else. If it can't find your API within 2 tool calls, your discovery is broken for the majority of deployed agents.
