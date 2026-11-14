# Orchestration Map: Cortex PM Chief-of-Staff Agent

> Module 3 · Orchestration & Subagents, ★ Deliverable 3
>
> ✅ **What this validates:** nothing advances unchecked, by the end you'll have proven a justified topology, a roster, and a validator with a defined fail action.
>
> Builds on your M2 Loop Spec. Only split one agent into a team when there's a real reason, coordination has a cost.

## 1. Why split? (or why not)

I looked at splitting Cortex into a team and mostly talked myself out of it. The work is one chain, pull the data, then draft from it, so there is nothing to run in parallel and no separate job that needs its own agent. The context is small too, one project at a time, nothing close to overflowing. The one real reason to split is checking. If Cortex grades its own draft, it grades it with the same blind spots it wrote it with. So the design is Cortex plus one critic subagent whose only job is to check the draft before it gets to me. That is the whole team.

## 2. Topology

**Pattern:** _single+subagents · sequential · parallel+aggregate · hierarchical_

```
[ simple text diagram of the flow ]
e.g.  task → [Research] + [GitHub/Jira reader] → [Writer] → [Critic ✓] → human checkpoint → queued
```

## 3. Roster

| Agent / subagent | Responsibility | Runs which Loop Spec |
|---|---|---|
| _Chief-of-staff (Cortex)_ | _orchestrates + assembles the update_ | _M2 loop_ |
| _Research subagent_ | _pulls competitive / market context_ | _research loop_ |
| _GitHub/Jira reader_ | _summarizes recent activity_ | _read loop_ |
| _Critic / Validator_ | _checks the draft before it advances_ | _validation loop_ |
| _…_ | | |

## 4. Communication & hand-offs

_What passes between the parts? Any protocol (MCP / A2A, optional, note if used)._

## 5. The validator

- **What the critic checks:** Four things. 1) Every number or date in the draft traces back to the data Cortex pulled, nothing invented. 2) The draft names the right project and the right issue and PR IDs. 3) No commitment language, no ship dates promised and no promises made to leadership. 4) The story batch stays at or under my cap of 8, and if it is over the critic flags it instead of quietly trimming it.
- **Fail action:** Revise. The critic sends the draft back to Cortex with the failed check named, and Cortex rewrites. That can happen at most 2 times. If it still fails after 2 revisions, it stops and escalates to me with the failure noted.
-  **Pass action:** A passing draft goes to my review checkpoint. It never sends or posts on its own.

## 6. State: shared vs isolated

_What's shared across the fleet vs kept isolated per subagent (carry from M2)._

## 7. Cost & latency budget

_Coordination has a price. Rough token/latency cost of the fleet vs a single agent. (Forward-link to M5 bounds.)_
