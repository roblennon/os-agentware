# Mode: from-prompt

Part of `os-skillify`. Selected when the input is an existing prompt, SOP, or GPT persona that works, and the job is to turn it into an installed skill, a mode of an existing skill, a shared reference, or a template without losing what made the original work. Long-form content goes to `from-content`; a stated need with no source goes to `microtool-from-job`.

## Job

Convert a hand-crafted prompt into skill files while preserving three things the original author spent time refining: the craft (the specific moves that shape output quality), the rationale (why those moves work), and the judgment (the heuristics that keep output sharp under edge cases). Scaffolding, the patches and incantations added to coax older models, is mostly noise on current models, but some of what looks like scaffolding hides real craft. This mode assesses rather than auto-drops.

## Before the phases

The parent skill's read-the-room step has already run: project conventions, the existing skills, voice samples if any. If the source overlaps a skill that exists, that was surfaced and the user chose to proceed.

Load `../../_shared/references/skill-prompting-principles.md` before phase 4 writes anything. It is what keeps a converted skill from regressing toward bullets-and-rules defaults, especially when the source is a writing or judgment job.

Load `../../_shared/references/self-extending-skills.md` during phase 3 and decide whether the skill being built is additive (its value grows as the user's modes, lenses, or coverage accumulate) or complete (one well-defined job, done once well). An additive skill gets the three-beat self-extending section in phase 4. A complete skill doesn't; adding it there is over-engineering.

When the source is an SOP, also load `../../_shared/references/sop-completeness.md` and grade it (runnable, partial, named-only) before converting. A partial or named-only SOP converts into a skill that performs confidence the source can't back, so show the grade and let the user decide whether to fill the gaps first.

## The six phases

Run them in order. Each produces something before the next starts, so a mistake gets caught where it was made.

### Phase 1: Classify

Read the source end to end. Tag every chunk into one of the categories in `../references/classification-taxonomy.md`: trigger and framing, craft moves, domain knowledge, output shape, examples, scaffolding candidates. The taxonomy file is the current list; read it rather than working from this sentence.

Craft moves are preserved verbatim. Domain knowledge goes to references. Output shape goes to templates. Examples get a disposition per `../../_shared/references/example-rules.md`. Scaffolding candidates get the three-question assessment in `../../_shared/references/scaffolding-patterns.md` before any decision, because hidden craft hides inside scaffolding more than anywhere else.

Write the classification table down somewhere in the project's working area before moving on. It is a checkpoint: a misclassification caught here is cheap, and one caught after the build is a rewrite.

### Phase 2: Surface the rationale

This is the phase that makes a converted skill trustworthy under edge cases. For every craft move and judgment heuristic, ask why it works.

If the rationale is stated in the source, even as an aside, lift it verbatim. If it is implicit, ask the user to articulate it before continuing. Don't guess; tacit craft is the most valuable thing being preserved, and a guessed reason is a wrong rule waiting to run. Record each as a one-liner: this move works because of that reason.

These notes become the skill's `RATIONALE.md`, an unlinked file at the skill root. Only the one sentence of why a rule needs in order to be applied well stays inline, beside the rule. `../references/rationale-extraction.md` has the prompting patterns, what not to capture, and the shape of the file.

### Phase 3: Plan the destination

Decide what the source becomes. Four options: a new standalone skill (a distinct job with no close siblings), a mode within an existing or new category skill (shares reference material with siblings), a shared reference only (pure domain knowledge, no job logic), or a template only (a stable output shape other skills use). The heuristic that does most of the work: if two prompts would load the same reference for the same reason, they are modes of one skill. The full decision tree is `../../_shared/references/skill-vs-mode-vs-reference.md`.

Also decide whether the skill wants companion agents. The test is whether the job involves two or more independent analytical passes that don't wait on each other. If so, plan one agent per parallel workstream and name them with the files.

Produce the plan: destination path, files to create, references to reuse, modes to group, agents if any.

### Phase 4: Build

Writes follow `../../_shared/references/skill-update-protocol.md`: show all proposed files as a batch, confirm, write, sanity-check each. If the project keeps restore points (a git commit, a snapshot tool), take one before persisting; a conversion is several files, and a clean revert target is cheap.

Create the files at the project's skills location, following the scaffolds in `../templates/`. For each converted skill:

- `SKILL.md`: trigger, run logic, pointers to references and templates. The description ends with a "Do NOT trigger for X" when confusion with an adjacent skill is likely.
- `RATIONALE.md`: the phase 2 notes, unlinked from everything else in the skill.
- `references/*.md`: extracted domain knowledge. Shared references go to `skills/_shared/references/` and are loaded by relative path.
- `modes/*.md`: for category skills with multiple modes.
- `templates/*.md`: strict output shapes, loaded only when the output has to match exactly.
- `examples/*.md`: per `../../_shared/references/example-rules.md`. Five to ten strong examples or none. A single dated example mis-trains more than no example does. Legacy examples kept with reservations carry a `legacy-` prefix and a note on what should replace them.
- Companion agent files, if phase 3 called for them, in whatever shape the harness expects (Claude Code, for one, reads `agents/*.md` with frontmatter and a system prompt in the body).

Naming follows `../../_shared/references/naming-conventions.md`. Frontmatter follows `../../_shared/references/frontmatter-format.md`: a `description: >-` block scalar, under 1024 characters, `name` equal to the folder name. Those rules are hard because a skill that breaks them fails to install.

### Phase 5: Verify

Run the converted skill against a representative input, real content the original prompt was built for, and compare the output to what the original produces. Four checks:

- **Craft preserved:** does the output show the same distinctive moves?
- **Rationale holds:** ask for a variation. Does the why left inline beside each rule give the agent enough judgment to adapt without breaking the thing? If the agent would have needed `RATIONALE.md` to get it right, that sentence belongs inline.
- **Example quality:** do the included examples still read as strong exemplars, or as dated AI output? Replace, drop, or flag.
- **No silent loss:** is there anything in the source that appears nowhere in the conversion or the decision log?

Write a verification note (the input, the output, the comparison) for the decision log. Skipping a check is how a conversion ships blander than its source without anyone noticing, so run and record the four. Failure shapes worth watching for: a dropped craft move that was doing work (converted output is blander), inputs the skill can't route between modes, a mode with no examples producing uneven output, and a variation request that breaks the skill (the inline why isn't teaching the right adaptation).

For a batch of related skills converted together, one batch verification file covering all of them is fine, with per-skill test plans and cross-skill notes.

### Phase 6: Log

Write a decision-log entry wherever the project keeps such things, following `../templates/decision-log-entry.template`: source, destination, disposition (the labels in `../references/disposition-vocabulary.md`), the classification table, rationale captured, what was dropped and why, example decisions, verification notes.

One source becoming one skill gets one entry named after the source. Several sources becoming one category skill get one consolidated entry named after the skill plus a thin stub per source pointing at it, so every source is still findable by name.

The log is what makes the conversion lossless: each source gets an entry or a stub, so nothing dropped stays dropped silently.

## Principles

Run all six phases even on a prompt that looks like a simple port. Those are the ones that most often hide the interesting craft, and the phases are fast once practiced.

Preserve wording on craft moves. When a chunk is a craft move, its exact phrasing is part of what makes it work.

Assess scaffolding; don't auto-drop. Hidden craft hides there.

Examples are high-leverage and high-risk. A bad one mis-trains the skill more than a missing one does.

TBD rationale can ship. If a why can't be resolved before the first version, name it as TBD rather than fabricating one.

References promoted to `_shared/` carry a section saying what you might change and what to generally leave alone, so they don't become sacred.

## After this mode

Run the produced skill on real input and fold any tweaks in through `refine`. If phase 3 surfaced a fold-in candidate (this should be a mode of an existing skill), run `extend` with the mode design instead. Then run `cleanup` over the finished files.
