# Orchestration

How is agent work coordinated across tools, tasks, and time?

---

Agents rarely execute in isolation. A real workflow might involve one agent gathering data, another processing it, a third generating a report, and a human reviewing the result. Orchestration is the coordination layer - how work gets assigned, tracked, sequenced, and completed across multiple actors and systems.

Without orchestration primitives, agent coordination devolves into polling and copy-paste. One agent finishes a task and writes the result somewhere. Another agent polls a directory every 30 seconds hoping to find it. A third agent starts work before the second finishes because there's no dependency signal. The result is race conditions, wasted compute, and workflows that break silently when timing changes.

Good orchestration treats agent work like a job system. Tasks have IDs. Runs have status. Completions emit events. Dependencies are declared, not inferred. A platform that can trigger an agent run with preloaded context, track its progress, and receive a structured completion event is orchestration-ready. A platform that requires duct-taping agents together through shared files and cron jobs is not.

**What this means for your site:**

- Assign unique IDs to every task and run. An agent should be able to reference a specific execution, check its status, and retrieve its output by ID.
- Emit completion events. When a task finishes - successfully or not - broadcast a structured event that downstream agents can consume. Don't make them poll.
- Support dependency declarations. "Task B starts after Task A completes" should be a system-level guarantee, not an agent-level polling loop.
- Provide sandboxed execution contexts. Each agent run should have its own workspace, environment, and state - not share mutable global state with concurrent runs.
- Accept preloaded context on task creation. When triggering an agent, pass in the relevant data, config, and constraints - don't make the agent fetch everything from scratch.
- Support cancellation and timeout. Long-running agent work needs a kill switch and a deadline, not just a start button.

**Good example:** A platform accepts `POST /runs` with `{"task": "generate-report", "context": {...}, "depends_on": ["run-abc"], "timeout_seconds": 300}`. The run gets an ID, emits progress events, and fires a completion webhook with the result payload when done.

**Bad example:** Agent orchestration is stitched together with cron jobs polling a shared S3 bucket. Task status is inferred from whether a file exists. Dependencies are managed by sleep timers. When one agent runs slow, the whole chain breaks.
