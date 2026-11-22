# AgentOps in Python

Trace, bound, and audit AI agent runs before they fail.

Talk by **Mikalai Saskavets**.

**Conference:** [Python Summit 2026](https://pythonsummit.org/), 19–20 October 2026 (19 October online, 20 October at the Copernicus Science Centre, Warsaw).
**Talk:** 20 October 2026.

**Slides:** https://miksask.github.io/talks/python-summit-agentops/

## Abstract

**AgentOps in Python: Trace, Bound, and Audit AI Agent Runs Before They Fail**

AI agents are increasingly connected to real production systems: internal support tools, deployment assistants, data pipelines, CI/CD copilots, and platform automation. The difficult part is not only making an agent call a tool. The difficult part is understanding what happened when one user request turns into multiple LLM calls, tool executions, retries, background jobs, and human approvals. This talk presents a practical AgentOps operating model for Python and cloud-native teams. I will treat every agent run as an observable workflow with three explicit contracts: a stable run ID across all steps, a trace that connects LLM calls with tool calls, and a ledger for side-effecting tool executions. Around these contracts, we will add production controls: idempotency keys, retry limits, timeouts, token and cost budgets, recursion limits, and escalation rules. The talk uses one Python-oriented reference architecture as a running example: an API layer, an agent/workflow layer, background workers, tool adapters, and observability storage. The same design can be implemented with FastAPI, LangGraph, Celery, Kubernetes Jobs, or similar systems, but the focus is on the operational contracts rather than on a specific framework. Attendees will leave with a concrete checklist for operating agentic workflows in production: what to log, what not to log, where to put idempotency keys, how to structure tool execution records, when to stop or ask for human approval, and how to turn production incidents into regression tests and evaluations.

### About the speaker (Bio)

Mikalai Saskavets is a Python and GenAI Engineer with 13+ years of experience in backend development and system architecture. He works on production LLM applications, RAG pipelines, and agent-based workflows, with a focus on reliability, observability, evaluation, and human-in-the-loop interactions. He has also contributed to the Python community as a PyCon Belarus Program Committee Co-Chair and Minsk Python Meetup organizer.

## Viewing the slides locally

Open `index.html` in a browser. No build step is needed.

## Rebuilding the deck

The deck is written with [Marp](https://marp.app/). To regenerate
`index.html` from `slides-deck.md`:

```bash
marp slides-deck.md -o index.html
```

The output embeds the Marp runtime (CSS and JS), so different Marp CLI versions
produce different `index.html` files. The current build uses Marp CLI v4.4.0
(Marp Core v4.3.0). To pin it:

```bash
npx @marp-team/marp-cli@4.4.0 slides-deck.md -o index.html
```
