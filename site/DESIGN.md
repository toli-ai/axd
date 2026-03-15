# AXD Site Design Document

**Version:** 1.0
**Date:** 2026-03-13
**Status:** Ready for review

---

## 1. Site Architecture

### Pages

| Page | URL | Purpose |
|------|-----|---------|
| Homepage | `/` | What AXD is, the 12 principles, 15 primitives, links to everything |
| Principle (x12) | `/principles/agents-are-users` through `/principles/accessibility-for-agents` | Deep dive on each principle |
| Anti-Patterns | `/anti-patterns` | The 25 anti-patterns, grouped by category |
| Metrics | `/metrics` | The 20 metrics and 4-level scoring system |
| Stack | `/stack` | The 10-layer AX Stack visualization |
| About | `/about` | What AXD is, who made it, how to contribute |

**Total: 17 pages.** Small enough to be a single HTML file with anchor links, but better as individual files for deep-linking and agent discoverability.

### URL Structure

```
axd.dev/
axd.dev/principles/agents-are-users
axd.dev/principles/structure-is-the-interface
axd.dev/principles/context-beats-prompting
axd.dev/principles/open-ecosystems-win
axd.dev/principles/every-action-needs-feedback
axd.dev/principles/recovery-is-mandatory
axd.dev/principles/discovery-is-part-of-the-product
axd.dev/principles/auth-is-experience
axd.dev/principles/memory-and-events
axd.dev/principles/trust-must-be-computable
axd.dev/principles/autonomy-must-be-bounded
axd.dev/principles/accessibility-for-agents
axd.dev/anti-patterns
axd.dev/metrics
axd.dev/stack
axd.dev/about
axd.dev/llms.txt
```

### Navigation Model

- **Header:** Logo/wordmark + 4 nav links (Principles, Anti-Patterns, Metrics, Stack)
- **Principle pages:** Previous/Next navigation at bottom (like 12factor.net)
- **Homepage:** Everything scannable in one scroll, with jump links to sections
- **Footer:** GitHub, llms.txt, souls.zip attribution

### Information Architecture

```
Homepage
├── Hero (one sentence + lineage)
├── The 12 Principles (numbered list with summaries)
├── The 15 Primitives (compact grid)
├── Quick links (Anti-Patterns, Metrics, Stack)
└── Footer (GitHub, llms.txt, attribution)

Principle Page (x12)
├── Number + Title
├── One-line summary (the subtitle)
├── Full explanation (2-4 paragraphs)
├── What this means for your site (bullet list)
├── Good example (code/pattern)
├── Bad example (code/anti-pattern)
└── Prev/Next navigation

Anti-Patterns Page
├── Introduction
├── 6 category sections
│   ├── Access (3 anti-patterns)
│   ├── Documentation (4)
│   ├── API Design (5)
│   ├── Error Handling (4)
│   ├── Discovery (3)
│   ├── Webhook (3)
│   └── Context (3)
└── Contribute CTA

Metrics Page
├── Introduction to scoring
├── 7 metric categories with 20 metrics
├── AX Scorecard table
└── Scoring levels (0-40)

Stack Page
├── ASCII/visual stack diagram
├── 10 layer definitions
├── Dependency chain explanation
└── "Fix from the bottom up" principle
```

---

## 2. Visual Design System

### Typography

**Primary font:** Inter (Google Fonts). Clean, modern, excellent readability at all sizes. Loaded with `display=swap` for performance.

**Monospace:** JetBrains Mono (Google Fonts). For code blocks and technical identifiers.

**Scale:**

| Element | Size | Weight | Line Height |
|---------|------|--------|-------------|
| Page title (h1) | 2.5rem (40px) | 700 | 1.15 |
| Section heading (h2) | 1.75rem (28px) | 600 | 1.3 |
| Subsection heading (h3) | 1.25rem (20px) | 600 | 1.4 |
| Body text | 1.0625rem (17px) | 400 | 1.7 |
| Small text / captions | 0.875rem (14px) | 400 | 1.5 |
| Principle number | 0.75rem (12px) | 700 | 1.0 |
| Code | 0.9375rem (15px) | 400 | 1.6 |

**Line length:** Max 680px for body text. Optimal readability.

### Colors

Deliberately minimal. This is a specification document, not a marketing site.

| Token | Hex | Usage |
|-------|-----|-------|
| `--ink` | `#1a1a1a` | Primary text |
| `--ink-light` | `#555555` | Secondary text, descriptions |
| `--ink-faint` | `#999999` | Captions, metadata |
| `--surface` | `#ffffff` | Page background |
| `--surface-warm` | `#fafaf8` | Alternate section background, code blocks |
| `--border` | `#e5e5e5` | Dividers, card borders |
| `--accent` | `#2563eb` | Links, principle numbers, interactive elements |
| `--accent-hover` | `#1d4ed8` | Link hover state |
| `--good` | `#16a34a` | Good example indicators |
| `--bad` | `#dc2626` | Bad example indicators |

**No gradients. No shadows deeper than 1px. No decorative elements.** The content is the design.

### Spacing

8px base unit. Everything is a multiple of 8.

| Token | Value | Usage |
|-------|-------|-------|
| `--space-xs` | 4px | Tight gaps (inline elements) |
| `--space-sm` | 8px | Between related items |
| `--space-md` | 16px | Standard paragraph spacing |
| `--space-lg` | 32px | Between sections |
| `--space-xl` | 64px | Between major page sections |
| `--space-2xl` | 96px | Hero padding, page sections |

### Component Styles

**Principle Card (Homepage)**
- No border, no card container
- Principle number as a small blue label: `I.` through `XII.` (Roman numerals, matching 12factor.net's convention)
- Title as a link in `--ink` color, bold
- One-line description below in `--ink-light`
- Hover: title turns `--accent`
- Spacing: 24px between items, with a thin `--border` divider

**Primitive Badge (Homepage)**
- Inline block, pill-shaped
- `--surface-warm` background, `--border` border, 1px
- Principle name in `--ink`, small text
- No hover effect - these are labels, not links (in v1)

**Code Block**
- `--surface-warm` background
- 1px `--border` border
- 16px padding
- `border-radius: 6px`
- JetBrains Mono font
- No syntax highlighting in v1 (keep it simple)

**Good/Bad Example**
- Thin left border: 3px `--good` or `--bad`
- Small label above: "Good" or "Bad" in the respective color
- Content in normal body style

**Navigation**
- Fixed header: white background, thin bottom border
- Logo left, nav links right
- Links: `--ink-light` default, `--ink` on hover, `--accent` when active
- Mobile: hamburger menu (the one place where minimal JS is acceptable)

---

## 3. Page-by-Page Layouts

### Homepage Layout

See Section 4 for detailed breakdown.

### Principle Page Layout

```
[Header Navigation]

[Breadcrumb: AXD > Principles > #N]

[Roman Numeral] — small, blue, uppercase
[Title] — h1, large
[Subtitle] — one-line summary, --ink-light

---

[Full explanation]
2-4 paragraphs of body text explaining the principle
in depth. Why it matters, how to think about it.

[What this means for your site]
- Bullet point 1
- Bullet point 2
- Bullet point 3
- Bullet point 4

[Good Example]
Green left-border block with title and
code/pattern example

[Bad Example]
Red left-border block with title and
code/anti-pattern example

---

[← Previous Principle]          [Next Principle →]

[Footer]
```

**Key decisions:**
- Roman numerals create continuity with 12factor.net and reinforce the "numbered standard" feel
- The subtitle (one-liner) is always visible - it's the principle compressed to its essence
- Good/bad examples are always present - they make the abstract concrete
- Prev/Next navigation encourages reading sequentially, like a book

### Anti-Patterns Page Layout

```
[Header Navigation]

[Title] — "AX Anti-Patterns"
[Subtitle] — "25 things that break agent experience."

[Table of Contents]
Grouped list of all 25 anti-patterns, linked by anchor

---

[Category Section: Access Anti-Patterns]
### 1. The Browser-Only Auth Flow
Description paragraph

### 2. The All-or-Nothing Token
Description paragraph

### 3. The Silent Permission Failure
Description paragraph

---

[Category Section: Documentation Anti-Patterns]
...

[Footer]
```

**Key decisions:**
- Table of contents at top for scanability (agents and humans both benefit)
- Numbered sequentially 1-25, grouped by category
- Each anti-pattern is its own anchor for deep linking
- Category sections have a subtle `--surface-warm` background alternation

### Metrics Page Layout

```
[Header Navigation]

[Title] — "AX Metrics"
[Subtitle] — "20 metrics for measuring agent experience quality."

[AX Scorecard Summary]
Visual table showing the 4 scoring levels (0-10, 11-20, 21-30, 31-40)
with labels: Not agent-ready, Basic AX, Good AX, Excellent AX, Gold standard

---

[Metric Category: Onboarding]
### 1. Time-to-First-Action (TTFA)
Definition + Target

### 2. Context Cost
Definition + Target

...

[Footer]
```

### Stack Page Layout

```
[Header Navigation]

[Title] — "The AX Stack"
[Subtitle] — "10 layers of agent experience."

[Stack Visualization]
CSS-rendered stack diagram - 10 colored layers
stacked vertically, labeled. Pure HTML/CSS, no images.

---

[Layer Definitions]
Each layer gets:
- Layer number and name
- "Handles:" bullet
- "Standards:" bullet
- "AX concern:" bullet (as a callout)

[Dependencies Section]
The dependency chain explanation

[Footer]
```

**Key decisions:**
- The stack visualization is CSS, not an image - it renders cleanly for agents and humans
- Layer numbers count from 1 (Transport) up to 10 (Governance), matching bottom-up reading
- Each layer links to relevant principles

---

## 4. Homepage in Detail

### Section 1: Hero

```
AXD
Agent Experience Design

How to design websites and web apps for AI agents.

UX is how you design for humans.
DX is how you design for developers.
AX is how you design for agents.
```

- "AXD" as large wordmark, not a logo image (text-based, agent-readable)
- Subtitle in `--ink-light`, one sentence
- The UX/DX/AX lineage as a three-line typographic element
- No hero image, no illustration, no gradient
- White background, centered text, generous vertical padding (96px top/bottom)

### Section 2: The 12 Principles

```
The 12 Principles

I. Agents Are Users
   Treat agents as a real user persona alongside your human users.

II. Structure Is the Interface
   Your API responses, HTML structure, and data formats are the agent's UI.

III. Context Beats Prompting
   A self-describing site beats clever instructions every time.

...through XII.
```

- Section heading "The 12 Principles" in h2
- Each principle: Roman numeral (small, blue), title (bold, linked), one-line description (light)
- Thin divider between each principle
- No cards, no grid - a clean vertical list, like a table of contents in a book
- Links go to individual principle pages

### Section 3: The 15 Primitives

```
The 15 Primitives
Building blocks of agent experience.

Context · Access · Navigation · Discovery · Notifications ·
Memory · Identity · Feedback · Recovery · Communication ·
Autonomy · Onboarding · Social Proof · Orchestration · Governance
```

- Section heading in h2
- One-line description
- Primitives displayed as a flowing text line with dot separators, or as a 3x5 compact grid
- Each primitive is a subtle pill/badge
- No individual pages for primitives in v1 - they're conceptual building blocks, not standalone essays

### Section 4: Quick Links

```
Also in the standard:

Anti-Patterns           Metrics              The AX Stack
25 things that break    20 metrics for       10 layers of agent
agent experience.       scoring AX quality.  experience architecture.
```

- Three-column layout (stacks to single column on mobile)
- Each is a text link with brief description
- No cards, no icons - just clean text links
- Links to `/anti-patterns`, `/metrics`, `/stack`

### Section 5: For Agents

```
For Agents

This site ships llms.txt for agent consumption.
Install the AXD audit skill to evaluate any website against these principles.

→ llms.txt    → Audit Skill    → GitHub
```

- Brief section acknowledging agent readers
- Links to llms.txt, the audit skill, and GitHub
- This section practices what AXD preaches - acknowledging agents as users

### Section 6: Footer

```
─────────────────────────────────────
An open standard by souls.zip

GitHub · llms.txt · Contribute · MIT License
```

- Minimal footer
- Attribution to souls.zip
- Key links
- No social media icons, no newsletter signup, no cookie banner

---

## 5. How the Site Eats Its Own Dog Food

The AXD site MUST practice what it preaches. Here's how each principle applies:

| Principle | How the site implements it |
|-----------|---------------------------|
| 1. Agents Are Users | Ships `llms.txt`, uses semantic HTML, includes schema.org markup |
| 2. Structure Is the Interface | Semantic HTML5 (`article`, `section`, `nav`, `header`, `footer`, `main`), meaningful heading hierarchy |
| 3. Context Beats Prompting | Every page starts with a title and one-sentence summary - no preamble needed |
| 4. Open Ecosystems Win | Standard is MIT licensed, no proprietary tooling required |
| 5. Every Action Needs Feedback | Not applicable (informational site, no user actions) |
| 6. Recovery Is Mandatory | Clean 404 page with navigation back to content |
| 7. Discovery Is Part of the Product | `llms.txt` index, clean URL structure, table of contents on long pages |
| 8. Auth Is Experience | No auth required - fully public |
| 9. Memory and Events | Stable URLs for bookmarking/referencing |
| 10. Trust Must Be Computable | Version number, last-updated dates, GitHub source link |
| 11. Autonomy Must Be Bounded | Informational site - all content is safe to consume |
| 12. Accessibility for Agents | Works without JS, clean HTML, small page sizes, fast loading |

### Specific agent-friendly features:

1. **`llms.txt`** at the root - structured index of all content
2. **Schema.org markup** - `WebSite`, `Article`, `BreadcrumbList` types
3. **Semantic HTML** - every heading, section, and list is meaningful
4. **No JavaScript requirement** - content renders in pure HTML
5. **Small page sizes** - each page under 20KB, fits easily in any context window
6. **Clean URL structure** - human and machine readable
7. **Structured headings** - h1 > h2 > h3 hierarchy, never skipping levels
8. **`<meta>` descriptions** - every page has a description meta tag

---

## 6. Technical Approach

### Build System: None

The site is static HTML. No build step. No SSG. No framework.

**Why:**
- The site has 17 pages. A build system adds complexity with zero benefit.
- Static HTML is the fastest possible delivery. No hydration, no bundle.
- Any developer can contribute by editing HTML files.
- The site practices what it preaches: structure is the interface, and HTML IS the structure.

### File Structure

```
axd-site/
├── index.html
├── principles/
│   ├── agents-are-users.html
│   ├── structure-is-the-interface.html
│   ├── context-beats-prompting.html
│   ├── open-ecosystems-win.html
│   ├── every-action-needs-feedback.html
│   ├── recovery-is-mandatory.html
│   ├── discovery-is-part-of-the-product.html
│   ├── auth-is-experience.html
│   ├── memory-and-events.html
│   ├── trust-must-be-computable.html
│   ├── autonomy-must-be-bounded.html
│   └── accessibility-for-agents.html
├── anti-patterns.html
├── metrics.html
├── stack.html
├── about.html
├── styles.css          ← Single shared stylesheet
├── llms.txt
├── robots.txt
├── sitemap.xml
├── favicon.svg         ← Simple SVG favicon, no external deps
└── 404.html
```

### Shared CSS

One `styles.css` file, under 5KB. Contains:
- CSS custom properties (the design tokens above)
- Base typography
- Layout (max-width container, responsive grid)
- Component styles (principle list, code blocks, good/bad examples, stack diagram)
- Print styles (the site should print cleanly too)

### Hosting

Static file hosting. Any of: GitHub Pages, Cloudflare Pages, Netlify, Vercel. No server required.

**Recommended:** GitHub Pages with custom domain `axd.dev`. Free, automatic deploys from the repo, SSL included.

### Performance Targets

| Metric | Target |
|--------|--------|
| First Contentful Paint | < 500ms |
| Total page weight (homepage) | < 50KB |
| Time to Interactive | < 500ms (no JS) |
| Lighthouse Performance | 100 |
| Core Web Vitals | All green |

### SEO and Agent Discoverability

- `<meta name="description">` on every page
- `<link rel="canonical">` on every page
- `sitemap.xml` listing all pages
- `robots.txt` allowing all crawlers
- `llms.txt` for agent discovery
- Open Graph tags for social sharing
- Schema.org JSON-LD on every page

### Progressive Enhancement (Optional JS)

The site works with zero JavaScript. Optional JS for:
- Mobile navigation toggle (hamburger menu)
- Copy button on code blocks

Both degrade gracefully. Mobile nav shows all links by default without JS. Code blocks are selectable text without the copy button.

---

## 7. Design Rationale

### Why Roman Numerals?

12factor.net uses them. They signal "this is a numbered standard" - a sequential, ordered set of principles. Arabic numbers feel like a list; Roman numerals feel like a framework.

### Why No Cards on the Homepage?

lawsofux.com uses cards beautifully, but AXD has 12 principles + 15 primitives + anti-patterns + metrics + stack. Cards would create visual overload. A clean numbered list (like 12factor.net) lets you scan 12 principles in seconds. Cards force you to parse 12 individual visual containers.

### Why No Dark Mode?

The brief says white and clean. A single theme means one set of design decisions, perfectly tuned. Dark mode can come in v2 with a `prefers-color-scheme` media query.

### Why Inter?

It's the closest thing to a "standard" for modern web typography. It was designed specifically for screens. It's free. It renders beautifully from 12px to 48px. It has a clean, neutral personality that lets the content speak.

### Why No Framework?

17 pages. A framework would be optimizing for a scale that doesn't exist. The maintenance cost of React/Next/Astro/Hugo is higher than the maintenance cost of 17 HTML files and one CSS file.

---

*This design document is a deliverable of the AXD site project. The companion `index.html` file contains the complete homepage mockup.*
