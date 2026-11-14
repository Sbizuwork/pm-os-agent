# Orchestration Map: Cortex PM Chief-of-Staff Agent

> Module 3 · Orchestration & Subagents, ★ Deliverable 3
>
> ✅ **What this validates:** nothing advances unchecked, by the end you'll have proven a justified topology, a roster, and a validator with a defined fail action.
>
> Builds on your M2 Loop Spec. Only split one agent into a team when there's a real reason, coordination has a cost.

## 1. Why split? (or why not)

I looked at splitting Cortex into a team and mostly talked myself out of it. The work is one chain, pull the data, then draft from it, so there is nothing to run in parallel and no separate job that needs its own agent. The context is small too, one project at a time, nothing close to overflowing. The one real reason to split is checking. If Cortex grades its own draft, it grades it with the same blind spots it wrote it with. So the design is Cortex plus one critic subagent whose only job is to check the draft before it gets to me. That is the whole team.

## 2. Topology

**Pattern:** single + subagents

```
[PM task comes in] → [Cortex: pulls project data, drafts the update and the story batch]
→ [Critic: checks the draft] → fail → back to Cortex to revise (max 2) → still failing → escalate to me
→ pass → [My review checkpoint] → queued. Nothing sends or posts on its own.
```

One agent does the work, one subagent checks it. There is no fleet and no parallel work, because the steps depend on each other.

## 3. Roster

| Agent / subagent | Responsibility | Runs which Loop Spec |
|---|---|---|
| Cortex (chief of staff) | Pulls project data, drafts the leadership update, proposes the story batch | My M2 loop |
 | Critic (validator subagent) | Checks the draft against the four rules in Field 5 and returns a pass or a fail with reasons | Validation loop only |

## 4. Communication & hand-offs

Cortex hands the critic two things: the draft, and the source data it pulled, because the critic cannot check tracing without the sources. The critic hands back one of two things, a pass, or a fail with the specific check that failed and why. The hand-off is plain and in-process, no MCP or A2A protocol. Anything fancier would be decoration for a two-agent setup.

## 5. The validator

- **What the critic checks:** Four things. 1) Every number or date in the draft traces back to the data Cortex pulled, nothing invented. 2) The draft names the right project and the right issue and PR IDs. 3) No commitment language, no ship dates promised and no promises made to leadership. 4) The story batch stays at or under my cap of 8, and if it is over the critic flags it instead of quietly trimming it.
- **Fail action:** Revise. The critic sends the draft back to Cortex with the failed check named, and Cortex rewrites. That can happen at most 2 times. If it still fails after 2 revisions, it stops and escalates to me with the failure noted.
-  **Pass action:** A passing draft goes to my review checkpoint. It never sends or posts on its own.

## 6. State: shared vs isolated

Shared: the source data and the draft. Both agents work from the same facts. Isolated: the reasoning. The critic never sees how Cortex talked itself into the draft, and Cortex never sees the critic's reasoning, only the verdict and the named failure. That separation is the whole reason the critic exists. Project state stays per project, from my Module 2 spec, nothing leaks across projects.

## 7. Cost & latency budget

_Coordination has a price. Rough token/latency cost of the fleet vs a single agent. (Forward-link to M5 bounds.)_
