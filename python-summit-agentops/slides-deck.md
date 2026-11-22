---
marp: true
paginate: true
size: 16:9
theme: default
title: "AgentOps in Python: Trace, Bound, and Audit AI Agent Runs Before They Fail"
author: "Mikalai Saskavets"
description: "Python Summit 2026 conference deck"
footer: "Python Summit 2026 · Mikalai Saskavets"
style: |
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
    --bg: #150601;
    --brand-bg: #321206;
    --panel: #321206;
    --panel-2: #4a1c0c;
    --inset: #220d05;
    --text: #fffcf8;
    --muted: #e4d3c8;
    --accent: #ff5d25;
    --accent-2: #ffb089;
    --accent-bg: #992d15;
    --warn: #fff907;
    --warn-bg: rgb(167, 66, 3);
    --danger: #ff6d6d;
    --good: #c6e07a;
    --line: #a85c36;
  }
  section {
    background: var(--bg);
    color: var(--text);
    color-scheme: dark;
    font-family: "Aptos", "Inter", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    font-size: 27px;
    line-height: 1.24;
    padding: 52px 68px 46px;
    --color-prettylights-syntax-keyword: #ff5d25 !important;
    --color-prettylights-syntax-entity: #fff6ee !important;
    --color-prettylights-syntax-constant: #ffc9a8 !important;
    --color-prettylights-syntax-string: #ffe56a !important;
    --color-prettylights-syntax-variable: #ffb089 !important;
    --color-prettylights-syntax-comment: #c4a090 !important;
    --color-prettylights-syntax-storage-modifier-import: #fff6ee !important;
    --color-prettylights-syntax-entity-tag: #ff8a55 !important;
    --color-prettylights-syntax-string-regexp: #ffb089 !important;
    --color-prettylights-syntax-markup-list: #ffe56a !important;
    --color-prettylights-syntax-meta-diff-range: #ff8a55 !important;
    --color-prettylights-syntax-constant-other-reference-link: #ffd0bc !important;
  }
  h1, h2, h3 { color: var(--text); font-weight: 400; letter-spacing: -0.02em; }
  h1 {
    font-family: "Play", "Inter", "Aptos", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    font-size: 52px;
    line-height: 1.08;
    margin-bottom: 18px;
  }
  h2 { font-size: 38px; margin: 0 0 22px; }
  h3 { font-size: 27px; margin: 0 0 10px; color: var(--accent); }
  p { margin: 8px 0 14px; }
  ul, ol { margin-top: 10px; }
  li { margin: 7px 0; }
  strong { color: var(--accent); }
  code {
    background: var(--inset);
    color: #fff6ee;
    border-radius: 5px;
    padding: 0.08em 0.28em;
  }
  pre {
    background: var(--inset);
    border: 1px solid var(--line);
    border-radius: 12px;
    padding: 18px 20px;
    font-size: 21px;
    line-height: 1.25;
    box-shadow: none;
  }
  section.adapter-slide pre { font-size: 18px; line-height: 1.2; padding: 14px 18px; }
  section.adapter-slide h2 { margin-bottom: 12px; }
  section.adapter-slide p { margin: 6px 0 8px; }
  section :is(pre, marp-pre) :where(.hljs-doctag, .hljs-keyword, .hljs-type, .hljs-template-tag, .hljs-template-variable, .hljs-variable.language_) { color: #ff5d25 !important; }
  section :is(pre, marp-pre) :where(.hljs-title, .hljs-title.class_, .hljs-title.function_) { color: #fff6ee !important; }
  section :is(pre, marp-pre) :where(.hljs-attr, .hljs-attribute, .hljs-literal, .hljs-meta, .hljs-number, .hljs-operator, .hljs-variable) { color: #ffc9a8 !important; }
  section :is(pre, marp-pre) :where(.hljs-string, .hljs-regexp) { color: #ffe56a !important; }
  section :is(pre, marp-pre) :where(.hljs-built_in, .hljs-symbol) { color: #ffb089 !important; }
  section :is(pre, marp-pre) :where(.hljs-comment, .hljs-code) { color: #c4a090 !important; }
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 21px;
  }
  th {
    color: var(--accent);
    text-align: left;
    border-bottom: 2px solid var(--line);
    padding: 8px 10px;
  }
  td {
    border-bottom: 1px solid var(--line);
    padding: 8px 10px;
    vertical-align: top;
  }
  section table { width: auto !important; max-width: 100% !important; margin: 0 auto; background: transparent !important; }
  section table th { background: var(--panel-2) !important; color: var(--accent) !important; }
  section table td { background: var(--panel) !important; color: var(--text) !important; }
  footer { color: var(--accent); font-size: 14px; }
  section::after { color: var(--accent); font-size: 14px; }
  .lead { display: flex; flex-direction: column; justify-content: center; }
  .lead h1 { font-size: 58px; max-width: 1100px; }
  .subtitle { color: var(--muted); font-size: 29px; max-width: 980px; }
  .kicker { color: var(--accent); font-size: 20px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; }
  .speaker { margin-top: 34px; color: var(--accent); font-size: 22px; }
  .big { font-size: 46px; font-weight: 700; line-height: 1.12; }
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
  }
  .card p:last-child, .card ul:last-child { margin-bottom: 0; }
  .card.danger-card { border-color: #b8554c; }
  .card.warn-card { border-color: #a6862a; }
  .card.good-card { border-color: #6d7a38; }
  .tag {
    display: inline-block;
    border: 1px solid var(--line);
    border-radius: 999px;
    color: var(--muted);
    font-size: 17px;
    padding: 5px 10px;
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
  .nobr { white-space: nowrap; }
  .node.accent-node { border-color: var(--accent); background-color: var(--accent-bg); }
  .node.warn-node { 
    border-color: var(--warn); 
    background-color: var(--warn-bg);
  }
  .arrow { color: var(--muted); font-size: 28px; }
  .rail {
    background: var(--inset);
    border: 1px solid var(--line);
    border-radius: 10px;
    padding: 11px 16px;
    margin: 16px 0;
    text-align: center;
    color: var(--accent);
    font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
    font-size: 20px;
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
  .time { color: var(--muted); font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; }
  .event { background: var(--panel); border-left: 4px solid var(--accent-2); border-radius: 8px; padding: 10px 14px; }
  .event.warn-event { border-left-color: var(--warn); }
  .event.danger-event { border-left-color: var(--danger); }
  .section-slide { display: flex; flex-direction: column; justify-content: center; }
  .section-slide h2 { font-size: 50px; }
  .section-slide p { color: var(--muted); font-size: 29px; }
  .state-row { display: flex; align-items: center; justify-content: center; gap: 10px; margin: 18px 0; }
  .state {
    border: 1px solid var(--line);
    border-radius: 10px;
    background: var(--panel);
    padding: 12px 16px;
    font-size: 20px;
    text-align: center;
  }
  .state.good-state { border-color: var(--good); }
  .state.warn-state { border-color: var(--warn); }
  .state.danger-state { border-color: var(--danger); }
  .quote {
    border-left: 5px solid var(--accent);
    padding: 8px 0 8px 22px;
    font-size: 34px;
    line-height: 1.25;
  }
  .footnote { position: absolute; left: 68px; bottom: 48px; color: var(--muted); font-size: 16px; }
  .bespoke-progress-bar,
  .bespoke-marp-presenter-dragbar-container { background: #ff5d25 !important; }
  svg.bespoke-marp-slide.bespoke-marp-active { --bov-selected: #ff5d25; }
  section.brand {
    background: var(--brand-bg);
    display: grid;
    grid-template-columns: minmax(0, 1.02fr) minmax(0, 0.98fr);
    column-gap: 28px;
    align-items: start;
    padding: 8px 28px 48px 56px;
  }
  section.brand .brand-copy {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    min-width: 0;
    padding: 72px 12px 0 0;
  }
  section.brand h1 {
    margin: 0 0 20px;
    max-width: none;
    font-size: 66px;
    font-weight: 400;
    line-height: 1.14;
    letter-spacing: -0.03em;
  }
  section.brand .brand-desc {
    margin: 0 0 40px;
    max-width: 470px;
    color: #d9cdc6;
    font-size: 22px;
    line-height: 1.3;
  }
  section.brand .brand-name,
  section.brand .brand-role {
    margin: 0;
    color: var(--accent);
    font-family: "Play", "Inter", "Aptos", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    font-weight: 400;
    line-height: 1.15;
  }
  section.brand .brand-name { font-size: 34px; margin-bottom: 18px; }
  section.brand .brand-role { font-size: 22px; }
  section.brand .brand-art {
    display: block;
    width: auto;
    height: 648px;
    max-width: 100%;
    margin: 0;
    justify-self: end;
    object-fit: contain;
    object-position: right top;
    background: transparent;
  }
  section.brand-end .brand-copy { padding-top: 64px; }
  section.brand-end h1 {
    color: var(--accent);
    font-size: 64px;
    margin-bottom: 20px;
  }
  section.brand-end .brand-note {
    margin: 0;
    max-width: 520px;
    color: var(--accent);
    font-size: 26px;
    line-height: 1.32;
  }
  section.brand footer {
    left: 96px;
    bottom: 20px;
    color: var(--accent);
    font-size: 16px;
  }
  section.brand::after {
    left: 56px;
    right: auto;
    bottom: 20px;
    color: var(--accent);
    font-size: 16px;
  }
---

<!-- _class: brand -->
<!-- _footer: "Event organized by: Academic Partners Foundation" -->

<div class="brand-copy">
  <h1>AgentOps<br>in Python</h1>
  <p class="brand-desc">Trace, Bound, and Audit AI Agent Runs Before They Fail</p>
  <p class="brand-name">Mikalai Saskavets</p>
  <p class="brand-role">Python &amp; GenAI Engineer, Coherent Solutions</p>
</div>
<img class="brand-art" src="./assets/python_summit_first_slide_image.png" alt="Python Summit, Warsaw, 19–20 October 2026">

---

## One core fix, many customer implementations

<p class="big">A core service changed → Need to deliver changes to customers' copies.</p>

<div class="timeline">
  <div class="time">core team</div><div class="event">Fix a commission calculation in the reference Python service</div>
  <div class="time">client teams</div><div class="event">Own customer workflows, tests, release dates, and business exceptions</div>
  <div class="time">worker</div><div class="event">Investigate applicability, adapt the fix, and prepare review evidence</div>
</div>

<p class="small muted">The copied services reflect years of customer-specific changes.</p>

---

## The task volume

<div class="rail">
  54 customers · about 540 microservices instances ⥤ 
  <br><br>
  12 changes × 18 targets = 
  <br><br>
  <big>216 candidate tasks per month</big>
</div>

<p class="small muted"><br><br>One candidate may produce a draft PR, a documented no-op, or an escalation.</p>

---

## The same intent needs different patches

| Target | Location of commission logic | Possible result |
|---|---|---|
| Customer A | Invoice-shaped Python calculation | Adapt the core test and patch |
| Customer B | Workflow step with a different refund state | Inspect the workflow and adapt the condition |
| Customer C | Different data model | Requires a different adaptation |
| Customer E | Feature not used | Record NOT_APPLICABLE |

<p class="small muted">A clean cherry-pick would not establish equivalent behavior.</p>

---

## Customer B received a clear task

<div class="two-col">
  <div class="card"><h3>Core intent</h3><p class="small">Exclude a fully refunded order from base commission.</p><p class="small">Core commit and regression test identify the change.</p></div>
  <div class="card"><h3>Customer representation</h3><p class="small">A refund uses <code>flow='REVERSAL'</code>.</p><p class="small">Client engineers own the final interpretation.</p></div>
</div>

<div class="rail">Input: core change ID, target commit, allowed paths, test commands, owner</div>

---

## The worker owned the execution path

<div class="flow">
  <div class="node">Task registry</div><div class="arrow">→</div>
  <div class="node">Celery</div><div class="arrow">→</div>
  <div class="node accent-node">Python worker</div><div class="arrow">→</div>
  <div class="node">Draft PR or escalation</div>
</div>

<p>Proposed worker: isolated checkout, model calls, patch application, local checks, trace spans, budget decisions, tool records.</p>
<p class="small muted">Reference architecture: GPT-4.1, Celery, RabbitMQ, PostgreSQL, GitHub App, OpenTelemetry.</p>

---

<!-- _class: adapter-slide -->

## The patch loop around Customer B

```python
assert MAX_PATCH_ATTEMPTS > 0
last_test = None
for attempt in range(MAX_PATCH_ATTEMPTS):
    evidence = read_allowed_files(worktree)
    patch = model.propose_patch(task, evidence, last_test)
    validate_paths(patch, allowed_paths)
    apply_patch(worktree, patch)
    last_test = run_pytest(worktree, deadline)
    if last_test.passed:
        return checked_commit(worktree)
return escalate(last_test)
```

<p class="small warn">The model proposes code. Python enforces path scope and owns every tool call.</p>

---

## Customer B kept failing the same test

<div class="timeline">
  <div class="time nobr">attempt 1</div><div class="event warn-event">Patch checked <code>kind='refund'</code>; pytest still saw commission 7.5</div>
  <div class="time nobr">attempt 2</div><div class="event warn-event">Another patch; same failing test and no new tests passed</div>
  <div class="time nobr">attempt 3</div><div class="event warn-event">Another patch; same failure signature</div>
  <div class="time">early design</div><div class="event danger-event">Without a progress check, retries could continue to the attempt cap</div>
</div>

---

## One run ID connects the evidence

```python
run_id = run-1842       core_change = core-fix-17
attempt 1: patch 26e019...  1 pass, 1 fail
attempt 2: patch 983444...  1 pass, 1 fail
attempt 3: patch 18bb4a...  1 pass, 1 fail
failure: test_refund_has_zero_commission
         expected 0.0, got 7.5
result: NO_PROGRESS_LIMIT_EXCEEDED; draft PR = false
```

---

## The span tree shows the loop

```python
propagate run-1842
  checkout customer-b
  attempt 1: model.call → patch.apply → test.run
  attempt 2: model.call → patch.apply → test.run
  attempt 3: model.call → patch.apply → test.run
  stop: NO_PROGRESS_LIMIT_EXCEEDED
```

<p class="small">Span attributes: run ID, change ID, target commit, attempt, tool, exit code, failure signature.</p>
<p class="small muted">Proposed OpenTelemetry layout.</p>

---

## The third repeated failure changed the decision

<div class="rail">same failure set + no newly passing tests for 3 attempts → NO_PROGRESS_LIMIT_EXCEEDED</div>

```python
if same_failure_streak >= 3 and newly_passing_tests == 0:
    stop_run("NO_PROGRESS_LIMIT_EXCEEDED")
    preserve(patches, pytest_results, trace_id)
    route_to_customer_owner(task)
```

---

## The budget was reserved before each step

| Limit | Worker decision for Customer B |
|---|---|
| Model calls and tokens | Reserve estimated headroom before the next request |
| Pytest runtime | Start only if its deadline fits inside the run deadline |
| Patch attempts | Stop at the configured maximum |
| Campaign budget | Do not start another target when the shared cap is exhausted |

---

## Customer B stopped with evidence

<div class="rail">NO_PROGRESS_LIMIT_EXCEEDED</div>

<div class="timeline big-one">
  <div class="time">reproduced failure</div><div class="event">Three patch hashes, the repeated test result, and a stop event</div>
  <div class="time">owner handoff</div><div class="event">Include target commit, patch diffs, protected output, and trace ID</div>
  <div class="time">task state</div><div class="event">Customer B stays pending for its client engineer; no draft PR</div>
</div>

---

## Customer A passed its local checks

<div class="timeline big-one">
  <div class="time">adaptation</div><div class="event">The invoice-shaped variant contains the core refund fix</div>
  <div class="time">local checks</div><div class="event">Two tests passed on the representative variant</div>
  <div class="time">PR decision</div><div class="event">Passing checks make the change a candidate for a draft PR</div>
  <div class="time">review path</div><div class="event">Push a checked branch, create a draft PR, then request owner review</div>
</div>

<p class="small muted"><br>Passing tests provide limited evidence for a future PR.</p>

---

## Customer C needed a deeper test

<p class="big">Two ordinary tests passed. The customer invariant test failed.</p>

<div class="two-col">
  <div class="card"><h3>Patch evidence</h3><p class="small">The core refund behavior looked correct under ordinary tests.</p></div>
  <div class="card"><h3>Customer rule</h3><p class="small">An additional test detected a lost VIP adjustment.</p></div>
</div>

<p class="small muted">The customer-specific check blocks a draft PR for Customer C.</p>

---

## The campaign was more than a PR count

| Outcome across 18 targets | Count |
|---|---:|
| Validated draft PR | 9 |
| Already had equivalent fix | 3 |
| Not affected | 2 |
| Needs client engineer | 2 |
| Budget exceeded | 1 |
| Test environment unavailable | 1 |
| TOTAL | 18 |

---

## The stopped task changed campaign state

<div class="timeline">
  <div class="time">Customer B</div><div class="event warn-event">NEEDS_HUMAN_INTERVENTION; no PR and no release claim</div>
  <div class="time">Customer A</div><div class="event">Local checks passed; PR_CREATED requires a draft confirmed by GitHub</div>
  <div class="time">campaign</div><div class="event">Check remaining allowance before starting the next target</div>
</div>

<p class="small muted">Run completion, PR acceptance, merge, and release are separate outcomes.</p>

---

## Different failure modes, different controls

| Failure mode | Control |
|---|---|
| The same test failure repeats | Stop on no progress; preserve patches and test output |
| Ordinary tests miss a customer rule | Run customer-specific checks; request owner review |
| Parallel tasks consum e the campaign budget | Reserve against a shared limit before dispatch |

---

## The next pilot gate follows the evidence

<div class="timeline">
  <div class="time">run</div><div class="event">Trace shows repeated failures and the enforced stop reason</div>
  <div class="time">tool</div><div class="event">Ledger agrees with actual process results and policy decisions</div>
  <div class="time">change</div><div class="event">Customer owner accepts the behavioral test and reviewed diff</div>
  <div class="time">system</div><div class="event">Crash, concurrency, budget, and GitHub unknown-result paths pass integration tests</div>
</div>

---

## Operational checklist for the next run

<div class="timeline">
  <div class="time">identity</div><div class="event">Keep one run ID across the queue, model, tools, tests, and handoff. Link protected artifacts from the trace.</div>
  <div class="time">tool</div><div class="event">Record the request, policy decision, and result. Use a stable key for each intended external write.</div>
  <div class="time">limits</div><div class="event">Reserve time, tokens, and cost before dispatch. Stop on no progress; reconcile UNKNOWN before another write.</div>
  <div class="time">handoff</div><div class="event">Preserve the checked diff and failed tests for the owner. Add a regression test and an evaluation case.</div>
</div>

---

<!-- _class: brand brand-end -->
<!-- _footer: "Event organized by: Academic Partners Foundation" -->

<div class="brand-copy">
  <h1>Thank you<br>for watching!</h1>
  <p class="brand-note">Remember to leave your questions<br>and rate the presentation<br>in the section below.</p>
</div>
<img class="brand-art" src="./assets/python_summit_last_slide_image.png" alt="Python Summit and Academic Partners">

