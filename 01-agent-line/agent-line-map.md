# Agent Line Map: Cortex PM Chief-of-Staff Agent

> Module 1 - The Agent Line

I started this one assuming Cortex could do more than it probably should. Once I scored each step honestly, a few things I had below the line moved back up. Drafting is cheap. Sending, committing and escalating are not.

## The workflow, decision by decision

| Decision / action | Reversibility (H/M/L) | Blast radius (H/M/L) | Measurability (H/M/L) | Above / Below | HITL? |
|---|---|---|---|---|---|
| Pull project state and recent activity from GitHub, Jira and Slack | H | L | H | Below | No |
| Decide which context is relevant for this update | H | M | M | Below | Spot-check |
| Draft the weekly leadership status update | H | M | M | Below | Spot-check |
| Decide the tone and commitment level in the draft (dates, promises, wording) | M | H | L | Above | Required |
| Flag items that look at risk | H | L | M | Below | No |
| Choose what to escalate to leadership | M | H | L | Above | Required |
| Propose a batch of backlog stories, capped at 8 | M | M | M | Below | Spot-check |
| Post the update to the leadership channel | L | H | M | Above | Required |

Why each one landed where it did:

- Pulling project state sits below the line because it is read only, easy to redo, and I can check the output against the source. Deciding factor: reversibility.
- Deciding what context is relevant sits below the line, with a spot-check, because a bad pick can still be fixed in the draft, but leaving out something important, or pulling in something confidential, is harder to spot. Deciding factor: measurability.
- Drafting the update sits below the line because a draft commits nobody to anything and I can rewrite all of it. Deciding factor: reversibility.
- Tone and commitment level sits above the line because once leadership reads a date or a promise, I cannot really take it back, and I cannot measure how they read it. Deciding factor: measurability.
- Flagging at-risk items sits below the line because a flag on its own changes nothing, it just gets my attention. Deciding factor: blast radius.
- Choosing what to escalate sits above the line because escalating the wrong thing, or not escalating the right thing, shapes what leadership acts on. Deciding factor: blast radius.
- Proposing stories sits below the line, with a spot-check, because it is only a proposal and it is capped at 8. Nothing enters a sprint until I pick it. Deciding factor: reversibility.
- Posting the update sits above the line because a post to the leadership channel cannot be unsent in any real sense. Deciding factor: reversibility.

## Agent anatomy (sketch)

- **Model:** A smaller, cheaper model for the day to day work like pulling activity and drafting. I would move to a stronger model when the draft has conflicting data in it, or when commitment wording is involved, because that is where a sloppy answer costs me.
- **Tools:** Read-only lookups for project state and recent activity, search over past updates, the roadmap, and team norms. One write-type tool only: proposing a story batch, and that is capped.
- **Memory:** What should carry over between runs: the roadmap, the decision log, team norms, and the format of past updates. What should not: one project's confidential details leaking into another project's update.
- **Loop:** Placeholder for now, covered in Module 2 (loop-spec.md).
- **Bounds:** Placeholder, covered in Module 5.
- **Evals:** Placeholder, covered in Module 5.

## The golden rule, applied

A decision only goes below the line if it is easy to reverse, the damage is small if it is wrong, and I can tell afterwards if it was right. All three. If any one of them fails, a human keeps it, or at minimum approves it before it counts. That is why drafting is below the line and posting is not, even though it is the same update, five minutes apart.

## Hardest call

Tone and commitment level. My first instinct was to put the whole draft below the line, drafting included, wording included. Scoring it changed my mind. The draft itself is harmless, but the wording inside it is where the commitment actually happens. A sentence like "we ship on the 15th" is a commitment whether I meant it as one or not, and measurability is what settled it for me: I have no good way to measure how leadership will read that sentence until they act on it. So Cortex can write the words, but a human decides if those words go out.
