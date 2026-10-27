# Mode: refine

Part of `os-skillify`. Selected when feedback from using a skill should become the skill's default: the user ran it, got output, changed the output, and wants the skill to produce the changed version next time. Also when the user names a skill and a behavior change directly (fold this default in, trim this mode, it keeps doing X and shouldn't). Not selected when the user said the tweak was a one-off, when the "feedback" is really a new behavior (`extend` for a mode, a generative mode for a skill), or when the feedback is about voice and tone in general rather than this skill's behavior, which belongs in the project's voice samples or style notes, not in one skill.

## Job

Update an existing skill from how it was actually used. This is the self-improvement loop. Without it, skills stay frozen at their initial design and the user re-applies the same tweak every time. With it, a correction retires: the same work that used to need the catch every session needs it once.

## Inputs

The target skill, named or resolved from recent context. The output the user got. The tweak, edit, or direction. Optionally the why, which often decides where the change belongs.

## Run

Load the whole skill: `SKILL.md`, the relevant modes, the relevant references. Read everything that could be touched before deciding what to touch.

Decide which file the change belongs in. An output-formatting tweak usually belongs in a mode file. An operating-principle tweak belongs in `SKILL.md` or a principles reference. A voice or tone tweak may not belong in the skill at all. A new behavior isn't a tweak; route it to `extend` or a generative mode and say so.

Before writing the rule, find the root. A correction tells you what went wrong once. Ask why, and whether the stated cause would survive a counter-example. If a shorter, more specific rewrite would also have been fine, length wasn't the cause. A wrong rule is worse than no rule, because it runs every time. When the project is an agentware system, `../../os-agentware/references/rules-and-gates.md` carries the shape a rule should take: the reason, the exception, and a calibrated force. Load `../../_shared/references/skill-prompting-principles.md` before designing the edit; every principle there applies to revisions as much as first writes, and a "tighten this up" tweak on a writing skill can quietly turn prose into bullets.

Design the smallest edit that accomplishes the intent. Don't refactor while you are in there. If the change exposes a deeper issue, name it as a separate candidate rather than expanding scope.

Load `../../_shared/references/self-extending-skills.md` and watch for tweaks that are self-extension asks in disguise: the writing skill should handle VSLs too, the editing skill needs a new lens. When the target is additive and doesn't carry the three-beat pattern, the right move is often to add the pattern as well as, or instead of, the specific tweak, because the pattern handles every future ask in the same family. Offer that path before applying.

Show the diff with its reasoning: which file and section, the change itself, and one line connecting the user's intent to this edit, so they can check the inference before approving. Writes follow `../../_shared/references/skill-update-protocol.md`. For anything beyond a trivial edit, take a restore point first if the project keeps them. After writing, check that the skill still parses, still routes, and has no broken references.

## Edge cases

The tweak fights the skill's stated purpose: surface the conflict and ask whether to update the purpose too, or leave the skill alone and route elsewhere.

The tweak applies across several modes: update them together, diffs shown as one batch.

The user has raised this tweak before and it never got folded in: say so, and ask whether to fix that pattern too.

The tweak is really voice calibration ("warmer," "less formal"): say where it belongs and ask before applying. Folding voice changes into individual skills is how a set of skills slowly drifts apart in voice.

## After this mode

Run the skill again on the input that prompted the tweak. `cleanup` over the changed file.
