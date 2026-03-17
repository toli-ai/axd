# Discovery

How does an agent find the capabilities, tools, and content it needs?

---

Discovery is how agents find what's available. Before an agent can use a tool, call an API, or install a skill, it needs to know the thing exists. For humans, this is browsing app stores, reading recommendation lists, or searching docs. For agents, it's querying registries, reading manifests, and evaluating structured metadata.

The quality of discovery determines whether agents find the right tool or give up. A registry that returns titles and nothing else forces the agent to fetch details on every single item to evaluate fitness. A registry that returns capability descriptions, input/output schemas, auth requirements, and compatibility tags lets the agent filter and select in one pass. The difference is seconds versus minutes - and for agents operating under time or cost budgets, that gap matters.

Discovery also has a trust dimension. When an agent finds three tools that claim to do the same thing, it needs signals to choose: which is maintained, which is verified, which works with its runtime. Without these signals, selection is random - and random selection in agent tooling means random failures in production.

**What this means for your site:**

- Expose a capability index with structured metadata - not just names, but descriptions, input/output schemas, auth requirements, and version info.
- Make capabilities searchable. Agents won't browse a paginated list of 200 items. Provide filtering by category, tag, or capability type.
- Include freshness and maintenance signals. `last_updated`, `maintained: true`, and version numbers let agents avoid stale or abandoned tools.
- Tag compatibility. If a tool requires a specific runtime, API version, or auth method, surface that in search results - not just on the detail page.
- Separate marketing copy from functional descriptions. "Revolutionary AI-powered solution" tells the agent nothing. "Accepts a search query string, returns ranked product results as JSON" tells it everything.

**Good example:** A tool registry where search results include description, input schema, required auth type, last updated date, and a compatibility badge. Agents filter to what works without clicking into each result.

**Bad example:** A flat list of 150 tools with only names and taglines like "Supercharge your workflow." No filtering, no schemas, no update dates.
