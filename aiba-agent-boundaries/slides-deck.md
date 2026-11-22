---
marp: true
paginate: true
size: 16:9
theme: default
title: "AI Agents Need Boundaries: Controlling Cost, Actions, and Accountability in Production"
author: "Mikalai Saskavets"
description: "A 25-minute AIBA talk on permission, resource, evidence, and handoff boundaries for AI agents"
footer: "AIBA 2026 · Mikalai Saskavets"
style: |
  @font-face {
    font-family: "Cygun";
    src: url("./assets/fonts/cygun/Cygun-Regular.ttf") format("truetype");
    font-weight: 400;
    font-style: normal;
    font-display: swap;
  }
  @font-face {
    font-family: "Cygun";
    src: url("./assets/fonts/cygun/Cygun-Bold.ttf") format("truetype");
    font-weight: 700;
    font-style: normal;
    font-display: swap;
  }
  @font-face {
    font-family: "Play";
    src: url("./assets/fonts/play/Play-Regular.woff2") format("woff2");
    font-weight: 400;
    font-style: normal;
    font-display: swap;
  }
  @font-face {
    font-family: "Play";
    src: url("./assets/fonts/play/Play-Bold.woff2") format("woff2");
    font-weight: 700;
    font-style: normal;
    font-display: swap;
  }
  @font-face {
    font-family: "Inter";
    src: url("./assets/fonts/inter/InterVariable.woff2") format("woff2");
    font-weight: 100 900;
    font-style: normal;
    font-display: swap;
  }
  :root {
    --bg: #000000;
    --brand-bg: #000000;
    --panel: #1d1d1d;
    --panel-2: #252525;
    --inset: #121212;
    --text: #fafafa;
    --muted: #8e9e99;
    --accent: #60d0a8;
    --accent-2: #38a898;
    --accent-bg: #228855;
    --accent-glow: rgba(96, 208, 168, 0.22);
    --warn: #f5b942;
    --warn-bg:rgb(167, 66, 3);
    --danger: #ec4747;
    --good: #60d0a8;
    --line: #5a7a70;
  }
  section {
    background-color: var(--bg);
    background-image: radial-gradient(880px 560px at 92% 38%, rgba(0, 80, 87, 0.28) 0%, rgba(96, 208, 168, 0.07) 40%, transparent 72%);
    color: var(--text);
    color-scheme: dark;
    font-family: "Inter", "Aptos", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    font-size: 27px;
    line-height: 1.24;
    padding: 52px 68px 46px;
  }
  h1, h2, h3 {
    color: var(--text);
    font-weight: 700;
    letter-spacing: -0.01em;
  }
  h1 {
    font-family: "Cygun", "Play", "Inter", "Aptos", sans-serif;
    font-size: 52px;
    line-height: 1.08;
    margin-bottom: 18px;
    letter-spacing: 0.02em;
    text-transform: uppercase;
  }
  h2 {
    font-family: "Play", "Cygun", "Play", "Inter", "Aptos", sans-serif;
    font-size: 38px;
    margin: 0 0 22px;
    letter-spacing: 0.01em;
  }
  h3 {
    font-size: 27px;
    margin: 0 0 10px;
    color: var(--accent);
  }
  p { margin: 8px 0 14px; }
  ul, ol { margin-top: 10px; }
  li { margin: 7px 0; }
  strong { color: var(--accent); }
  code {
    background: var(--inset);
    color: #7ce7c2;
    border: 1px solid var(--line);
    border-radius: 5px;
    padding: 0.08em 0.32em;
  }
  pre {
    background: var(--inset);
    border: 1px solid var(--line);
    border-radius: 12px;
    padding: 18px 20px;
    font-size: 21px;
    line-height: 1.25;
    box-shadow: 0 6px 24px rgba(0, 0, 0, 0.4);
  }
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 20px;
  }
  th {
    color: var(--accent);
    text-align: left;
    border-bottom: 2px solid var(--accent);
    padding: 9px 12px;
  }
  td {
    border-bottom: 1px solid var(--line);
    padding: 9px 12px;
    vertical-align: top;
  }
  section table { width: auto !important; max-width: 100% !important; margin: 0 auto; background: transparent !important; }
  section table th { background: var(--panel-2) !important; color: var(--accent) !important; border-bottom: 2px solid var(--accent) !important; }
  section table td { background: var(--panel) !important; color: var(--text) !important; border-bottom: 1px solid var(--line) !important; }
  footer {
    color: var(--accent);
    font-size: 14px;
    letter-spacing: 0.04em;
  }
  section::after {
    color: var(--accent);
    font-size: 14px;
  }
  .lead {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-image:
      radial-gradient(720px 520px at 12% 88%, rgba(0, 80, 87, 0.35) 0%, transparent 70%),
      radial-gradient(900px 620px at 96% 40%, rgba(56, 168, 152, 0.28) 0%, rgba(96, 208, 168, 0.08) 42%, transparent 75%);
  }
  .lead h1 {
    font-size: 56px;
    max-width: 1100px;
    color: #ffffff;
    letter-spacing: 0.03em;
  }
  .subtitle {
    font-family: "Play", "Cygun", "Play", "Inter", "Aptos", sans-serif;
    color: var(--muted);
    font-size: 28px;
    max-width: 980px;
    line-height: 1.3;
  }
  .kicker {
    color: var(--accent);
    font-size: 20px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.14em;
  }
  .speaker {
    margin-top: 34px;
    color: var(--accent);
    font-size: 22px;
  }
  .big {
    font-family: "Play", "Cygun", "Play", "Inter", "Aptos", sans-serif;
    font-size: 32px;
    font-weight: 700;
    line-height: 1.12;
  }
  .center { text-align: center; }
  .muted { color: var(--muted); }
  .small { font-size: 20px; }
  .tiny { font-size: 16px; }
  .accent { color: var(--accent); }
  .warn { color: var(--warn); }
  .danger { color: var(--danger); }
  .good { color: var(--good); }
  .two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 26px; align-items: stretch; }
  .three-col { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; align-items: stretch; }
  .card {
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 14px;
    padding: 20px 22px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.35);
  }
  .card p:last-child, .card ul:last-child { margin-bottom: 0; }
  .card.danger-card {
    border-color: rgba(236, 71, 71, 0.7);
    background: linear-gradient(180deg, rgba(236, 71, 71, 0.1) 0%, var(--panel) 100%);
  }
  .card.warn-card {
    border-color: rgba(245, 185, 66, 0.7);
    background: linear-gradient(180deg, rgba(245, 185, 66, 0.1) 0%, var(--panel) 100%);
  }
  .card.good-card {
    border-color: var(--accent);
    background: linear-gradient(180deg, rgba(96, 208, 168, 0.1) 0%, var(--panel) 100%);
    box-shadow: inset 0 0 28px rgba(96, 208, 168, 0.12), 0 0 16px rgba(96, 208, 168, 0.1);
  }
  .incident , .baloon {
    display: inline-block;
    color: var(--warn);
    border: 1px solid rgba(245, 185, 66, 0.5);
    background: rgba(96, 87, 68, 0.08);
    border-radius: 999px;
    padding: 5px 12px;
    margin-bottom: 14px;
    font-size: 17px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }
  .pure-arrow {

    display: inline-block;
    color: var(--muted);
    font-size: 17px;
    font-weight: 700;
    border: 1px solid transparent;
    border-radius: 999px;
    padding: 5px 12px;

  }
  .tag {
    display: inline-block;
    border: 1px solid var(--line);
    background: rgba(255, 255, 255, 0.02);
    border-radius: 999px;
    color: var(--muted);
    font-size: 17px;
    padding: 5px 11px;
    margin: 3px 5px 3px 0;
  }
  .flow {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    margin: 26px 0;
    flex-wrap: nowrap;
  }
  .node {
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 11px;
    padding: 14px 16px;
    text-align: center;
    min-width: 118px;
    font-size: 21px;
  }
  .node.accent-node {
    border-color: var(--accent);
    color: var(--accent);
    box-shadow: 0 0 16px rgba(96, 208, 168, 0.22);
  }
  .node.warn-node {
    border-color: var(--warn);
    background-color: var(--warn-bg)
  }
  .node.danger-node {
    border-color: var(--danger);
    color: var(--danger);
  }
  .node.good-node {
    border-color: var(--good);
    color: var(--good);
  }
  .arrow { color: var(--muted); font-size: 28px; }
  .rail {
    background: linear-gradient(90deg, rgba(0, 80, 87, 0.35) 0%, rgba(29, 29, 29, 0.95) 100%);
    border: 1px solid rgba(96, 208, 168, 0.45);
    border-radius: 10px;
    padding: 12px 18px;
    margin: 16px 0;
    text-align: center;
    color: var(--accent);
    font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
    font-size: 20px;
    box-shadow: 0 0 20px rgba(96, 208, 168, 0.1);
  }
  .timeline {
    display: grid;
    grid-template-columns: 170px 1fr;
    gap: 8px 18px;
    align-items: center;
    margin-top: 18px;
  }
  .timeline.big-one {
    grid-template-columns:  200px 1fr;  
  }
  .time {
    color: var(--accent);
    font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
    font-weight: 600;
  }
  .time.danger {
    color: var(--danger);
  }
  .event {
    background: var(--panel);
    border: 1px solid var(--line);
    border-left: 4px solid var(--accent-2);
    border-radius: 8px;
    padding: 10px 14px;
  }
  .event.warn-event {
    border-left-color: var(--warn);
    background: linear-gradient(90deg, rgba(245, 185, 66, 0.1) 0%, var(--panel) 100%);
  }
  .event.danger-event {
    border-left-color: var(--danger);
    background: linear-gradient(90deg, rgba(236, 71, 71, 0.1) 0%, var(--panel) 100%);
  }
  .event.good-event {
    border-left-color: var(--good);
  }
  .section-slide {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  .section-slide h2 { font-size: 50px; }
  .section-slide p { color: var(--muted); font-size: 29px; }
  .quote {
    border-left: 5px solid var(--accent);
    padding: 8px 0 8px 22px;
    font-size: 34px;
    line-height: 1.25;
  }
  .equation {
    font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
    font-size: 44px;
    text-align: center;
    color: var(--accent);
    margin: 28px 0;
  }
  .bespoke-progress-bar,
  .bespoke-marp-presenter-dragbar-container { background: #60d0a8 !important; }
  svg.bespoke-marp-slide.bespoke-marp-active { --bov-selected: #60d0a8; }
  @media print {
    section {
      background-color: #000000 !important;
      background-image: none !important;
    }
    .card,
    .card.danger-card,
    .card.warn-card,
    .card.good-card,
    .event,
    .event.warn-event,
    .event.danger-event {
      background-color: var(--panel) !important;
      background-image: none !important;
      box-shadow: none !important;
    }
    .rail,
    .incident,
    .tag {
      background-color: var(--inset) !important;
      background-image: none !important;
      box-shadow: none !important;
    }
    .node.accent-node,
    pre {
      box-shadow: none !important;
    }
    section table {
      background-color: #000000 !important;
    }
  }
---

<!-- _class: lead -->
<!-- _paginate: false -->

<div class="kicker">AIBA 2026 · Cloud & AI · 21 October</div>

# AI Agents Need Boundaries

<div class="subtitle">Controlling Cost, Actions, and Accountability in Production</div>

<div class="speaker">Mikalai Saskavets · Python & GenAI Engineer · Coherent Solutions</div>

---

<div class="incident">Сustomer incident</div>

## One task reached 55 repair rounds

<div class="rail">55 attempts · no validated result · no outcomes</div>

---

## What this task does

<div class="flow">
  <div class="node">Core Product</div><div class="arrow">→</div>
  <div class="node">Core Product<br> Changes</div><div class="arrow">→</div>
  <div class="node accent-node">Prepare fix</div><div class="arrow">→</div>
  <div class="node accent-node">Apply fix</div><div class="arrow">→</div>
  <div class="node">Customer's<br> Custom Product<br> Version</div>
</div>

---

## One fix met different customer code

| Target | How commission logic differs |
|---|---|
| Core service | Fully refunded orders earn no base commission |
| Customer A | Calculates commission from invoices |
| Customer B | Refunds appear as a `REVERSAL` flow |
| Customer C | A local VIP adjustment must remain intact |

<div class="rail">
  <br>
    12 core changes × 18 target versions = 216 candidate tasks per month
  <br>&nbsp;
</div>

---

## Customer B used a different refund signal

```python
Expected behavior: fully refunded order → base commission 0.0
Customer B data:  flow = 'REVERSAL'
Wrong patch:      checks kind = 'refund'
Test result:      expected 0.0, got 7.0
```

<div class="quote">The patch changed code, but the refund rule stayed wrong.</div>

---

## Repeated attempts with no improvement

<div class="timeline">
  <div class="time">Round 1</div><div class="event warn-event">Changed patch; refund test fails</div>
  <div class="time">Round 5</div><div class="event warn-event">Changed patch; same failure</div>
  <div class="time">Round 25</div><div class="event warn-event">Changed patch; same failure</div>
  <div class="time">Round 55</div><div class="event danger-event">Same failure; human cancels agent's job</div>
</div>

<div class="rail">The worker counted attempts but did not compare test outcomes.</div>

---

## A repeated result triggers a stop

<div class="rail">Same failure + no new passing tests for 3 rounds → stop</div>

```python
attempt 1: 12 pass, 1 fail  (expected 0.0, got 7.0)
attempt 2: 12 pass, 1 fail  (expected 0.0, got 7.0) # <- same failure
attempt 3: 12 pass, 1 fail  (expected 0.0, got 7.0) # <- same failure
outcome: NO_PROGRESS_LIMIT_EXCEEDED
```

---

## A repeated result triggers a stop

<div class="rail">Same failure + no new passing tests for 3 rounds → stop</div>

```python
attempt 1: 11 pass, 2 fail  (expected 0.0, got 7.0), (expected: 'good', got 'bad')
attempt 2: 11 pass, 2 fail  (expected 0.0, got 7.0), (expected: 'good', got 'bad') # <- same failures
attempt 1: 12 pass, 1 fail  (expected 0.0, got 7.0) # <- have some progress, reset attempts counter
attempt 2: 12 pass, 1 fail  (expected 0.0, got 7.0) # <- same failure
attempt 3: 12 pass, 1 fail  (expected 0.0, got 7.0) # <- same failure 
outcome: NO_PROGRESS_LIMIT_EXCEEDED
```

---

## Resource limits cover the whole task

| Level | Example limit |
|---|---|
| Step / Attempt | Model tokens or test runtime |
| Run | Total attempts and a fixed deadline |
| Task | Total budget across queue retries |
| Campaign | Shared budget across customer targets |

<div class="rail">Reserve before work starts. Record actual use after it ends.</div>

---

## Four boundaries for agent work

<div class="timeline">
  <div class="time">Action</div><div class="event">Which tools and targets may the agent use?</div>
  <div class="time danger">Resource</div><div class="event">How much time and cost may this work consume?</div>
  <div class="time">Evidence</div><div class="event">What record/artifact will explain each important action?</div>
  <div class="time">Handoff</div><div class="event">When must the worker stop or ask a person?</div>
</div>

<p class="small muted">The worker enforces these rules around the model's proposals.</p>

---

<div class="baloon">Action</div>

## The worker owns tool permission

<div class="flow">
  <div class="node">Model proposes</div><div class="arrow">→</div>
  <div class="node accent-node">Worker checks policy</div>
</div>

<div class="two-col">
  <div class="card good-card"><h3>ALLOW</h3><p>Execute and record the result.</p></div>
  <div class="card danger-card"><h3>DENY</h3><p>Record the denial. Do not execute.</p></div>
</div>

<p class="small muted">The task defines allowed paths, commands, and target.</p>

---

<div class="baloon">Action</div>

## Running tests executes customer code

<div class="timeline">
  <div class="time">Workspace</div><div class="event">Disposable checkout at a recorded commit</div>
  <div class="time">Process</div><div class="event">Restricted network, CPU, memory, and time</div>
  <div class="time">Secrets</div><div class="event">No production credentials in the test environment</div>
</div>

---

<div class="baloon">Evidence</div>

## One run connects the evidence

| Record | Question it answers |
|---|---|
| Task packet | What work and scope were approved? |
| Trace and test artifact | What happened in what order, and what failed? |
| Tool action ledger | What was requested, allowed, and executed? |
| Budget account | How much did the work consume? |

<div class="rail">Local check: run-1842 connects attempts, results, and the final stop</div>

---

<div class="baloon">Evidence</div>
<div class="pure-arrow">→</div><div class="baloon">Handoff</div>

## Customer B stops with evidence

<div class="two-col">
  <div class="card warn-card"><h3>Controlled run outcome</h3><p><code>NO_PROGRESS_LIMIT_EXCEEDED</code></p><p class="small">No validated patch. No draft PR.</p></div>
  <div class="card good-card"><h3>Proposed owner handoff</h3><p class="small">Target commit, last diff, failed tests, trace, tool records, and used budget.</p></div>
</div>

<div class="rail">A person decides whether to fix the rule or authorize a scoped new run.</div>

---

<div class="baloon">Handoff</div>

## People own code acceptance and release

<div class="flow">
  <div class="node">Draft PR</div><div class="arrow">→</div>
  <div class="node">Ready for review</div><div class="arrow">→</div>
  <div class="node accent-node">Checks + owner review</div><div class="arrow">→</div>
  <div class="node good-node">Human merge</div><div class="arrow">→</div>
  <div class="node">Deploy</div>
</div>

<div class="rail">Agent execution, merged code, and customer rollout are separate milestones.</div>

---

## One campaign has several outcomes

| Campaign outcome across 18 targets | Count |
|---|---:|
| Validated draft PR | 9 |
| Already fixed | 3 |
| Not affected | 2 |
| Human adaptation needed | 2 |
| Budget exceeded | 1 |
| Test environment unavailable | 1 |

<div class="rail">Nine draft PRs are review work, not nine deployed fixes.</div>

---

## Four questions for a design review

<div class="timeline">
  <div class="time">Action</div><div class="event">Who checks tool permission before execution?</div>
  <div class="time">Resource</div><div class="event">Where are run and campaign limits reserved?</div>
  <div class="time">Evidence</div><div class="event">Can the collected artifacts explain requests, decisions, results, and cost?</div>
  <div class="time">Handoff</div><div class="event">Which result stops work, and who owns the next step?</div>
</div>

<div class="rail">A useful agent can finish, stop, or ask for help with a clear reason.</div>

---

<!-- _class: lead -->

<div class="kicker">AIBA 2026 · Questions</div>

# Thank you

