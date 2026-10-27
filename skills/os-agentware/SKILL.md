---
name: os-agentware
version: 2.0.0
description: >-
  Create, improve, and audit an agentware system: the harness, AI, agents, skills,
  SOPs, scripts, tools, knowledgebase, and process that together do a kind of work.
  Modes: create (stand a system up, from nothing or inside an existing project),
  improve (fold learnings, corrections, and new tooling back into the system),
  audit (find drift, bloat, duplication, and rules that block wanted work).
  Triggers on "set up agentware for this", "build me a system for X", "fold this
  lesson into the system", "my system is drifting", "audit my AI setup", "too many
  skills". Do NOT trigger for running a project day to day (os-showrunner) or for
  writing one skill (os-skillify).
---

# os-agentware

This skill is for the system itself: creating one, changing one, keeping one good, making one better. Running a project inside a system is the showrunner's job (`os-showrunner`), and the showrunner invokes this skill when the stack needs work.

Read `references/agentware.md` before doing anything here. It is the doctrine, short, and the whole skill assumes you have it in your head. Not a summary of it, the file. If the project you are working in has its own doctrine or conventions (an `AGENTS.md`, a design doc, a way it already does things), read that too, and where the two disagree the project wins. The doctrine is the general case. A real system is the specific case, and the specific case is the one that has to work.

## What a system is made of

Agentware is AI plus skills plus agents plus code plus process. Any of these can carry the weight at a given step, and part of the craft is choosing which one should.

- **The harness and the AI.** Whatever runs the agents. Usually one of a few coding harnesses, sometimes several in the same project.
- **The showrunner, lieutenants, and workers.** The showrunner is the operator's interface and is responsible for the outcome. Lieutenants are showrunners with a specialty. Workers are anything that does a bounded piece of work: a subagent, a skill, a script, a tool, a one-off brief written at dispatch time.
- **Skills.** The registered procedures the harness can route to. Kept under fifty, related ones rolled into one skill with modes, shared references where one source of truth matters.
- **SOPs.** Procedures that are not registered. They cost nothing until someone opens them, so they can be long and thorough. Most procedures start here.
- **Scripts, tools, GUIs.** Code is a first-class part of the system, not an exception to it. When a step is deterministic, repeatable, or needs to be fast and exact, write code for it. Build it so both the agent and the human can use it, which usually means a command line first and a small GUI when a human needs to see something. Wrap it in the skill or SOP that knows how to use it well.
- **The knowledgebase.** Research, findings, decisions, sources. It grows without limit as long as it stays useful and searchable, and the agents actually search it when deciding things.
- **State.** What is in flight, what was decided, what is parked. Kept short, kept true, trimmed as things settle. The showrunner's default layout is in `../os-showrunner/references/project-state.md`; projects with their own tracker keep it.
- **Process.** The loop that routes learnings back in: a correction becomes a principle in a skill, finished research lands in the knowledgebase, a repeated manual step becomes a script. A system without that loop is prompting with extra steps.

## Modes

Pick one and open its file. The modes are written to be read, not inferred from their names.

- `modes/create.md`: standing a system up, from nothing or inside a project that already has conventions. Where to start, what to build first, how to install it so the harness finds it.
- `modes/improve.md`: folding something back in. A correction, a lesson, a repeated step, a new tool, a rule that turned out wrong. Also consolidating when the system has grown.
- `modes/audit.md`: looking at the whole thing for drift, bloat, duplication, orphaned files, rules that block work the operator wanted, and hygiene. Findings for the operator, ranked by how much daily work they touch.

## Principles that run through every mode

**Reuse before reinventing.** Look at what the project and the harness already have before building anything. Most of the time a piece of what you need exists and the job is to point at it or extend it. Building a parallel thing next to an existing one is how systems sprawl and nobody can say which copy works.

**Flex to the project and the harness.** A system built inside a project with conventions keeps those conventions. A system that wants to be harness-specific uses that harness's surfaces (its skills folder, its context file, its hooks). Otherwise stay agnostic and portable, favoring the open skills format and plain files. The layouts and shapes in this repo are defaults the agentware considers, not requirements.

**Principles over rules, and rules over gates.** How to write a rule so it survives contact with a case you did not anticipate, when a gate earns its place, and how to tell a real cause from a correlation when encoding a lesson: `references/rules-and-gates.md`. Load it at the moment you are about to write any rule, check, or gate into the system. That moment is where systems quietly go wrong.

**Encode the operator, not the model.** The hardest material in any system is how the operator actually works, which they have never had to articulate. The three ways to get it out of them, and the two traps when writing it down: `references/encoding-the-operator.md`.

**Scope to the goal.** Match the effort to the value. A typo does not need a review pass. A critical bug may need a plan, fresh eyes on the plan, the fix, fresh eyes on the fix, and a review. Planning and re-reviewing plans is usually higher leverage than re-reviewing outputs, because a problem caught while deciding what to do never becomes a problem in the output. Favor what is practical and showable. Notice when a sidequest has taken over.

**Find the root.** Ask why, then why again, until the mechanism is clear. Fix the bug in the shared helper, not the one call site. Fix the approach when the approach is the problem. Be willing to be wrong on the way to something better.

**Recency.** The harnesses, models, and tools move faster than any training data. Check versions and current behavior before building on them.

**Hygiene.** Clean up worktrees, caches, containers, and temp folders at milestones and checkpoints. Keep always-loaded files lean. Trim or archive state that has settled. Subagents keep the main thread's token use down; use them for reading, checking, and bounded work.

**Write skills the house way.** Skills, modes, SOPs, and references this skill produces get written through `os-skillify`, which loads `../_shared/references/skill-prompting-principles.md` and runs its cleanup mode after writing. Those principles are what keep a self-improving system from drifting into the model's default register, and that drift leaks into everything the system then produces.

## Related skills

- `os-showrunner`: runs a project inside a system. Calls this skill when the system itself needs work.
- `os-skillify`: writes and repairs skills, modes, SOPs, and references. This skill decides what to write; skillify writes it.
