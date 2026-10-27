# Mode: consolidate

Part of `os-skillify`. Selected when there are two drafts of one skill and the job is to merge them into one with a written rationale: as the last phase of `dual-lane`, or on its own when the user has two drafts from anywhere. Editing one draft is `refine` or `enhance`; drafting fresh is a generative mode.

## Job

Produce one `SKILL.md` from two, with a rationale a future reader can use to trace why each choice went the way it did. The rationale is part of the output, not an optional extra; a merge without one is a file nobody can revisit.

## Inputs

Two draft paths, in either order. The destination path for the merged file. The type lens, inherited from the drafts or asked once; it adjusts the rubric. The original brief, strongly recommended: its hard constraints, required capabilities, and required outputs are the merge's correctness floor.

Writes follow `../../_shared/references/skill-update-protocol.md`. The merged draft and its rationale are shown together before anything is written.

## Phases

### 1. Read both drafts in full

Catalog the structural elements in each (frontmatter, sections, examples, tables, code), the voice and framing differences (one opens with a role statement, the other is procedural; one leads with failure modes, the other buries them), the vocabulary differences (same concept, different labels), the coverage differences (what each has that the other lacks), and the substantive disagreements (where they contradict each other). Write a short diff summary to drive the choices that follow.

### 2. Apply the rubric

`../references/consolidation-rubric.md` says which elements typically come from which lane and how the type lens shifts the weighting: creative skills favor voice protection, anti-collapse mechanisms, and failure-mode framing; technical skills favor invariants, edge-case coverage, and procedural rigor; hybrid weights per section. The rubric is a starting point, and in a project whose house style has settled, one lane usually provides the backbone while the other contributes targeted additions. Lean into that when it is clear; pick per element when it isn't.

### 3. Resolve substantive disagreements

When the drafts disagree on substance rather than framing, pick deliberately. Check against the brief's hard constraints first; usually one draft is brief-consistent and the other isn't. If both are, pick on craft grounds and write the reasoning into the rationale. If you can't pick with confidence, mark the point TBD in the merged draft and hand it to the user. Splitting the difference produces a position nobody chose.

### 4. Compose

Write the merged `SKILL.md` to the destination. Follow the project's house style if a sibling skill exists there: section order, vocabulary, link conventions. Length should match the more comprehensive draft, because the goal is the best of both rather than a shorter average; if both ran well over the brief's target, trim the elements with the weakest justification, usually redundant examples or over-explained reasoning.

### 5. Rationale

Inline as an appendix section in the merged file when it is short, or as a sidecar file beside the drafts when the skill should stay clean of merge noise. Minimum content: what each lane contributed, what was discarded from each and why, where they disagreed and which way the merge went and why, any TBDs left for the user.

### 6. Log

A decision-log entry with the input paths, the destination, and a pointer to the rationale.

## Principles

Both drafts are first-class inputs; the rubric weights, it doesn't rank. House style wins ties. The brief is the correctness floor: a hard constraint missing from the merged draft is a bug. Nothing is quietly dropped; anything from either draft that doesn't make the merge gets a line in the log.

## Failure modes

Keeping everything from both drafts, which produces a skill twice as long and worse than either: pick per element. Switching between role-statement framing and procedural framing mid-file: pick one voice. Two disposition taxonomies with overlapping labels in one skill: pick the cleaner one and say why. A merge with no rationale: phase 5 is not optional. Drift from the brief because neither draft was checked against it: verify the merged draft against the brief before calling it done.
