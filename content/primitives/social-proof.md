# Social Proof

How does an agent assess whether something is trustworthy, maintained, and worth using?

---

When a human evaluates a product, they check reviews, star ratings, download counts, and "last updated" dates. Agents need the same signals - but structured as data, not scattered across UI elements. Social proof for agents is the metadata that enables trust decisions: is this tool maintained, is this publisher verified, does this work with my runtime, and do other agents use it successfully?

Without social proof, agents select tools and services essentially at random. Three tools claim to handle payments. One was last updated two years ago, one has a 30% failure rate, and one is actively maintained with a 99.5% success rate. Without provenance metadata, the agent has no basis to choose - and choosing wrong means failed transactions, wasted time, and broken workflows.

Trust and provenance data is not optional in agent ecosystems. As the number of available tools, skills, and services grows, the quality signal becomes the primary filter. Agents operating without it are like humans shopping on a marketplace with no reviews, no seller ratings, and no return policy.

**What this means for your site:**

- Include publisher verification status. A signed publisher identity tells agents the tool comes from who it claims to come from.
- Expose maintenance signals: `last_updated`, `maintained` flag, version history. Agents should be able to filter out abandoned tools without checking each one manually.
- Provide success and reliability metrics where available. A `success_rate: 0.995` field is more useful than a marketing claim of "enterprise-grade reliability."
- Tag runtime and version compatibility. If a tool requires Node 20+ or API v3, surface that in the listing metadata - not just in the install-time error message.
- Show usage indicators. Install counts, active user counts, or invocation frequency help agents distinguish proven tools from untested ones.
- Separate editorial ratings from computed metrics. Human-curated quality scores and automated success rates serve different purposes - provide both where possible.

**Good example:** A skill registry entry shows: `publisher: "verified:acme-corp"`, `last_updated: "2025-01-10"`, `success_rate: 0.992`, `installs: 14200`, `compatible_runtimes: ["node-20", "python-3.11"]`, `version: "2.4.1"`. The agent evaluates fitness in one read.

**Bad example:** A tool listing shows a name, a one-sentence marketing tagline, and a logo. No update date, no publisher info, no compatibility tags, no usage data. The agent installs it, discovers it's incompatible, and starts over.
