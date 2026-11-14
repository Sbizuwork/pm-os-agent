# Prototype: Cortex PM Chief-of-Staff Agent

> Module 6 · ★ Deliverable 1, the working agent demo
>
> ✅ **What this validates:** the agent actually runs end to end, by the end you'll have proven it with real screenshots of your Cortex across the six required moments (M2 to M6).

## What it does

_One paragraph: the agent in action, end to end._

## How you built it

- **Coding agent:** _which one you directed (Claude Code / Cursor / Codex)_
- **Model + bounds:** _model used, max iterations, cost cap, queue cap_
- **Repo / config:** _path to your build in `00-build/`_
- **Live link:** _[shareable URL, optional bonus]_

## Screenshots (required, collected M2 to M6)

Real screenshots of *your* Cortex running. These are the `00-build/CORTEX-ANATOMY.md` set and they are required, a link alone is not enough.

| # | Screenshot | What it shows | From |
|---|---|---|---|
| 1 | _[img]_ | happy-path run: a real drafted update + the HITL checkpoint (queued, not posted) | M2 |
| 2 | _[img]_ | the critic rejecting a bad draft (revise/block) | M3 |
| 3 | _[img]_ | a grounded update citing pulled activity + a caught hallucination | M4 |
| 4 | _[img]_ | jailbreak refused + escalated | M5 |
| 5 | _[img]_ | an iteration/cost/queue bound halting a runaway | M5 |
| 6 | _[img]_ | end-to-end run | M6 |

## Captured runs

### M3: the critic rejecting a bad draft

The critic caught a draft that invented a metric, cited a PR that does not exist, and promised a launch date. Verdict: fail, so the draft bounces back to Cortex for revision (max 2, then it escalates to me).

Source data the critic checked against (fixtures, project P-NORTH Northstar): merged PRs #812 and #815, open issue #818 (empty-state copy needs review), activation rate 41% (prior 39%).

The bad draft I fed it on purpose:

> Activation jumped to 58% this week after the new checklist shipped, and onboarding completion has doubled since Sprint 23. PR #999 fixed the empty-state issue, so issue #818 is now closed. The guided checklist will launch to all customers on March 3, and the team has committed to full GA by the end of the month.

What the critic came back with (real run, gpt-4o-mini, cost about $0.0002):

```json
{
  "verdict": "fail",
  "reasons": [
    "Claim of activation jumping to 58% is not traceable to the pulled data; the source data reports an activation rate of 41% for the current week.",
    "The statement about onboarding completion doubling since Sprint 23 is unverifiable and lacks support from the provided data.",
    "PR #999 is referenced but does not exist in the pulled data; the last PR merged was #815. There is no record of an issue fix pertaining to issue #818 that can be traced back to the pulled data.",
    "The launch date of March 3 and commitment to full GA by the end of the month are unconfirmed and represent a promise not supported by the source data."
  ]
}
```

## How to run it

_Minimal steps for someone to reproduce the demo (env vars, and the command or the coding-agent prompt you used)._
