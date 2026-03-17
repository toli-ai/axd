# Access

How does an agent authenticate, get permissions, and maintain a session?

---

Access is the gateway to everything. Before an agent can read data, call an endpoint, or trigger a workflow, it needs to prove who it is and what it's allowed to do. For human users, this is login screens and cookie sessions. For agents, it's API keys, OAuth tokens, and scoped permissions.

The critical difference: agents can't click through a browser-based OAuth flow, solve a CAPTCHA, or check an email for a verification code. If your only auth path requires a visual browser, agents are locked out entirely. Access needs a programmatic path - token exchange, service accounts, delegated credentials - that works without a rendered UI.

Equally important is scope separation. An agent that only needs to read product listings should not receive a token that can also delete the database. Least privilege is not just a security best practice - it's how agents operate safely. When something goes wrong (and it will), the blast radius is determined by what the token allows. A read-only token can't cause a write-path disaster.

**What this means for your site:**

- Provide a programmatic auth flow. If OAuth is your primary method, support a client credentials or device flow that doesn't require a browser session.
- Separate read and write scopes. Let agents request exactly the permissions they need, not an all-or-nothing bundle.
- Return clear errors on permission failures. A 403 should include which specific permission is missing and how to request it - not just "Forbidden."
- Support short-lived tokens with refresh mechanisms. Agents should not hold long-lived credentials that become a security liability.
- Document the auth flow in machine-readable format. If an agent needs to discover how to authenticate, that information should be in your API manifest, not buried in a getting-started guide.

**Good example:** An API offers scoped tokens - `orders:read`, `orders:write`, `inventory:read` - with a token exchange endpoint. Permission errors return `{"missing_scope": "orders:write", "request_url": "/oauth/authorize"}`.

**Bad example:** A single API key grants full access. Permission failures return `403 Forbidden` with no body. The only way to get the key is through a browser-based dashboard.
