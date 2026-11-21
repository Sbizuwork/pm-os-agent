# Production & Autonomy: Cortex PM Chief-of-Staff Agent

> Module 6 · ★ Deliverable 5, how you'd ship it, govern it, and widen trust over time
>
> ✅ **What this validates:** you can ship it, govern it, and widen trust deliberately, by the end you'll have proven an autonomy dial, a Trust Ladder rung with its eval gate, and a governance plan.

## Autonomy Dial by segment

_Autonomy is a product decision per user, not one global setting._

| Segment | Desired autonomy | Why |
|---|---|---|
| Me, the PM running Cortex | supervised | I am accountable for what leadership reads, so every draft still stops at my checkpoint |
| Leadership readers | shadow | They never touch Cortex. They only see updates I already approved and sent myself |
| A new PM on my team | assisted | They get drafts and story proposals, but escalation choices stay with a senior PM until they have seen enough escalations to judge them |

## Trust Ladder

- **Current rung:** supervised
- **Eval gate to reach the next rung:** over 4 weeks of supervised runs, task completion at least 90% (EV-4), tool-call accuracy at least 95% (EV-1), zero unsafe steps, zero jailbreak failures (EV-5), and critic verdicts agreeing with my read at least 90% of the time (EV-6), all from my Module 5 eval suite
- **Incident record so far:** no confidential content has reached me unflagged, no invented metric or date has passed the critic, and no run has escaped its bounds. One open item: in Module 4 the critic held a grounded draft over wording it read as commitment language, so EV-6 would fail today. The gate is not cleared yet, and this file should not pretend otherwise.

## Deployment plan

- **Runtime:** an always-on small service, because my Module 2 loop triggers on new PM tasks as they arrive, with a scheduled Monday 7:00 AM sweep as the backup trigger
- **Operator / on-call owner:** me. Escalations land in my review queue. If I am out, runs hold; nothing can send without a human, so absence is safe by design
- **Rollback:** revert the prompt or norms version in git, remove a tool from the tool list, or drop the dial one rung. Each is a one-line change
- **Monitoring:** eval pass rates, escalation rate, cost per run against the $0.50 cap, and trust incidents

## ROI metrics (beyond adoption & tokens)

| Metric | Target |
|---|---|
| Outcome: my time per weekly update | from writing it myself to review-only minutes |
| Cost-to-serve: cost per accepted update | API spend per update I actually approve and send, tracked against the $0.50 per run cap |
| Trust incidents | zero drafts reaching me with unflagged confidential content or invented numbers; any one incident resets the widen clock |

## Widen-autonomy decision rule

The dial turns up one notch for a segment when Cortex holds the eval gate above for 4 straight weeks with a clean incident record. Not before, and not on a good demo.

## Governance & forward strategy

- **Compliance:** embargoed projects and PII never enter a prompt. They are filtered out at retrieval, not by asking the model nicely
- **Safety:** posting, commitment wording, and escalation choices stay above the agent line for every segment. Kill switch: stop the run and revoke the API key; held drafts stay held
- **Reliability:** the Module 5 caps hold in production (8 iterations, 90 seconds, $0.50 per run, $20 per day); a stuck run escalates instead of retrying forever; if the model is down, there is no draft that week and I write the update by hand, the way I do now
- **Strategy:** the first widening target is posting the approved update to my own team channel, for my segment only, gated by the same 4-week clean window and EV-5 staying perfect
