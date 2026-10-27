# Rationale: os-skillify

Why this skill is shaped the way it is. For the person maintaining it and for the next rewrite pass. Not loaded by the skill; nothing in SKILL.md points here on purpose.

## Shape

**Modes and the type lens stay independent.** The mode says what skillify does (convert, build, extend, refine, audit, merge, clean up). The type lens (creative, technical, hybrid) says how the mode adapts. They blend rather than conflict because a type is a lens applied across operations, not another operation. If a type-specific operation ever diverges in steps rather than only in content, it should split into its own mode. That right is reserved.

**Everything that touches an instruction file lives in one skill.** Generative modes, the working modes (extend, refine, enhance), the merge modes, and the cleanup pass share the same opening step (read the project first), the same write discipline, the same prompting principles, and the same disposition vocabulary. Splitting them into sibling skills would duplicate the opening and the discipline, and it would spend listing slots the doctrine says to conserve.

**Cleanup is a mode, not a skill.** It was a separate skill in the workspace this was ported from. The ruling that folded it in: fewer skills, one place for everything about writing instruction files. The three-piles method and the review table survived intact because they are what makes the pass tolerable for the operator; a single giant review table is how these passes lose weeks.

**Extend and refine are modes here, not in a separate tuning skill.** In the source workspace they belonged to a tuning meta-skill that also carried session close-out, pattern reflection, and routing. None of that travels. What remained was two edit operations on existing skills, which belong beside the generation operations that create them.

**Dual-lane names a counterpart of different lineage** rather than saying "run twice." Two runs of this skill produce two drafts that vary in wording and share the same instincts, which is not a second opinion. Telling each lane what to optimize for is part of the design, encoded in the divergent-strengths reference, because two lanes told the same thing come back the same underneath.

**Consolidate is its own mode** because it has standalone value (two drafts from anywhere) and because separating it lets dual-lane stop short for a human read of both drafts.

**Interview is a top-level mode** because brief quality bounds everything downstream. The narrower clarification inside microtool-from-job shares its craft and its reference but stops at design-readiness.

**The type lens defaults to "ask once."** Inferring wrong silently is worse than asking. Requiring an answer every time is friction. Asking once when the input doesn't make it obvious is the middle.

**Hybrid means the user picks per section**, not both checklists applied wholesale. Both at once produces bloat.

**Show-before-write is the one real requirement.** Nearly everything else in this skill is advice with its reason. This one holds because these are the files that write the next files, and a wrong edit that lands silently propagates before anyone sees it. The frontmatter rules hold for a plainer reason: a skill that breaks them fails to install.

## modes/cleanup.md

The three classes (correctness, craft, register) want three different kinds of attention: verification against the files, the skill-writing principles, and the humanize method. Collapsing them into one review is how passes lose weeks. A collection of operator-approved before-and-after edits pulls a model toward the operator's standard more than any rule file, which is why high-stakes passes load the whole collection and why each pass feeds it. The log entry at the end is optional and project-local now; in the source workspace it was a dedicated file, and a pass that doesn't write down what it learned still repeats itself, so the entry goes wherever the project already keeps such things.

## What the port dropped, and why

This skill was ported from a private operator workspace into this standalone repo. The method travels; the workspace's mandates don't.

**The inheritance protocol.** The source loaded a fixed stack before any mode ran: a user profile, voiceprint files, org rules, an inbox of corrections, a system tracker, a setup-philosophy file, usage logs, a briefs folder, all at workspace-specific paths. It became the "Before writing anything" section: read the project's context file, the existing skills, any voice samples or style notes, and the agentware doctrine when the project is a system. Written as what a good author does, not as a gate, because a gate that names files a project doesn't have blocks work the user wanted.

**The routing reference and the tuning skill.** Figure-it-out routing became two sentences in the existing-skills paragraph. The close-out and reflect modes of the tuning skill didn't come along; they depend on the workspace's inbox and tracker.

**Library save and find, and the workspace layout contract.** Outputs save where the project already keeps such things. The layout reference was a thirty-page contract for one workspace's directory tree; the path-depth rules it carried moved into naming-conventions.

**Proactive prompting.** The source had a reference describing when to offer "want to make this a skill?" based on usage logs and a rejection-state file. The only part skillify relied on, the instant offer for freshly earned tool knowledge, was folded into the tool-wrapper reference.

**Creative criteria and the fresh-eyes, content-interview, and knowledge skills.** The criteria reference was pointed at from one see-also line and nothing in skillify used it. The skills are described generically where the capability matters (a skeptical second read, a one-question-at-a-time interview) and otherwise not mentioned, because they don't exist in this repo.

**The 900-character shipping budget and release lint.** The 1024-character platform limit stays because it is a limit. The lower budget existed so the source workspace could ship skills with headroom for customization, and the lint that enforced it lives there.

**Auto-save snapshots.** The source wrapped every write in a named snapshot and commit through a workspace skill. Here each mode says to take a restore point first if the project keeps them, in whatever form it keeps them.

**The workspace's name, "the pack," "the buyer."** Rewritten for a repo someone clones into their own project.

Nothing in the method was dropped: the six phases of from-prompt, the craft-preservation moves, the seven-section microtool anatomy, the type lens, the question bank, the divergent-strengths and consolidation rubrics, the cluster signals, the disposition vocabulary, the three piles, the review table, and the humanize method all came through. What changed is the register where it had drifted (gates rewritten as advice with reasons) and the paths.
