---
marp: true
paginate: true
size: 16:9
theme: default
title: "When AI Agents Fail in Production: Tracing, Budgets, and Tool Execution Ledgers"
author: "Mikalai Saskavets"
description: "DevAI 2026 conference deck"
footer: "DevAI 2026 · Mikalai Saskavets"
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
    --bg: #0e0111;
    --brand-bg: #24042b;
    --panel: #2a0733;
    --panel-2: #3b0c47;
    --inset: #1a0420;
    --text: #fdf7ff;
    --muted: #dccae3;
    --accent: #d819fd;
    --accent-2: #ec9bff;
    --accent-bg: #9919fd;
    --warn: #ffc65c;
    --warn-bg: rgb(167, 66, 3);
    --danger: #ff6464;
    --good: #3fdcc0;
    --line: #9440a8;
  }
  section {
    background: var(--bg);
    color: var(--text);
    color-scheme: dark;
    font-family: "Aptos", "Inter", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    font-size: 27px;
    line-height: 1.24;
    padding: 52px 68px 46px;
  }
  h1, h2, h3 {
    color: var(--text);
    font-weight: 400;
    letter-spacing: -0.02em;
  }
  h1 {
    font-family: "Play", "Inter", "Aptos", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    font-size: 52px;
    line-height: 1.08;
    margin-bottom: 18px;
  }
  h2 {
    font-size: 38px;
    margin: 0 0 22px;
  }
  h3 {
    font-size: 27px;
    margin: 0 0 10px;
    color: var(--accent);
  }
  p {
    margin: 8px 0 14px;
  }
  ul, ol {
    margin-top: 10px;
  }
  li {
    margin: 7px 0;
  }
  strong {
    color: var(--accent);
  }
  code {
    background: var(--inset);
    color: #fbeaff;
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
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 20px;
  }
  th {
    color: #e04dff;
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
  section table th { background: var(--panel-2) !important; color: #e04dff !important; }
  section table td { background: var(--panel) !important; color: var(--text) !important; }
  footer {
    color: var(--accent);
    font-size: 14px;
  }
  section::after {
    color: var(--accent);
    font-size: 14px;
  }
  .big {
    font-size: 46px;
    font-weight: 700;
    line-height: 1.12;
  }
  .center {
    text-align: center;
  }
  .muted {
    color: var(--muted);
  }
  .small {
    font-size: 20px;
  }
  .tiny {
    font-size: 16px;
  }
  .accent {
    color: var(--accent);
  }
  .warn {
    color: var(--warn);
  }
  .danger {
    color: var(--danger);
  }
  .good {
    color: var(--good);
  }
  .two-col {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 26px;
    align-items: stretch;
  }
  .three-col {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 18px;
    align-items: stretch;
  }
  .four-col {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 14px;
    align-items: stretch;
  }
  .card {
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 14px;
    padding: 20px 22px;
  }
  .card p:last-child,
  .card ul:last-child {
    margin-bottom: 0;
  }
  .card.danger-card {
    border-color: #b84a58;
  }
  .card.warn-card {
    border-color: #a3803a;
  }
  .card.good-card {
    border-color: #26907f;
  }
  .incident {
    display: inline-block;
    color: var(--warn);
    border: 1px solid #a3803a;
    border-radius: 999px;
    padding: 5px 11px;
    margin-bottom: 14px;
    font-size: 17px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
  }
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
  .node.accent-node {
    border-color: var(--accent);
  }
  .node.warn-node {
    border-color: var(--warn);
    background-color: var(--warn-bg)
  }
  .node.danger-node {
    border-color: var(--danger);
  }
  .node.good-node {
    border-color: var(--good);
  }
  .arrow {
    color: var(--muted);
    font-size: 28px;
  }
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
  .time {
    color: var(--muted);
    font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
  }
  .event {
    background: var(--panel);
    border-left: 4px solid var(--accent-2);
    border-radius: 8px;
    padding: 10px 14px;
  }
  .event.warn-event {
    border-left-color: var(--warn);
  }
  .event.danger-event {
    border-left-color: var(--danger);
  }
  .event.good-event {
    border-left-color: var(--good);
  }
  .section-slide {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  .section-slide h2 {
    font-size: 50px;
  }
  .section-slide p {
    color: var(--muted);
    font-size: 29px;
  }
  .state-row {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    margin: 18px 0;
  }
  .state {
    border: 1px solid var(--line);
    border-radius: 10px;
    background: var(--panel);
    padding: 12px 16px;
    font-size: 20px;
    text-align: center;
  }
  .state.good-state {
    border-color: var(--good);
  }
  .state.warn-state {
    border-color: var(--warn);
  }
  .state.danger-state {
    border-color: var(--danger);
  }
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
    color: var(--warn);
    margin: 28px 0;
  }
  .signal {
    border-left: 5px solid var(--danger);
    background: var(--panel);
    border-radius: 8px;
    padding: 13px 16px;
    margin: 10px 0;
  }
  .control {
    border-left: 5px solid var(--good);
    background: var(--panel);
    border-radius: 8px;
    padding: 13px 16px;
    margin: 10px 0;
  }
  .footnote {
    position: absolute;
    left: 68px;
    bottom: 48px;
    color: var(--muted);
    font-size: 16px;
  }
  section.brand {
    background: var(--brand-bg);
    padding: 0;
  }
  section.brand .brand-copy,
  section.brand .brand-person {
    position: absolute;
    left: 89px;
    width: 610px;
  }
  section.brand .brand-copy {
    top: 64px;
  }
  section.brand h1 {
    margin: 0;
    padding: 0;
    border: 0;
    color: var(--text);
    font-size: 69.5px;
    font-weight: 400;
    line-height: 76px;
    letter-spacing: 0;
  }
  section.brand .brand-desc {
    margin: 24px 0 0;
    color: #ffffff;
    font-size: 26.8px;
    line-height: 1.2;
  }
  section.brand .brand-person {
    top: 351px;
  }
  section.brand .brand-name,
  section.brand .brand-role {
    margin: 0;
    color: var(--accent);
    font-family: "Play", "Inter", "Aptos", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
  }
  section.brand .brand-name {
    font-size: 37px;
    line-height: 1.15;
  }
  section.brand .brand-role {
    margin-top: 31px;
    font-size: 24px;
    line-height: 1.2;
  }
  section.brand .brand-art {
    position: absolute;
    top: 0;
    right: 0;
    width: auto;
    height: 720px;
    max-width: none;
    margin: 0;
    background: transparent;
  }
  section.brand-end h1,
  section.brand-end .brand-desc {
    color: var(--accent);
  }
  section.brand footer,
  section.brand::after {
    top: 671px;
    bottom: auto;
    height: 18px;
    padding: 0;
    color: var(--accent);
    font-size: 14.8px;
    line-height: 18px;
  }
  section.brand footer {
    left: 89px;
    right: auto;
  }
  section.brand::after {
    left: 32px;
    right: auto;
  }
---

<!-- _class: brand -->
<!-- _footer: "Event organized by: Academic Partners Foundation" -->

<div class="brand-copy">
  <h1>When AI Agents<br>Fail in Production</h1>
  <p class="brand-desc">Tracing, Budgets, and Tool Execution Ledgers</p>
</div>
<div class="brand-person">
  <p class="brand-name">Mikalai Saskavets</p>
  <p class="brand-role">Python &amp; GenAI Engineer, Coherent Solutions</p>
</div>
<img class="brand-art" src="./assets/devai_first_slide_image.png" alt="DevAI by Data Science Summit, Warsaw, 19–20 October 2026">

---

<div class="incident">Incident · Customer B</div>

## One task reached 25 repair rounds

<div class="timeline">
  <div class="time">Intent</div><div class="event">Adapt a core commission fix to Customer B</div>
  <div class="time">Round 1</div><div class="event warn-event">The refund test fails after the first patch</div>
  <div class="time">Round 25</div><div class="event danger-event">The same refund test still fails</div>
  <div class="time">Result</div><div class="event">Operator cancels. No validated change or draft PR.</div>
</div>

---

## The work crossed divergent customer versions

| Planning scale | Workload assumption |
|---|---|
| 54 enterprise customers | About 540 customer service instances |
| 12 core changes each month | 18 candidate implementations per change |
| 12 × 18 | 216 potential tasks each month |

<div class="rail">A candidate task may end in a PR, a no-op, or a human escalation.</div>

---

## One commission fix had different code paths

| Customer version | Where the behavior lived |
|---|---|
| A | Original calculation function |
| B | A workflow engine with REVERSAL events |
| C | A different order data model |
| E | The affected feature was not used |

<p class="small muted">The core fix excluded refunded orders from earned commission.</p>

---

## The campaign carried a change specification

<div class="two-col">
  <div class="card"><h3>Core evidence</h3><p>Source commit, bug description, and regression test for refunded orders.</p></div>
  <div class="card"><h3>Target context</h3><p>Repository, pinned commit, owning team, known customer rules, and exclusions.</p></div>
</div>

<div class="rail">One task represented one candidate customer implementation.</div>

---

## Customer B encoded refunds as REVERSAL

<pre><code>Expected: refunded orders earn no commission
Target rule: refunds use flow='REVERSAL'
Wrong patch: checks kind='refund' instead
Check: Customer B's focused Python tests
</code></pre>

<div class="quote">The wrong field left the refund bug in place.</div>

---

## The worker boundary for tools and GitHub writes

<div class="flow">
  <div class="node">Change<br>task</div><div class="arrow">→</div>
  <div class="node">Celery<br>queue</div><div class="arrow">→</div>
  <div class="node accent-node">Python<br>worker</div><div class="arrow">→</div>
  <div class="node">Patch and<br>pytest</div><div class="arrow">→</div>
  <div class="node warn-node">Draft PR<br>if valid</div>
</div>

<p class="small">Reference design: GPT-4.1 proposes edits; Python validates tools, limits runs, and owns GitHub App actions.</p>

---

<div class="incident">Selected incident rounds · Customer B</div>

## The same failure survived each patch

| Round | Worker action | Focused pytest result |
|---|---|---|
| 1 | First workflow patch | 1 failed |
| 5 | Another patch | 1 failed, same test |
| 12 | Another patch | 1 failed, same test |
| 25 | Another patch | 1 failed, same test |

<div class="rail">Twenty-five test runs were not twenty-five units of progress.</div>

---

## The test artifact showed repeated behavior

<pre><code>Focused Customer B test suite
exit_code: 1
failed_ids: test_refund_has_zero_commission
failure_group: refund_has_zero_commission
patch_round: 12
</code></pre>

---

## A completion message could hide the failed checks

<div class="two-col">
  <div class="card warn-card"><h3>Representative agent summary</h3><p>"Updated the workflow. Ready for review."</p></div>
  <div class="card danger-card"><h3>Worker evidence</h3><p>Last pytest exit code: 1.<br>The refund test still failed.<br>No draft PR created.</p></div>
</div>

<div class="quote">The platform reported the tool result, not the model's confidence.</div>

---

## The review joined four records by run ID

| Question | Evidence to join |
|---|---|
| What was requested? | Change specification and target commit |
| What happened? | Trace and captured pytest artifacts |
| What was allowed? | Tool execution ledger with policy decisions |
| What was consumed? | Budget account across attempts |

<!-- <p class="small muted">GitHub state answered a fifth question: whether any PR was published.</p> -->

---

## A thin trace could not show repetition

<div class="two-col">
  <div class="card warn-card"><h3>Earlier span</h3><p>shell.execute<br>duration: 18 s<br>status: OK</p></div>
  <div class="card good-card"><h3>Useful span</h3><p>round: 12<br>patch hash: p12<br>pytest exit: 1<br>failure group: refund_has_zero_commission</p></div>
</div>

<div class="rail">An OK tool span meant the command ran; it did not mean the tests passed.</div>

---

## The tool ledger recorded authorization and result

<pre><code>run_id: case-B-25      round: 12
tool: test_runner      command: focused Customer B suite
policy: ALLOW          executed: true
exit_code: 1           output_artifact: test-B-12
target_commit: b72f... patch_hash: p12
</code></pre>

<p class="small muted">Representative ledger record.
 </p>

---

## A denied request still belonged in the ledger

<pre><code>run_id: policy-probe-1
tool: shell
operation: pip install unknown-package
policy_decision: denied
executed: false
</code></pre>

<div class="rail">The local allowlist rejected and recorded the request without running it.</div>

---

## The loop passed every local gate

<div class="timeline">
  <div class="time">Model call</div><div class="event">Within its individual request limit</div>
  <div class="time">Patch</div><div class="event">Applied inside the disposable workspace</div>
  <div class="time">Pytest</div><div class="event">Command completed and produced a result</div>
  <div class="time">Missing gate</div><div class="event danger-event">No check for repeated failure without progress</div>
</div>

<br>
<div class="quote">The runtime counted calls, but it did not compare their outcomes.</div>

---

## Three unchanged failures stopped the revised run

```python
if same_failure_signature and no_new_tests_pass:
    no_progress_streak += 1
else:
    no_progress_streak = 1
if no_progress_streak >= 3:
    stop("NO_PROGRESS_LIMIT_EXCEEDED")
```

<p class="small muted">The first failed round counted as one. A bigger diff did not count as progress.</p>

---

## The local reproduction stopped after three repeats

| Local check | Observed result |
|---|---|
| Customer B test | Expected 0.0, got 7.5 |
| Candidate patches | Three distinct patches check wrong fields |
| Repeated signature | One pass, one same failure each round |
| Stop reason | NO_PROGRESS_LIMIT_EXCEEDED |

---

## The low average hid the higher costs

<div class="equation">216 potential tasks × $5 each = $1080</div>

<p class="center">&nbsp;</p>

<div class="quote">A few large repositories or repair loops can break that average.</div>

---

## The budget account followed the task

<div class="timeline">
  <div class="time">Before call</div><div class="event">Reserve estimated tokens or tool time atomically</div>
  <div class="time">After call</div><div class="event">Settle actual consumption and release unused reserve</div>
  <div class="time">At a limit</div><div class="event warn-event">Record BUDGET_EXCEEDED and block new work</div>
</div>

<!-- <div class="rail">Local budget check: a four-unit cap granted 2 + 2, then denied 2. Concurrency remains untested.</div> -->

---

## Customer B ended as a handoff, not a PR

<div class="two-col">
  <div class="card warn-card"><h3>Controlled run state</h3><p>NO_PROGRESS_LIMIT_EXCEEDED</p><p class="small">No validated patch and no draft PR.</p></div>
  <div class="card good-card"><h3>Proposed owner handoff</h3><p>Last diff, target commit, failing tests, trace, ledger, and consumed budget.</p></div>
</div>

<br>
<div class="quote">The controlled run leaves a bounded problem with evidence.</div>

---

## A draft PR began the human change path

<div class="flow">
  <div class="node">Draft PR</div><div class="arrow">→</div>
  <div class="node accent-node">Ready for<br>review</div><div class="arrow">→</div>
  <div class="node">PR checks<br>and owner review</div><div class="arrow">→</div>
  <div class="node good-node">Human<br>merge</div><div class="arrow">→</div>
  <div class="node">Deploy</div>
</div>

<div class="rail">Runtime policy guarded work before review. GitHub rules guarded merge.</div>

---

## One 18-target campaign had six outcomes

| Campaign outcome | Targets |
|---|---:|
| Validated draft PR | 9 |
| Already fixed | 3 |
| Not affected | 2 |
| Human adaptation needed | 2 |
| Budget exceeded | 1 |
| Test environment unavailable | 1 |

<div class="rail">Nine draft PRs were review work, not nine deployed fixes.</div>

---

## The campaign record separated three milestones

<div class="three-col">
  <div class="card"><h3>Agent execution</h3><p>Patch checked, no-op, or explicit stop.</p></div>
  <div class="card"><h3>Code acceptance</h3><p>Owner review and merge of the current commit.</p></div>
  <div class="card"><h3>Customer rollout</h3><p>Release and production verification.</p></div>
</div>

<p class="small muted">Draft PRs still require merge, release, and production verification.</p>

---

## Customer C exposed a different limit

<div class="two-col">
  <div class="card good-card"><h3>Ordinary tests</h3><p>Two pass in the representative Customer C variant.</p></div>
  <div class="card warn-card"><h3>Customer invariant</h3><p>One additional test catches a lost VIP adjustment.</p></div>
</div>

<div class="rail">The customer-specific check blocks a draft PR for Customer C.</div>

---

## Publishing had its own uncertain result

<div class="two-col">
  <div class="card"><h3>Branch push</h3><p>Check the remote branch and expected commit after a lost response.</p></div>
  <div class="card warn-card"><h3>Draft PR create</h3><p>Check open and closed PRs for the known head branch after a lost response.</p></div>
</div>

<div class="rail">The worker held the action as UNKNOWN until reconciliation.</div>

---

## Two failures need different controls

<div class="two-col">
  <div class="card danger-card"><h3>Customer B repair loop</h3><p>The same refund test fails after changed patches.</p><p>Compare results across attempts; stop and hand off when the work makes no progress.</p></div>
  <div class="card warn-card"><h3>Lost GitHub response</h3><p>A branch push or PR create may have succeeded.</p><p>Keep its action key and check GitHub before another write.</p></div>
</div>

<div class="rail">Progress checks govern patch attempts. Reconciliation governs uncertain GitHub writes.</div>
<p class="small muted">The GitHub timeout is a separate recovery scenario.</p>

---

<!-- _class: brand brand-end -->
<!-- _footer: "Event organized by: Academic Partners Foundation" -->

<div class="brand-copy">
  <h1>Thank you for<br>watching!</h1>
  <p class="brand-desc">Remember to leave your questions<br>and rate the presentation<br>in the section below.</p>
</div>
<img class="brand-art" src="./assets/devai_last_slide_image.png" alt="DevAI by Data Science Summit and Academic Partners">

