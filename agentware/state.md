# os-agentware: build state

**Freshness:** 2026-10-27

## What this system is

The open-source home of agentware: the doctrine, the `os-agentware` skill for creating and improving agentware systems, the `os-showrunner` skill for running one, and the small set of companion skills and shared references they need to work outside Personal OS. This repo is itself an agentware system and keeps its own state here.

## The ask, verbatim

> "The os-agentware skill was written mostly by AI and has some significant flaws. It's written in a very AI-like register, focused perhaps too much on gates, and cannot stand alone outside of Personal OS. I would like to refactor this skill such that it can be shared and opensourced on github and it should come with some of the related skills that are necessary to allow it to function."

> "Perhaps one of the other main failures is that the current skill is fairly emphatic that this is not code/software, when in fact agentware is AI+skills+agents+code+process. [...] Scripts and little bits of GUI and other tooling are mission-critical."

> "I think showrunner's should have their own skill, as many other agents do, and it should be independent of the os-agentware skill which the showrunner might invoke. the os-agentware skill should be for creating, modifying, maintaining, and improving agentware systems at a general level. This can be combined with knowledge of a specific agentware system which may even supercede some of the principles in the agentware doctrine."

> "Let's create os-agentware-2.0 fresh, rebuilding the entire skill and system from scratch [...] write the skill in my style and register, and use /os-skillify and its principles throughout. We can reference the existing agentware skill and associated resources, but we should not assume they are valid or correct."

Rulings on the open questions (2026-10-27): new repo, keep the `os-` prefix. Agentware is the concept, the showrunner is the one making it happen. Companion skills come along in as much fullness as is useful with the Personal OS mandates stripped; the same primitives and folder structure, refined into suggestions the agentware considers, flexing to the project's conventions and the harness's. No outside research; this is built from Rob's own thinking and projects. Fable 5.1 for any subagents, with final review staying here.

## Done looks like

A repo someone can clone into a project (or symlink into their skills folder) and get a working showrunner plus the ability to create and improve their agentware, with no reference back into Personal OS. The doctrine reads like Rob wrote it. The old skill's gate-heavy register and "this is not software" stance are gone. Personal OS installs the skills from this repo instead of carrying its own copies.

## Budget

This session and its review passes, sliced: doctrine and map (done), os-agentware skill, os-showrunner skill, companion skills and shared references, review and cleanup, publish. Rob rules at the checkpoint after each slice that changes shape.

## Undo

Nothing outside this repo changes until the publish slice. Delete the folder and nothing is lost but the work.

## In flight

- Slice 1 done: doctrine, frame, map. Rob ruled: map holds; hazmat folds into skillify as a mode; append-only state files get trimmed and archived so only what is active or recently completed loads.
- Slice 2: drafting `os-agentware` (SKILL, modes create/improve/audit, references).
- Next checkpoint: Rob reads the os-agentware draft before the showrunner is drafted.

## Deferred

- Personal OS cutover: replace `~/personal-os/skills/os-agentware` with a link into this repo, and decide whether os-skillify and os-hazmat in Personal OS become links too or stay as the richer house versions. (2026-10-27, after publish)
- Whether `os-checkpoint` or a slimmer thread-closeout belongs in the companion set. (2026-10-27)
- A worked example project in `examples/` so a stranger sees the layout in use. (2026-10-27)
