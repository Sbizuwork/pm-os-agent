# Loop Spec: Cortex PM Chief-of-Staff Agent

> Module 2 - Loop Engineering

My first instinct was a goal loop, give Cortex the task and let it run until it is done. I backed off that. For version 1 I want it fired by something specific, with a hard definition of done, so I can see exactly what it did and where it stopped.

## 1. Trigger & loop type

**Chosen type:** Hook, as the main trigger, plus a cron sweep as backup.

The hook fires when a new PM task comes in, for example a request in the team channel or a new task assigned to me. That starts one run for that one task.

The backup is a Monday morning cron sweep (7am) that pulls together the weekly update draft, in case nothing triggered it during the week.

Why not the others:

- Heartbeat: I ruled this out. Cortex does not need to sit there polling all day. That burns spend and mostly finds nothing new.
- Pure cron on its own: too rigid. Half the real requests are ad hoc and would wait days for the next scheduled run.
- Pure goal loop: too open-ended for version 1. I want a trigger and an end I can point to, not an agent deciding for itself when it feels finished.

One dedupe rule: each run is tied to the task or message ID that fired it. If the same message fires the hook twice, Cortex attaches to the run that already exists instead of drafting the same update twice.

## 2. Goal / definition of done

Done means: a draft status update written back to the task thread, grounded in real activity I can check, plus any proposed stories sitting in a queue for me to approve. Cortex never sends or posts anything. Done is a draft waiting on a human, not a message sent.

How I know the draft is actually done, and not just long:

- Every claim in the draft points back to a real item, a ticket, a commit, a message. No claim with nothing behind it.
- No date or commitment appears in the draft unless that date exists in the source data.
- The at-risk section is there even if it is empty, so I know Cortex looked.

## 3. Stop conditions

| Condition | What it looks like | What happens |
|---|---|---|
| **Success** | Draft is written, claims check out against the sources, proposed stories are at or under the cap of 8 | Stop. Queue everything for my approval and log the run |
| **Stuck / give up** | Data will not pull after 3 tries, or two passes in a row produce no new information, or the sources contradict each other on a basic fact like a date | Stop, log what it tried, and tell me it is stuck instead of guessing |
| **Escalate to human** | The task touches anything above the line from Module 1: a public ship date, an embargoed or confidential project, a story batch over the cap, or wording that commits the team | Stop before drafting that part, flag it, and wait for me |

The escalate condition does the heavy lifting for safety. The success and stuck exits mostly save time and money. The escalate exit is the one that keeps Cortex from making a commitment in my name.

## 4. State

State is kept per project, and projects do not share state with each other.

What persists across runs for a project: the last approved update, the decision log, the roadmap notes and team norms for that project, and the list of task IDs already handled, so the dedupe rule works.

What is per run only: the activity pulled for this run, the draft in progress, and the attempt count. That gets cleared when the run ends, apart from what gets logged.

Scope note: no cross-project state. If Cortex is drafting for one project, it does not get to reach into another project's context to fill a gap. Gaps get flagged, not filled from somewhere else.

## 5. The five things a loop can lean on

| Component | For Cortex |
|---|---|
| **Work tree** | Not needed yet, because Cortex writes drafts and proposals, not code. There is nothing to isolate per run. I would revisit this if it ever starts editing shared files. |
| **Skills** | One real one so far: drafting a status update in the format of my past updates. That format is the skill. More skills wait until the basic loop is proven. |
| **Plugins / connectors** | None wired live yet. For now Cortex runs on the class fixture data. The plan is read-only connections to GitHub, Jira and Slack, in that order, and only after the line in Module 1 is respected by the tool permissions themselves. |
| **Subagents** | Placeholder, this is Module 3 (orchestration-map.md). The obvious first subagent is a checker that verifies draft claims against sources, because the main loop should not grade its own work. |
| **State tracking** | Always on. Per project state above, plus a simple run log: task ID, what fired it, steps taken, how it stopped (success, stuck, or escalated). If I cannot see how a run ended, I do not trust the next one. |

## Link to live loop

The starter build lives in `00-build/` in this repo (agent.py). The stop conditions in this spec are the ones I want that build to follow: stop at the approval queue, never post, and escalate on the Module 1 above-the-line items.
