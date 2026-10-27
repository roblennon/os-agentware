---
name: os-skillify
version: 1.0.0
description: >-
  Write, change, audit, and clean up skills and the instruction files around
  them. Generative modes route by input: from-prompt (convert a prompt, SOP, or
  persona), from-content (a multi-mode skill from an article or transcript),
  microtool-from-content and microtool-from-job (one focused tool, installed or
  copy-pasteable), interview (build the brief first). Working modes: extend (add
  a mode to an existing skill), refine (fold a tweak or correction in), enhance
  (audit a skill or a library for redundancy, drift, and splits), dual-lane and
  consolidate (two drafts, one merge), cleanup (the pass after AI writes or
  rewrites instruction files). Triggers on "skillify this",
  "make me a skill from X", "add a mode to", "fold this into the skill", "audit
  my skills", "this skill sounds like AI wrote it", "run hazmat". Do NOT trigger
  for building or auditing a whole agentware system (os-agentware) or for
  editing ordinary prose.
---

# Skillify

Skills, modes, references, SOPs, and the context files a harness loads shape everything written through them afterward. Everything about how they are written leaks into what they produce: the register, the shape, the rules, the examples. This skill is the one place for making those files and keeping them good: new ones from a prompt or a body of content or a stated need, new modes on existing skills, tweaks folded in from use, audits across a library, and the cleanup pass that runs after any of that, so the next rewrite doesn't inherit this one's tics.

What it adds over a stock skill builder is two things. It reads the project before it writes, so the result fits what is already there instead of starting from a blank slate. And it writes the house way: `../_shared/references/skill-prompting-principles.md` is the current list of the ways a generated skill goes wrong and the counter-move for each. Load that file before producing any file here rather than working from memory, because it grows.

## Before writing anything

A good author reads the room first. Four things, in whatever order the project makes natural:

The project's context file (`AGENTS.md`, `CLAUDE.md`, or the harness's equivalent) and its conventions: where files go, how they are named, what the project already insists on. A skill that ignores these reads as foreign the day it lands.

The existing skills. Scan names, descriptions, and mode lists. The question is whether the ask is really a new skill at all. A request that is feedback on a skill the user just ran is `refine`. A request that fits as another mode of a skill that exists is `extend`. Only what is left goes to the generative modes. Say which you think it is and why, and let the user override; a strong match against an existing skill is worth a sentence even when the user asked for something new, because a duplicate is the most expensive thing this skill can make.

Any voice samples, style notes, or voiceprints the project keeps. Prose in a produced skill should sound like the operator, not like a model, and the samples are how that happens. With none on file, say so and write voice-neutral rather than inventing a voice.

The agentware doctrine, when the project is an agentware system: `../os-agentware/references/agentware.md`, especially what it says about skills, SOPs, gates, and absolutes. A project's own doctrine wins where the two disagree.

When something you would normally read is missing, say so. Silent approximation is the failure this section exists to prevent.

## Modes

Pick one and open its file. The mode files are written to be read, not inferred from their names.

Generative, routed by what you are starting from:

- `modes/from-prompt.md`: an existing prompt, SOP, or persona with craft worth preserving. Six phases from classification to a decision log, so nothing is lost silently.
- `modes/from-content.md`: long-form content (article, transcript, chapter) that covers a domain with several jobs in it. Produces a full skill with modes.
- `modes/microtool-from-content.md`: the same kind of content, one tight job. An installed single-mode skill or a copy-pasteable prompt.
- `modes/microtool-from-job.md`: a stated need, pain, or concept with no source content. Runs a short clarification interview when the need is thin.
- `modes/interview.md`: build the brief conversationally when the input is thin. The brief bounds everything downstream, so this is craft, not setup.

Working on what exists:

- `modes/extend.md`: add a mode to an existing skill. One new file, one index update, both shown together.
- `modes/refine.md`: fold a tweak, a correction, or a changed default into an existing skill. Smallest edit that does the job.
- `modes/enhance.md`: audit one skill, a cluster, or the library for redundancy, drift, missing structure, and skills doing two jobs. Operates on live files, so it takes a restore point first.
- `modes/dual-lane.md`: draft a foundational skill twice, from one brief, with two builders of different lineage, then merge. Worth the cost only for skills that carry real weight.
- `modes/consolidate.md`: merge two drafts into one with a written rationale. Runs on its own or as the end of dual-lane.
- `modes/cleanup.md`: the pass after AI has written or rewritten instruction files. Correctness, craft, and register, in three piles the operator can rule on.

When a request mixes modes, name the chain (interview then dual-lane; from-prompt then enhance on the cluster it joins). When it fits none of them, say so, handle it once with the closest mode and the gaps named, and offer to add the mode next time if the shape recurs.

## The type lens

A setting on top of any mode: `creative`, `technical`, or `hybrid`. Creative skills fail by sounding like AI wrote it; technical skills fail by breaking in production; hybrid skills have sections of each. The lens changes which questions get asked, which stress tests apply, and which sections the produced skill carries. It does not change which mode runs. When the input doesn't make the type obvious, ask once. Guessing wrong silently costs more than the question. The framework is `references/type-lens.md`.

## How this skill works

**Show before you write.** A file write, new or changed, is shown first and waits for a yes, and the yes can cover a class of change the user has already ruled on. This one is a real requirement, not advice: a wrong edit to a skill lands in everything that skill produces before anyone sees it. The discipline, including the sanity checks that run after each write, is `../_shared/references/skill-update-protocol.md`.

**Nothing gets dropped without saying so.** Every conversion produces a decision-log entry. Every consolidation says what was kept from each draft and what was discarded. Every audit finding gets logged, including the ones where the answer was to do nothing, so the next audit doesn't re-surface them cold. Where the log lives is the project's call; the template is `templates/decision-log-entry.template`.

**Preserve craft and phrasing.** When the source's wording is effective, reuse it verbatim. If the source has named frameworks, use their names and their structure. If it has three pillars, the skill has three pillars, not five for symmetry. Working out what the source implies is fine. Adding what it doesn't have is not, unless invention is the job.

**When two drafts disagree on substance, pick or punt.** Pick deliberately with the reasoning written down, or mark it TBD and hand it to the user. Splitting the difference produces a position nobody chose.

**Descriptions route.** A produced skill's frontmatter description is a routing prompt: the job, the distinctions that affect selection, the modes, the trigger phrases, and a "Do NOT trigger for X" when confusion with a neighbor is real. The rules that decide whether a skill installs at all are `../_shared/references/frontmatter-format.md`, and they are the one place in this skill where the hard limits are hard.

**Additive skills get the self-extending pattern; complete skills don't.** A skill whose value compounds with use (a writing skill meets a sixth format, an editing skill a fifth lens) should surface a gap, offer two paths, and hand off cleanly. A skill that does one stable job once well should not carry that section. The distinction and the pattern are `../_shared/references/self-extending-skills.md`.

**Rationale lives in an unlinked file.** Why a skill is shaped the way it is, what an earlier version did, what was dropped: that goes in `RATIONALE.md` at the skill root, and nothing in the skill links to it, so it never loads on trigger. Only the one sentence of why a rule needs to be applied well stays inline, beside the rule. `references/rationale-extraction.md` says what goes where.

**A reference moves to `_shared/` once a second skill needs it for the same reason.** Waiting for a third risks two copies drifting.

**Skills ship empty.** No user-specific names, accounts, or filter lists inline. Those belong in the project's own files, loaded at run time.

**Outputs save where the project already keeps such things.** No per-skill save scheme.

**Pace findings.** Audits and cleanup passes turn up a lot. Bring the operator a few at a time, ranked, with the rest held back until they ask.

**Count the listing cost.** Every skill costs something in every session, because its description sits in the harness's standing context, and most harnesses cap that listing and degrade it quietly. After generating, offer the check in `../_shared/references/context-capacity.md` once. What to tier is the user's call.

**Run cleanup after writing.** Finish the files and their basic checks first. Then open `modes/cleanup.md` as a separate pass over the finished files. Don't load its catalog or method during generation; a model that is holding a list of tells while it writes produces different tells.

## Tool-wrapper skills

When a session has just learned to drive an external tool the hard way (docs fetched, auth untangled, an MCP's real tool names discovered, a working invocation finally landed), offer to bank it as a small wrapper skill, or extend the existing wrapper for that tool. This offer doesn't wait for a pattern to repeat; the knowledge evaporates at session end. Generation routes through `modes/microtool-from-job.md`. What a wrapper has to contain to be worth more than a doc-dump is `references/tool-wrapper-skills.md`. Load it before generating one.

## References

In `references/`:

- `classification-taxonomy.md`: the chunk categories `from-prompt` tags in phase 1
- `rationale-extraction.md`: how to surface the why, and the split between inline why and `RATIONALE.md`
- `craft-preservation-from-content.md`: how the content modes keep the source's frameworks, terms, and phrasing
- `microtool-anatomy.md`: the seven-section structure the microtool modes produce
- `output-format-tradeoffs.md`: installed skill versus copy-pasteable prompt
- `interview-the-need.md`: the question bank for both the short clarification and the full brief
- `type-lens.md`: creative, technical, hybrid
- `divergent-strengths-templates.md`: what each lane optimizes for in `dual-lane`
- `consolidation-rubric.md`: how `consolidate` weights the two drafts
- `cluster-coherence-signals.md`: what `enhance` looks for when deciding to merge, split, or leave alone
- `disposition-vocabulary.md`: the fixed labels for what happened to a source or a finding
- `prompt-based-vs-tool-wrapper.md`: the early triage that separates a prompt from glue around a tool
- `tool-wrapper-skills.md`: the contents standard for a wrapper skill
- `humanize.md`: the register-repair method `cleanup` calls

In `../_shared/references/`:

- `skill-prompting-principles.md`: how every produced file is written
- `skill-update-protocol.md`: show before write, and the checks after
- `frontmatter-format.md`: the rules that decide whether a skill installs
- `naming-conventions.md`: names for skills, modes, references, and files
- `skill-vs-mode-vs-reference.md`: where a piece of knowledge or logic belongs
- `self-extending-skills.md`: additive versus complete, and the three-beat pattern
- `example-rules.md`: when examples help and when they mis-train
- `scaffolding-patterns.md`: assessing what looks like coaxing before dropping it
- `sop-completeness.md`: grading whether a procedure can actually be handed to someone
- `ai-writing-patterns.md`: the catalog of what machine-written prose does
- `context-capacity.md`: the listing budget and the levers

Templates in `templates/`: `SKILL.md.template`, `mode.md.template`, `reference.md.template`, `RATIONALE.md.template`, `decision-log-entry.template`, and `review-table.md` for cleanup's taste findings.

## Related skills

- `os-agentware`: decides what a system needs written. This skill writes it, and runs the cleanup pass after.
- `os-showrunner`: runs a project and calls this skill when a skill or SOP needs making or mending.
