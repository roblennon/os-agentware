# Mode: enhance

Part of `os-skillify`. Selected when the work is on skills that already exist: audit one, a cluster, or the whole library; consolidate siblings that share vocabulary and references into a category skill; split a skill that does two jobs; modernize patterns bound to an old harness or a private setup; fill in missing structure across a set. A tweak to one skill is `refine`; one new mode on one skill is `extend`. This is the cross-skill surface.

## Job

Audit and improve live skills without losing what works. The mode modifies files people already depend on, so the workflow is built around that: a restore point first, changes ordered by how easily they reverse, a check after each one, and a log of the lineage.

## Before the phases

The parent skill's read-the-room step has run. Its existing-skills question is turned around here: everything is an existing skill, so the question is whether a consolidation or split affects skills outside the surveyed set. When it does, say so before applying.

Writes follow `../../_shared/references/skill-update-protocol.md`, with the restore point and per-change check below layered on, because a bad consolidation cascades.

## Setup

Confirm with the user before scanning: the target skills (one, a cluster, or an arbitrary related set); where working artifacts live during the run (audits, logs, restore points), conventionally a dated scratch folder; and what the run is optimizing for. The usual goals: cohesion (find redundancy across siblings and consolidate where two skills load the same thing for the same reason), idiom alignment (modernize patterns from another harness, another era, or another machine), splits (skills doing two distinct jobs), mode additions, structural completeness (missing negative triggers, a rationale section still sitting inside a loaded file, missing `RATIONALE.md`, example gaps), or a specific goal in the user's words. The type lens, if given, shapes what stronger means: for creative skills, more voice-protective and more disciplined craft; for technical, more precise and better edge-case coverage.

Then take a restore point. A git commit, a snapshot, a copy of the target folders: whatever the project uses. Skills aren't always in a clean state when an audit starts, and this is the rollback path.

## Phases

### 1. Survey

For each target skill, read `SKILL.md`, every mode, every reference, every template. Build a profile: the job in one sentence, the inputs, the run shape (numbered steps, a mode router, one workflow), every reference it loads including shared ones, its templates, which other skills it invokes, and any legacy artifacts (machine- or harness-bound paths, outdated delegation rules, custom scheduling, state files the project doesn't use). Write each profile to the working area. For multi-skill audits, add an overlap matrix: pairwise vocabulary, reference, and job overlap.

### 2. Detect signals

Scan the profiles for the patterns in `../references/cluster-coherence-signals.md` and bin the findings: consolidation candidates (shared vocabulary, the same reference loaded from different paths, job-shape overlap); split candidates (different reference sets per mode, different output shapes, different invocation patterns); drift candidates (custom scheduling, delegation rules from an old policy, state files from a specific setup, hard-coded paths, cross-references to skills that don't exist here); structural gaps (no negative trigger, a rationale section in a loaded file, no `RATIONALE.md` when the skill has rationale anywhere, example gaps, noting that an empty `examples/` folder is sometimes correct per `../../_shared/references/example-rules.md`); and promotion candidates (references duplicated across skills that haven't moved to `_shared/`). Write the findings down.

Load `../../_shared/references/scaffolding-patterns.md` when a survey turns up suspected coaxing in a skill body; the three questions there decide whether it is doing work.

### 3. Surface decisions

Give each finding a disposition from `../references/disposition-vocabulary.md`: consolidate, split, adapt, augment, defer, or no-op. Bring the borderline calls to the user one at a time, with no more than three options and your pick: whether a look-alike pair should merge or is intentionally distinct (same vocabulary for different reasons is real, and a no-op with a note is sometimes right); whether a meta-skill stays standalone or becomes a mode; whether a legacy idiom gets adapted now or waits until it actually gets in the way; whether a two-job skill splits or stays bundled because the jobs are tightly coupled. Apply the clear ones directly (a missing negative trigger, a reference duplicated across three skills) with a log entry each.

### 4. Apply, ordered by reversibility

Promotion and consolidation first: they create shared references and delete nothing yet. Augmentation second: it adds missing structure. Adaptation third, with a per-change confirmation, because it changes behavior. Splits last, per skill, because they create new files and then remove content from existing ones.

Show each change before writing it. Read the modified file end to end after each write; a check batched to the end loses the ability to attribute a regression. Log the change as you go, not in a final sweep. If a change misfires (a regression, craft lost, a garbled description), revert to the restore point.

### 5. Verify

For each modified skill: does it still do its original job (walk the run section against the original)? Does `RATIONALE.md` still describe the essential moves, and is the one-line why still beside each rule? Do all cross-references resolve? Is there orphaned text, a mode body still mentioning a reference that moved? Does the skill still appear correctly in the harness's listing with its negative triggers intact? For multi-skill runs, one verification file covering all of them.

### 6. Log

Per modified skill, a decision-log entry per `../templates/decision-log-entry.template`: date, goals, each change with its why and lineage, references promoted or created, adaptations (also recorded in that skill's `RATIONALE.md`, so a future maintainer reads why a change happened and not just that it did), splits, deferrals with what would unblock them, and verification notes. If the skill was created through `from-prompt`, append to its existing log rather than starting a new file; the log is the skill's full trajectory.

## Status updates

Four natural checkpoints: after detection (findings and proposed dispositions, before any change), after apply (what changed, what was deferred), after verify, and at the end (summary and recommended next steps). Pace the findings.

## Principles

Restore point before changes. Order by reversibility. Check per change. Confirm borderline calls; the cost of asking is low and the cost of a wrong merge over live skills is high. Findings tagged no-op still get a log entry, so the next audit doesn't re-surface the same pair without context.

## Cross-mode interactions

A `from-prompt` run that deferred sources for missing dependencies can come back through `enhance` when those dependencies land. An `enhance` run that finds a missing sibling (the cluster needs a skill that doesn't exist) hands off to `from-prompt` and then re-runs on the cluster. When two surveyed skills genuinely warrant a merge complex enough to want two drafts first, hand off to `dual-lane` from inside this mode. And `cleanup` runs over whatever this mode rewrote.
