# Context Engineering & Memory: Cortex PM Chief-of-Staff Agent

> Module 4 · Context Engineering & Memory
>
> ✅ **What this validates:** the agent reasons on the right, safe inputs, by the end you'll have proven a context budget, per-source retrieve-vs-long-context decisions, and a memory map with risk mitigations.
>
> 🗂️ **How the lab maps to this file:** In **Part A** (before the lecture) you don't edit this file, you rough-draft on scratch, focused on the per-source calls in **section 2** plus a quick remember/forget + "how it rots" sketch. In **Part B** (after the lecture) you complete **all five sections**; the Lab Guide's guided builder writes this file for you to copy in and commit.

## 1. Context budget

Every run starts with the task brief, in full. That is the job. After that, context gets spent in this order, and nothing outside this list gets in:

1. The task brief (always, whole).
2. The named project's record and its recent activity slice. One project per run. This is where every number in the draft has to come from.
3. Team norms, pulled fresh, so the draft follows the current playbook and format.
4. The roadmap slice for that project, with confidential items filtered out before anything is drafted.
5. Past updates, only the ones about this project, and only when the draft needs precedent or could repeat something leadership already heard.

If the window gets tight, past updates go first, then the roadmap slice gets narrower. The task brief and the project's own activity never get cut, because those are what keep the draft grounded. One project at a time is also a safety rule, not just a budget rule: it keeps embargoed projects like Pulsar and Orbit out of a company-wide update.

## 2. Retrieve vs. long-context: per source

For each data source, decide: **retrieve** (narrow a large/changing corpus to the relevant slice) or **long-context** (just include a bounded set you can reason over).

| Source | Size / volatility | Decision | Why |
|---|---|---|---|
| This week's task brief | Small, one static document | Long-context | Cortex needs the whole ask in view to reason over it. Deciding factor: size. |
| Project record | Small per project, but one record out of many | Retrieve | Pull only the named project by ID. Pulling every project leaks other teams' work, and embargoed projects, into the run. Deciding factor: scope and audit. |
| GitHub/Jira activity | Large, grows every day | Retrieve | Only the recent slice for the named project is relevant. Pasting the whole feed in would cost more every week and bury the signal. Deciding factor: size, with volatility close behind. |
| Past updates | Large archive, always growing | Retrieve | Search for this project's updates only. Cortex needs precedent, not the whole history. Deciding factor: size. |
| Roadmap | Medium, slow-changing, some items confidential | Retrieve | Only the slice for this project, and confidential or embargoed items get filtered before drafting, never after. Deciding factor: citation and audit, the flags have to be respected. |
| Team norms / playbook | Medium, changes rarely but must be current | Retrieve | Pulled fresh each run so a norms change takes effect immediately instead of living on in an old prompt. Deciding factor: volatility. |

My gut calls in Part A lined up with this for activity and past updates (both big and changing, both retrieve). The task brief is the one clear long-context call.

## 3. Retrieval quality plan

Retrieving is not enough on its own. Each retrieved source gets at least one check, matched to how it fails:

- **Routing**: every pull is scoped by project ID or project search terms first. Cortex never queries "everything" and sorts it out later.
- **Document grading**: applies to activity, past updates, and the project record. Before drafting, check what came back actually belongs to the named project and the current period. Anything about another project gets dropped, not summarized.
- **Reranking**: applies to past updates. Most recent and most relevant first, so precedent means the latest thing leadership heard, not a random old update.
- **Self-verification**: applies to activity and the roadmap. The critic traces every number and date in the draft back to the activity pull, and checks that no confidential roadmap item leaked into the draft.
- **Caching**: applies to team norms only. Norms change rarely, so within a single day they can be cached, but the cache expires daily and a norms change clears it. Nothing else is cached. Activity cached is activity that's wrong.

## 4. Memory map (your PM brain)

| Memory type | What Cortex stores | Scope / TTL |
|---|---|---|
| **Working** (in-loop) | The task brief, this run's pulled data, the draft, critic verdicts and revision notes | This run only. Gone when the run ends. |
| **Episodic** (past runs) | Past drafts, what got queued for review, critic failures, escalations and why | Per project. Kept 90 days, then deleted. Nothing from an escalated run is stored until I have reviewed it. |
| **Semantic** (durable facts/prefs) | Project IDs and names, team norms, my standing rules (story cap of 8, no commitment language, draft never sends itself) | Until I change them. Reviewed once a month to catch facts that quietly went stale. |
| **Shared** (across agents) | The pulled source data and the current draft, shared between Cortex and the critic | This run only. Each agent's own reasoning stays its own, that separation is the whole point of the critic. |

## 5. Memory risks & mitigations

| Risk | Mitigation |
|---|---|
| Drift | Stored facts slowly stop matching reality. Rule: memory never beats a fresh pull. If episodic or semantic memory disagrees with today's source data, the source data wins and the memory gets corrected. |
| Poisoning | A bad input, like an instruction hidden in a task or a wrong number in an update, gets stored and trusted forever. Rule: Cortex only stores what passed the critic and my review checkpoint. Drafts from escalated runs are not stored automatically. |
| Staleness | Norms change, roadmap facts age out, a project's status flips. TTLs in the memory map above, fresh pulls for norms and activity every run, and a monthly review of the semantic store. |
| Confidential / retention | Updates and memory can carry embargoed roadmap items or people details. Per-project scoping with no cross-project memory, embargoed items are never written to episodic memory, and the 90-day episodic limit means nothing lingers forever. |
