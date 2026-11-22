# When AI Agents Fail in Production

Tracing, budgets, and tool execution ledgers.

Talk by **Mikalai Saskavets**.

**Conference:** [DevAI by Data Science Summit 2026](https://devai.dssconf.pl/), 19–20 October 2026 (19 October online, 20 October at the Copernicus Science Centre, Warsaw).
**Talk:** 20 October 2026.

**Slides:** https://miksask.github.io/talks/devai-agent-failures/

## Abstract

**When AI Agents Fail in Production: Tracing, Budgets, and Tool Execution Ledgers**

Problem: AI agents are increasingly connected to real production systems: internal support tools, deployment assistants, data pipelines, CI/CD copilots, and platform automation. The difficult part is not only making an agent call a tool. The difficult part is understanding what happened when one user request turns into multiple LLM calls, tool executions, retries, background jobs, and human approvals. Methodology: This talk presents a practical AgentOps operating model for Python and cloud-native teams. Every agent run is treated as an observable workflow with three explicit contracts: a stable run ID across all steps, a trace that connects LLM calls with tool calls, and a ledger for side-effecting tool executions. Around these contracts, we add production controls: idempotency keys, retry limits, timeouts, token and cost budgets, recursion limits, and escalation rules. Conclusions: Normal service logs are not enough for agentic systems. Production agent workflows need operational contracts that make failures explainable, auditable, and bounded before they become expensive or unsafe. Implications for practitioners and business: Attendees will leave with a concrete checklist for operating agentic workflows in production: what to log, what not to log, where to put idempotency keys, how to structure tool execution records, when to stop or ask for human approval, and how to turn production incidents into regression tests and evaluations.

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
