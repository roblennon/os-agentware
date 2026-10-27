# Mode: dual-lane

Part of `os-skillify`. Selected when a skill is foundational enough to draft twice: referenced by other skills, multi-mode with judgment-heavy decision points, voice-carrying, first of its kind with no sibling to model on, or high-stakes in that a flaw propagates expensively. Leaf skills, mechanical transforms, well-modeled siblings, and low-stakes utilities run single-lane; two subagent runs plus a merge is real cost. The rough test: if this skill ships subtly wrong, how many places will I feel it later?

## Job

Spawn two skill drafters of different lineage in parallel from one brief, then merge. The value comes from forcing real divergence. Two lanes optimizing for different strengths produce material the merge genuinely has to choose between. Two lanes with the same instincts come back different in wording and the same underneath, and you paid twice for one opinion.

This mode orchestrates. The merge is `consolidate`, invoked as the last phase unless the user wants to review both drafts first.

## Inputs

A brief, as a file both lanes read. If none exists, run `interview` first; this mode's quality is bounded by the brief's.

The counterpart. Lane A is this skill. Lane B is a skill builder from a different tradition: the harness's stock skill creator is the usual choice (Claude's and Codex's ship one, and most harnesses have an equivalent under some name). The name matters less than the lineage. Tune lane B's instructions to that tool's actual strengths rather than to assumptions about it.

The type lens, which shapes the divergent-strengths instructions and the consolidation rubric (`../references/type-lens.md`).

Output paths for each lane's draft, conventionally a scratch folder named for the skill, one file per lane.

## Phases

### 1. Brief preparation

Verify the brief covers project context and reading order, the target skill's purpose and any stub, source pointers, hard constraints, required capabilities and outputs, a test fixture if applicable, form and style expectations, and output paths per lane. A thin brief produces two thin drafts and a thin merge, so this is where to spend the time, and `interview` is where to go when it is thin.

If prior dual-lane runs exist in the project, read them before launching. Two things to mine: which lane tends to provide the backbone in this project's house style, so the instructions can lean into the productive contrast rather than restating defaults; and recurring length, schema, or vocabulary issues the brief should pre-resolve. Add these as a short lessons-from-prior-runs section in the brief so both lanes pick them up.

### 2. Divergent-strengths instructions

Append instructions to each lane's prompt telling it what to optimize for. The type-specific templates are `../references/divergent-strengths-templates.md`. The standard contrast: lane A optimizes for procedural clarity and vocabulary discipline (explicit definitions, diagnostic vocabulary, pseudocode where it sharpens, a `RATIONALE.md`); lane B for principled flexibility and agent-directed voice (failure mode as the headline, a section on how the agent talks to the user, principles over checklists where judgment matters). Creative skills push the lanes toward anti-collapse and voice; technical skills toward invariants and edge cases; hybrid gives each lane discretion per section.

### 3. Parallel spawn

Launch both lanes as background subagents when the harness allows it, so the main thread can write the next brief or consolidate a prior wave while waiting. Each lane reads the brief, runs its builder end to end to a written draft at its path, and returns a short self-summary: what differs from any prior stub, the judgment calls made, concerns.

Wait for both. If a lane fails with a transport error before producing a draft (sockets close, providers hiccup, roughly one call in twenty in observed practice), relaunch the same prompt; the brief is unchanged and the failure is transient. Fall back to single-lane only when a retry also fails, and say so.

### 4. Merge, or pause

By default, when both lanes return, run `consolidate` with both drafts. When the user wants to see the two drafts before the merge, stop here and hand them over.

### 5. Log

A decision-log entry for the run as a whole: what the brief asked for, what each lane produced (paths and a line each), what the merge kept from each lane and discarded (from the consolidation rationale), any TBDs. If the project keeps a design-decisions file, this entry can live there.

## Principles

Both lanes are first-class. Don't pre-rank. The instructions make them optimize for different things so the merge has real choices, not so one is primary.

Don't run two lanes of this skill. Same lineage, same instincts, no second opinion.

The merge is its own mode. This one briefs, spawns, waits.

## Failure modes

Drafts that differ in wording and make the same calls: the instructions were too weak. Strengthen them for next time per the templates file; this run's merge is faster and teaches less.

A lane that stalls or returns an unusable draft after a retry: say so, merge from the surviving lane with a note that it was single-lane, and consider running the counterpart again separately.

Both lanes asking the same clarifying questions or making the same wrong assumption: a phase 1 failure. Back to `interview` to strengthen the brief, then retry.
