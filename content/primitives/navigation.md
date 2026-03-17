# Navigation

How does an agent move between resources, states, and actions?

---

Navigation is how an agent traverses your system. Humans have menus, breadcrumbs, and back buttons. Agents have links, resource IDs, and next-action hints. When navigation works, an agent can flow from discovery to inspection to action without guessing where to go next. When it breaks, the agent dead-ends after every call.

The biggest navigation failure is disconnected resources. An agent searches for products and gets a list of IDs. Now what? If the response doesn't include links to each product's detail endpoint, the agent has to know your URL pattern by convention. That's fragile. It breaks when you change versions, restructure paths, or add new resource types. Linked resources are self-navigating - the agent follows the data instead of hardcoding assumptions.

Good navigation also means signaling what comes next. After an agent creates an order, the response should indicate the valid next steps: confirm, cancel, add items. This is not about dumping every possible action - it's about surfacing the relevant transitions from the current state. Think of it as a state machine the agent can follow without reading the manual.

**What this means for your site:**

- Include links in API responses. Every resource reference should be a full URL or a clear path, not just a bare ID that requires URL construction.
- Add next-action hints to state-changing responses. After a POST, tell the agent what it can do next with the created resource.
- Use consistent, predictable URL structures. `/orders/123` and `/orders/123/items` is navigable. `/api/v2/getOrderById?id=123` and `/fetch-items?order=123` is not.
- Provide parent and sibling references. An item should link back to its collection. A detail page should link to related resources.
- Support pagination with cursors or next-page links, not just offset numbers that break when data changes.

**Good example:** A search response returns results where each item includes `detail_url`, `actions: ["inspect", "purchase"]`, and `related: [{"type": "reviews", "url": "/products/42/reviews"}]`. The agent navigates without guessing.

**Bad example:** The API returns bare IDs with no links. Moving between resources requires the agent to know the URL template for every resource type, and those templates are only documented in a README.
