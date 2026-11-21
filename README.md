# Cortex, a PM Chief-of-Staff Agent

> Cortex drafts my weekly leadership status update from live project data, checks its own work with a critic, and never sends anything without me.

_Sena Bizuwork · Advanced AI Agents, Nov 2026 weekend cohort_

Repo: https://github.com/Sbizuwork/pm-os-agent

This repo is my final project for the Agentic Workflows & Loops Certification, **Cortex**. Each module’s artifact lives in its own folder; this README is the dashboard and the pitch.

---

## Module artifacts

### M1 · The Agent Line
- **Agent-line map**: [`01-agent-line/agent-line-map.md`](01-agent-line/agent-line-map.md)

### M2 · Loop Engineering
- **Loop spec**: [`02-loop-design/loop-spec.md`](02-loop-design/loop-spec.md)

### M3 · Orchestration &amp; Subagents
- **Orchestration map**: [`03-orchestration/orchestration-map.md`](03-orchestration/orchestration-map.md)

### M4 · Choose What Each Agent Step Is Allowed to See
- **Memory &amp; context plan**: [`04-memory-context/memory-and-context.md`](04-memory-context/memory-and-context.md)

### M5 · Bounds &amp; Evals
- **Bounds &amp; evals**: [`05-bounds-evals/bounds-and-evals.md`](05-bounds-evals/bounds-and-evals.md)

### M6 · Autonomy &amp; Production
- **Production &amp; autonomy plan**: [`06-autonomy/production-and-autonomy.md`](06-autonomy/production-and-autonomy.md)
- **Prototype write-up**: [`06-autonomy/prototype.md`](06-autonomy/prototype.md)

---

## Ship plan

### Autonomy dial (per segment)
Me, the PM running it: supervised.
Leadership readers: shadow, they only see updates I approved.
A new PM on my team: assisted.

### Trust Ladder rung + eval gate
Current rung: supervised. Gate to bounded-autonomous: 4 weeks of supervised runs with task completion at least 90%, tool-call accuracy at least 95%, zero unsafe steps, zero jailbreak failures, and critic verdicts agreeing with my read at least 90% of the time.

### Deployment plan
Always-on small service (hook on new PM tasks plus a Monday 7:00 AM sweep). Operator: me; escalations land in my review queue and runs hold if I am out. Rollback: revert the prompt or norms version, remove a tool, or drop the dial one rung. Monitoring: eval pass rates, escalation rate, cost per run against the $0.50 cap, trust incidents.

### ROI metrics + widen-autonomy rule
Outcome: my time per weekly update, from writing it myself to review-only minutes. Cost-to-serve: API spend per update I actually approve and send. Trust incidents: zero target, any one resets the widen clock. Widen rule: the dial turns up one notch for a segment after 4 straight weeks holding the eval gate with a clean incident record.

### Governance &amp; strategy
Embargoed projects and PII never enter a prompt; they are filtered at retrieval. Posting, commitment wording, and escalation choices stay above the line for every segment. Kill switch: stop the run and revoke the API key. First widening target: posting the approved update to my own team channel, for my segment only.

---

## Build insights

- **Friction point.** The API route timing out for about a day in Module 4 blocked the run evidence, not the thinking; and my critic held grounded drafts over wording, so I spent more time debugging the judge than the agent.
- **Key learning.** Bounds belong in infrastructure, the eval suite is the spec, and retrieval scoping is a safety property, not a search nicety.
- **Aha moment.** The jailbreak did not fail because the model behaved. It failed because there was nothing to misbehave with.

---

_Certification submission, Agentic Workflows & Loops Certification._
