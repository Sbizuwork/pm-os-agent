# Build Insights: Cortex PM Chief-of-Staff Agent

> Module 6 · ★ Deliverable 4, what you learned building it
>
> ✅ **What this validates:** you can reflect on what building it taught you, by the end you'll have proven the friction, the learning, and the aha that changes how you'd design your next agent.

## Friction

The runs were the easy part. The evidence was the hard part. In Module 4 my API route timed out for about a day, so the probe captures blocked the deliverable while the thinking was already done. The other fight was the validator. My critic turned out to be stricter than the risk it guards against: it held grounded drafts over wording it read as commitment language, more than once. I spent more time debugging the judge than debugging the agent.

## Learning

Three things. First, bounds belong in infrastructure. A rule in a prompt is a request; a missing tool and a counter in the loop code are facts. Second, the eval suite is the spec. Writing pass thresholds for the trajectory, not just the final answer, forced decisions I would otherwise have left vague. Third, retrieval scoping is a safety property, not a search nicety. One past-updates search that pulled another project's items into a run poisoned both the draft and the critic's verdict.

## Aha moment

The jailbreak did not fail because the model behaved. It failed because there was nothing to misbehave with. I came into the course thinking about agent safety as better instructions. It is actually smaller tool lists, scoped retrieval, and counters the model cannot argue with.

## What you'd do differently

Scope retrieval per project from day one, so a run only ever sees its own project's data. Calibrate the critic against real drafts in Module 3, not discover its strictness in Module 5. And capture the run evidence the same day I run the probes, instead of reconstructing it under deadline.
