---
marp: true
theme: default
size: 16:9
paginate: true
style: |
  @font-face {
    font-family: 'Instrument Sans';
    src: url('assets/fonts/InstrumentSans-Regular.woff2') format('woff2');
    font-weight: 400; font-style: normal; font-display: swap;
  }
  @font-face {
    font-family: 'Instrument Sans';
    src: url('assets/fonts/InstrumentSans-Medium.woff2') format('woff2');
    font-weight: 500; font-style: normal; font-display: swap;
  }
  @font-face {
    font-family: 'Instrument Sans';
    src: url('assets/fonts/InstrumentSans-SemiBold.woff2') format('woff2');
    font-weight: 600; font-style: normal; font-display: swap;
  }
  @font-face {
    font-family: 'Instrument Sans';
    src: url('assets/fonts/InstrumentSans-Bold.woff2') format('woff2');
    font-weight: 700; font-style: normal; font-display: swap;
  }

  :root {
    --midnight: #192833; --dark-teal: #126275; --medium-teal: #0AADC8;
    --light-teal: #83F0FF; --white: #FFFFFF; --off-white: #F2F9F9;
    --green: #4BCFA0; --amber: #FFB566; --red: #E27070;
    --body-secondary: #4a6870; --chrome-muted: #5a7a80;
    --radius-3: 8px;
  }

  /* ---------- Light slide (default) ---------- */
  section {
    width: 1280px; height: 720px;
    padding: 112px 60px 48px;
    display: flex; flex-direction: column; justify-content: flex-start;
    font-family: 'Instrument Sans', Arial, sans-serif;
    font-size: 24px; line-height: 1.45;
    color: var(--midnight);
    background: var(--white) url('assets/coherent-logo-navy.svg') no-repeat left 60px top 48px / 100px 28px;
    /* The 6px top bar sits outside the padding edge, so measure the logo from the slide edge. */
    background-origin: border-box;
    border-top: 6px solid var(--midnight);
  }
  section h1 {
    font-size: 40px; font-weight: 700; line-height: 1.15; letter-spacing: -0.5px;
    color: var(--dark-teal); margin: 0 0 28px; padding: 0; border: 0;
  }
  section h1::after {
    content: ''; display: block; width: 60px; height: 3px;
    background: var(--medium-teal); border-radius: 2px; margin-top: 12px;
  }
  section h2 {
    font-size: 24px; font-weight: 700; color: var(--dark-teal);
    margin: 18px 0 8px; padding: 0; border: 0;
  }
  section p, section li { color: var(--midnight); }
  section ul, section ol { padding-left: 1.1em; margin: 0; }
  section li { margin: 6px 0; }
  section li::marker { color: var(--medium-teal); font-weight: 700; }
  section strong { color: var(--dark-teal); }
  section a { color: var(--dark-teal); text-decoration: none; }

  /* ---------- Chrome: copyright, tagline, page number ---------- */
  section header {
    position: absolute; top: 24px; left: auto; right: 60px;
    font-size: 12px; line-height: 1.5; text-align: right;
    color: var(--chrome-muted);
  }
  section footer {
    position: absolute; bottom: 32px; left: 60px; right: auto;
    font-size: 11px; letter-spacing: 0.5px; color: var(--midnight);
  }
  section footer em { font-style: normal; color: var(--medium-teal); padding: 0 2px; }
  section::after {
    right: 60px; bottom: 32px; padding: 0;
    font-size: 11px; color: var(--chrome-muted);
  }

  /* ---------- Code ---------- */
  section code {
    font-family: 'JetBrains Mono', Menlo, Consolas, monospace;
    background: rgba(18,98,117,0.08); color: var(--dark-teal);
    border-radius: 4px; padding: 1px 6px; font-size: 0.9em;
  }
  section pre {
    background: var(--midnight); border: 0; border-left: 4px solid var(--medium-teal);
    border-radius: var(--radius-3); padding: 20px 24px; margin: 4px 0 20px;
    font-size: 20px; line-height: 1.5;
  }
  section pre code { background: transparent; color: var(--off-white); padding: 0; font-size: 1em; }
  section pre .hljs-keyword, section pre .hljs-built_in, section pre .hljs-type { color: var(--light-teal); }
  section pre .hljs-string { color: var(--green); }
  section pre .hljs-number, section pre .hljs-literal { color: var(--amber); }
  section pre .hljs-title, section pre .hljs-function, section pre .hljs-params { color: var(--off-white); }
  section pre .hljs-comment { color: rgba(242,249,249,0.55); font-style: normal; }

  /* ---------- Tables ---------- */
  section table { border-collapse: collapse; width: 100%; font-size: 20px; margin: 0 0 20px; display: table; }
  section table tr, section table tr:nth-child(2n) { background: transparent; border: 0; }
  section table th {
    text-align: left; padding: 10px 16px; border: 0;
    font-size: 14px; font-weight: 600; letter-spacing: 0.5px; text-transform: uppercase;
    background: rgba(18,98,117,0.08); color: var(--dark-teal);
  }
  section table td { padding: 10px 16px; border: 0; border-top: 1px solid rgba(18,98,117,0.12); color: var(--midnight); }
  section table td:first-child { font-weight: 600; color: var(--dark-teal); }

  /* ---------- Two-column comparison: h1, h2 + block, h2 + block, optional note ---------- */
  section.cols {
    display: grid; grid-template-columns: 1fr 1fr; column-gap: 24px;
    grid-template-rows: auto auto auto 1fr; align-content: start;
  }
  section.cols h1 { grid-column: 1 / -1; grid-row: 1; }
  section.cols h2 { margin: 0 0 10px; }
  section.cols h2:nth-of-type(1) { grid-column: 1; grid-row: 2; }
  section.cols h2:nth-of-type(2) { grid-column: 2; grid-row: 2; }
  section.cols h2:nth-of-type(1) + * { grid-column: 1; grid-row: 3; }
  section.cols h2:nth-of-type(2) + * { grid-column: 2; grid-row: 3; }
  section.cols h2 + * {
    margin: 0; background: var(--white);
    border: 1px solid rgba(25,40,51,0.08); border-left: 4px solid var(--dark-teal);
    border-radius: var(--radius-3); padding: 16px 20px 16px 20px; font-size: 22px;
  }
  section.cols h2:nth-of-type(2) + * { border-left-color: var(--medium-teal); }
  section.cols h2 + ul { padding-left: 44px; }
  section.cols h2:nth-of-type(2) + * ~ :not(header):not(footer) {
    grid-column: 1 / -1; grid-row: 4; align-self: start;
    margin-top: 24px; color: var(--body-secondary);
  }

  /* ---------- Dark slide ---------- */
  section.dark {
    padding-top: 128px;
    color: var(--white);
    background: var(--midnight) url('assets/coherent-logo-teal.svg') no-repeat left 60px top 48px / 100px 28px;
    border-top: 0;
  }
  section.dark::before {
    content: ''; position: absolute; right: -5%; bottom: 80px;
    width: 70%; height: 1px; background: rgba(255,255,255,0.08);
    transform: rotate(-15deg); transform-origin: right bottom;
    box-shadow: -40px 40px 0 rgba(255,255,255,0.08);
  }
  section.dark h1 { color: var(--white); }
  section.dark h2 { color: var(--light-teal); }
  section.dark p, section.dark li { color: rgba(255,255,255,0.85); }
  section.dark strong { color: var(--light-teal); }
  section.dark a { color: var(--medium-teal); }
  section.dark code { background: rgba(131,240,255,0.12); color: var(--light-teal); }
  section.dark header { top: 48px; color: rgba(255,255,255,0.7); }
  section.dark footer { color: var(--white); }
  section.dark::after { right: 60px; color: rgba(255,255,255,0.5); }
  section.dark.cols h2 + * {
    background: rgba(255,255,255,0.05); border: 1px solid rgba(131,240,255,0.12);
    border-left: 4px solid var(--medium-teal); color: rgba(255,255,255,0.85);
  }
  section.dark.cols h2:nth-of-type(1) + * { border-left-color: var(--red); }
  section.dark.cols h2:nth-of-type(2) + * { border-left-color: var(--green); }

  /* ---------- Cover and closing ---------- */
  section.cover, section.closing {
    justify-content: center; padding-top: 64px;
    background-size: 159px 44px;
    border-right: 5px solid var(--medium-teal);
  }
  section.cover h1, section.closing h1 { font-size: 52px; max-width: 900px; margin-bottom: 12px; }
  section.cover h1::before {
    opacity: 0;
    content: 'Coherent Solutions'; display: block; margin-bottom: 20px;
    font-size: 15px; font-weight: 500; letter-spacing: 2px; text-transform: uppercase;
    color: var(--medium-teal);
  }
  section.cover h1::after, section.closing h1::after { width: 80px; margin-top: 20px; }
  section.cover p:first-of-type { font-size: 30px; color: var(--light-teal); margin: 8px 0 0; }
  section.cover p:last-of-type { font-size: 20px; color: rgba(255,255,255,0.6); margin-top: 28px; }
  section.closing p { font-size: 20px; color: rgba(255,255,255,0.7); margin: 4px 0; }
  section.closing p:first-of-type { font-size: 24px; color: var(--white); font-weight: 500; margin-top: 16px; }
  section.closing p:last-of-type { font-size: 22px; color: var(--light-teal); margin-top: 28px; }
  section.closing a:has(img) { display: inline-flex; align-items: center; gap: 12px; }
  section.closing a img { width: 22px; height: 22px; margin: 0; flex: none; background: transparent; }

  /* ---------- Screenshot slides: one interface, large enough to read ---------- */
  section.shot { padding-top: 100px; padding-bottom: 36px; }
  section.shot h1 { margin-bottom: 12px; }
  section.shot p { margin: 0; }
  section.shot img {
    display: block; width: auto; max-width: 1160px; max-height: 470px; height: auto;
    margin: 2px auto 0; border-radius: 8px; background: var(--white);
  }
  section.shot p:last-of-type {
    margin-top: 12px; font-size: 20px; line-height: 1.3; color: var(--body-secondary);
  }
  section.dark.shot::before { display: none; }
  section.dark.shot img { border: 1px solid rgba(255,255,255,0.16); }
  section.shot:not(.dark) img { border: 1px solid rgba(25,40,51,0.10); }
  section.dark.shot p:last-of-type { color: rgba(255,255,255,0.62); }

  /* ---------- Full-bleed image: stretched over title, logo, and page number ---------- */
  section.fullbleed {
    position: relative;
    padding: 0;
    border: 0;
    overflow: hidden;
  }
  section.fullbleed p {
    position: absolute;
    inset: 0;
    margin: 0;
    top: 100px;
    width: 100%;
    height: 100%;
    z-index: 2;
  }
  section.fullbleed img { 
    display: block;
    width: 100%;
    max-width: none;
    max-height: none;
    margin: 0;
    border: 0;
    border-radius: 0;
    object-fit: fill;
    background: transparent;
  }

  /* ---------- Diagram slides: one full-width SVG under the title ---------- */
  section.diagram { padding-top: 100px; padding-bottom: 36px; }
  section.diagram h1 { margin-bottom: 8px; }
  section.diagram p { margin: 0; }
  section.diagram img {
    display: block; width: 1160px; max-width: 100%; height: auto;
    margin: 4px auto 0; background: transparent; border: 0;
  }
  section.diagram p + p {
    margin-top: 10px; font-size: 20px; line-height: 1.3; color: var(--body-secondary);
  }
  section.dark.diagram { padding-top: 100px; }
  section.dark.diagram::before { display: none; }
  section.dark.diagram p + p { color: rgba(255,255,255,0.62); }
---

<!-- _class: dark cover -->
<!-- _paginate: false -->

# Human-in-the-Loop is not enough

How to stop AI agent loops in Python

Mikalai Saskavets · PyCon Wroclaw 2026

<!--
-->

---

<!-- _class: diagram -->

# A standard on-call pipeline

![Production feeds monitoring and alert rules; incident routing pages the on-call engineer and escalates if the page is not acknowledged](assets/draws/02-standard-oncall-pipeline--light.svg)

The engineer investigates each page.

<!--
-->

---

<!-- _class: diagram -->

# New services created alert fatigue

![Recurring latency alerts every 5–10 minutes, then the same on-call triage](assets/draws/03-alert-fatigue--light.svg)

Uncertain thresholds. Repeated triage was the cost.

<!--
-->

---

<!-- _class: diagram -->

# We added AI-assisted incident triage

![AI triage collects evidence, prepares a summary, and proposes the next action; consequential actions need policy checks and human approval](assets/draws/04-ai-assisted-triage--light.svg)

The engineer receives evidence and a proposal.

<!--
-->

---

<!-- _class: dark shot -->

# The first approval

![Approval request 1: update_alert_rule raises the latency-p95 threshold from 500 ms to 1000 ms and waits for Approve, Reject, or Escalate](assets/screenshots/01-first-approval-cropped.png)


<!--
-->

---

<!-- _class: diagram -->

# The alert storm moved

![AI triage reduces raw-alert review and introduces repeated approval requests](assets/draws/05-approval-fatigue-shift--light.svg)

We reduced alert fatigue and found approval fatigue.

<!--
-->

---

<!-- _class: dark shot -->

# One incident, one repeated decision

![The human rejects the threshold change and asks for an investigation, but the agent proposes the same 500 → 1000 ms change again](assets/screenshots/02-naive-repeat.png)

Different wording, same action. 

<!--
-->


---

<!-- _class: dark shot -->

# One incident, one repeated decision

![Approval request 1 is rejected; approval request 2 asks for the same latency-p95 change from 500 ms to 1000 ms](assets/screenshots/02-naive-repeat-cropped.png)

Different wording, same action. 

<!--
-->

---

<!-- _class: diagram -->

# HITL is a boundary, not a UI

![Slack, Discord, and Chainlit share one human-interaction boundary and one execution policy](assets/draws/08-channel-independent-hitl--light.svg)

Chainlit is the interface in this talk. Slack and Discord would use the same boundary.

<!--
-->

---

<!-- _class: cols -->

# Only consequential actions need approval

## Read-only investigation
Metrics, logs, Kubernetes status, summaries — automatic but bounded.

## Consequential actions
Rule changes, suppression, resolution, escalation — policy checks and approval when required.

<!--
-->

---

# Feedback without a transition

~~~python
input_from_human = "Do not change this threshold"
messages.append(input_from_human)
proposal = planner(messages)
route(proposal)  # same proposal can reach the approval gate again
~~~

The conversation changed. The allowed transition did not.

<!--
-->

---

# A human decision becomes execution state

| Decision / Event | Execution meaning |
| --- | --- |
| Approve | Authorize this exact pending change |
| Reject | Deny this proposal in this investigation |
| Revise | Change objective or constraints |
| Escalate | Hand off to the human on-call engineer |
| Timeout | Apply backend escalation policy |

No response is never approval.

<!--
-->

---

<!-- _class: diagram -->

# The controlled workflow

![Preflight, proposal, guard, approval gate, and execution, with rejection persisted and blocked paths stopped](assets/draws/12-controlled-workflow--light.svg)

Every approval-controlled effect crosses the guard, the gate, and final revalidation.
<!--
-->

---

# State that changes the next transition

~~~python
class RunState(TypedDict):
    proposal_steps: int
    no_progress_count: int
    denied_fingerprints: list[str]
    pending: dict  # contains proposal_fingerprint, operation_id
    approval_token: str
    deadline_at: float
    ownership: Literal["ai", "human"]
    status: str
    stop_reason: str
~~~

These are selected fields

<!--
-->

---

<!-- _class: diagram -->

# Two identities solve two different problems

![proposal_fingerprint deduplicates equivalent proposals; operation_id stays stable across retry, resume, and replay](assets/draws/14-proposal-vs-operation-identity--light.svg)



<!--
-->

---

<!-- _class: diagram -->

# Approval belongs to one exact rule change

![An approval for rule version 7 is rejected after the live rule moves to version 8](assets/draws/15-stale-approval--light.svg)

A stale approval cannot authorize a newer rule version.

<!--
-->

---

# The guard runs before the side effect

~~~python
if state["ownership"] == "human":
    return stop("incident_escalated")
if action.fingerprint in state["denied_fingerprints"]:
    return stop("previously_rejected")
if deadline_expired(state) or budget_exhausted(state):
    return escalate("policy_limit")
if ledger.succeeded(action.operation_id):
    return existing_receipt()
return require_approval(action)
~~~

The model proposes. Application code decides what may execute.

<!--
-->

---

<!-- _class: diagram -->

# Pause and resume with LangGraph

![Persist the pending gate, resume the same thread, re-enter the node, validate, then execute](assets/draws/17-langgraph-interrupt-resume--light.svg)

<!--
-->

---

<!-- _class: diagram -->

# Checkpoint is not the effect ledger

![An effect can commit before the checkpoint records success; a retry reuses the same operation_id](assets/draws/18-checkpoint-vs-effect-ledger--light.svg)

<!--
-->

---

<!-- _class: diagram -->

# Limits must end in a defined outcome

![No progress, exhausted budget, deadline, or approval timeout transfers the incident to a person](assets/draws/19-termination-and-escalation--light.svg)

A missing reply is never approval.

<!--
-->

---

<!-- _class: fullbleed -->

![Naive versus controlled after the same rejection: the naive agent asks for the same threshold change again; the controlled guard blocks it and hands the incident to the human on-call](assets/screenshots/04-compare-naive-and-controlled.png)


<!--
-->

---

<!-- _class: dark shot -->

# Same rejection, different execution


![After approval request 1 is rejected, the guard blocks the repeated proposal as previously_rejected, and the human on-call owns INC-1042](assets/screenshots/03-controlled-stop-cropped.png)

<!--
-->


---

# A human decision must change execution

- Persist the decision where the next guard reads it
- Bind approval to the exact action and revision
- Keep operation identity stable across retry and resume
- Escalate or terminate explicitly

Otherwise, we risk replacing alert fatigue with approval fatigue.


<!--
-->

---

<!-- _class: dark closing -->
<!-- _paginate: false -->

# Thanks

<br><br><br>

Mikalai Saskavets

<a href="https://github.com/miksask"><img src="assets/logo-github.svg" alt="" width="22" height="22">github.com/miksask</a>

<a href="https://linkedin.com/in/mikalaisaskavets/"><img src="assets/logo-linkedin.svg" alt="" width="22" height="22">linkedin.com/in/mikalaisaskavets/</a>

&nbsp;

<!--
-->



