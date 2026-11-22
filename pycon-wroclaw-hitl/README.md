# Human-in-the-Loop is not enough

How to stop AI agent loops in Python.

Talk by **Mikalai Saskavets**.

**Conference:** [PyCon Wroclaw 2026](https://www.pyconwroclaw.com/), Wroclaw, 20–21 November 2026.
**Talk:** 21 November 2026.

**Slides:** https://miksask.github.io/talks/pycon-wroclaw-hitl/

## Abstract

### Human-in-the-loop is not enough: how to stop AI agent loops in Python

Human-in-the-Loop is now common in AI agent workflows: users approve actions, provide feedback, or interrupt execution. Yet production agents can still repeat the same tool calls, ignore corrections, continue after an intervention, or get stuck in multi-agent loops.

The underlying issue is execution state. If human feedback does not change the state of the workflow, the available actions, or its termination conditions, the agent can reach the same decision again.

This talk presents a practical anti-loop pattern for Python agent systems. We will combine explicit execution state, action deduplication, interrupt/resume gates, checkpointing, execution limits, and termination rules. A production-style example implemented with LangGraph and Chainlit will show how these mechanisms work together and where they belong in the workflow.

Attendees will leave with a concrete approach for building Python agent workflows where human intervention actually changes execution and repeated actions are detected before they become runaway loops.

---

### About the speaker (Bio)

Mikalai Saskavets is a Python and GenAI Engineer with 13+ years of experience in backend development and system architecture. He builds production LLM applications, RAG pipelines, and agent-based workflows, focusing on reliability, observability, evaluation, and execution control. He has also contributed to the Python community as a PyCon Belarus Program Committee Co-Chair and Minsk Python Meetup organizer.

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
