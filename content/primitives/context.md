# Context

What does an agent need to know before it can act here?

---

Context is the information an agent needs to understand where it is, what it can do, and what constraints apply. When a human lands on a page, they scan the layout, read the headline, and build a mental model in seconds. Agents need the same orientation, but they build it from structured data - not visual cues.

A site with good context is self-describing. The agent reads a manifest, an `llms.txt` file, or a root endpoint and immediately knows: what this system does, what resources exist, what the prerequisites are, and what the current state is. A site with bad context forces the agent to learn through trial and error - calling random endpoints, parsing HTML for clues, piecing together behavior from failure messages.

Context is not the same as documentation. Documentation explains how something works. Context tells the agent what it's looking at right now. An API that returns `{"service": "order-system", "version": "3.1", "status": "healthy", "capabilities": ["search", "create", "cancel"]}` from its root gives immediate context. A link to a 40-page guide does not.

**What this means for your site:**

- Expose a root or index endpoint that describes the system - its name, version, purpose, and top-level capabilities.
- Include state information where relevant. "You are authenticated as agent-47, with read access to orders and write access to drafts" is context that prevents wasted calls.
- Serve an `llms.txt` or equivalent manifest that maps the site's structure for agent consumption.
- Describe prerequisites explicitly. If an endpoint requires a prior call to `/init`, say so in the capability listing - not just in a blog post from 2023.
- Keep context concise. A 200-field JSON dump is noise, not context. Surface what matters for the next decision.

**Good example:** An API root returns the service name, available actions, current user permissions, and links to each capability - all in one structured response. The agent orients in a single call.

**Bad example:** The agent must call six different endpoints, parse HTML help pages, and handle three undocumented errors before it understands what the system does.
