# Mode: extend

Part of `os-skillify`. Selected when a request fits as another mode of a skill that already exists, either because the parent skill's existing-skills check found the match and the user agreed, or because the user named the target outright: add a mode to the email skill for X, extend the showrunner to handle Y. Not selected when the new behavior contradicts the host skill's purpose or is large enough to be its own skill (then a generative mode), or when the user said "new skill" and meant it.

## Job

Add a mode to an existing skill rather than making a new skill that duplicates intent. The skill grows while staying coherent. This is the payoff of checking for an existing skill first.

## Inputs

The target skill's path. The new behavior, in the user's words. Optionally, source material that fuels the mode's design: examples, content, prior outputs.

## Run

Read the target's `SKILL.md` to understand its scope, mode boundaries, and operating principles. Read its existing modes for shape: how they open, how they are structured, how long they run. A new mode that reads as if a different author wrote it breaks the skill's coherence, so mirror the shape.

Design the mode following that shape, with `../../_shared/references/skill-prompting-principles.md` loaded first. Mirroring the host and applying the principles point the same way most of the time. Where they conflict (the host predates the principles and is bullet-heavy in a prose domain), surface the conflict rather than silently choosing; the user may want the host brought up to the principles at the same time.

Load `../../_shared/references/self-extending-skills.md` and consider whether the host should gain the self-extending pattern alongside the new mode. A recurring "add mode X to skill Y" is itself a signal the skill is additive. Offer it; don't add it silently, and don't add it to a skill that does one stable job.

Update the host's mode index and its frontmatter description so the new mode is reachable. Before showing the change, count the folded description exactly and report its length and the room left under the 1024-character platform limit. Crossing 1024 breaks the install, so if the addition would cross it, stop and propose a compression that keeps the host's modes, its likely trigger phrases, and its real sibling boundaries.

Show both files together before writing: the new mode in full, and the `SKILL.md` change as a diff. Writes follow `../../_shared/references/skill-update-protocol.md`; two files change in this mode and both diffs surface in one batch. Take a restore point first if the project keeps them. After writing, check that the skill still parses and the new mode is reachable from the host's routing.

## Edge cases

The new mode would duplicate an existing one: say so, and route to `refine` (the user may mean "tweak the existing mode") or ask whether they really want two.

The new mode would touch logic that lives in another skill: flag the dependency and ask how to handle it (extend both, extract a shared reference, or keep as-is and point).

The host skill came from somewhere else (a shared library, a published set) and may be updated upstream: note that the customization is theirs, and consider whether the addition is personal or something every user of that skill would want, in which case it is worth suggesting upstream.

## After this mode

Run the new mode on a real input. `cleanup` over the new file and the changed index.
