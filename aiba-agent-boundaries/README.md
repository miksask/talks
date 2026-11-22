# AI Agents Need Boundaries

Controlling cost, actions, and accountability in production.

Talk by **Mikalai Saskavets**.

**Conference:** [AIBA Conference 2026](https://aibaconference.com/agenda/), Katowice, 21–23 October 2026.
**Talk:** 21 October 2026, Cloud & AI stage.

**Slides:** https://miksask.github.io/talks/aiba-agent-boundaries/

## Abstract

#### AI Agents Need Boundaries: Controlling Cost, Actions, and Accountability in Production

Problem: AI agents can turn one request into many model calls, tool actions, retries, and side effects, making cost, risk, and accountability hard to control. Methodology: a practical model of execution boundaries, action records, budgets, and escalation rules, illustrated with production-style failures. Conclusion: bounded autonomy makes behavior safer and explainable. Business value: teams gain a framework for moving agents from demos to dependable production systems.

### About the speaker (Bio)

Mikalai has 15+ years of software engineering experience, combining GenAI development with engineering leadership. He builds production LLM applications, RAG pipelines, and AI agent workflows, focusing on reliability and turning AI capabilities into dependable business value.

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
