# Mode: microtool-from-content

Part of `os-skillify`. Selected when the input is content (a transcript, article, podcast, chapter) and the user wants one focused tool from it rather than a full skill: the single highest-leverage move the source teaches. A multi-mode skill from the same content goes to `from-content`; a need with no content goes to `microtool-from-job`; a working prompt goes to `from-prompt`.

## Job

Design a single-purpose tool that does one thing well, either as an installed single-mode skill or as a copy-pasteable prompt someone can drop into any model.

## Before the steps

The parent skill's read-the-room step has run. Load `../../_shared/references/skill-prompting-principles.md` before writing the tool. The copy-pasteable format is especially exposed to verbatim-example leakage, because the whole prompt ships as one artifact that will be pasted into other models; placeholders describe the effect a slot should produce, not sample text.

Load `../../_shared/references/self-extending-skills.md` and decide additive or complete. Microtools lean complete (they are single-job by design), but a generator that grows with the user's examples is additive even at this scale.

Content that arrives as PDF, HTML, or scans gets converted to clean Markdown first if it will be kept as a reference, for the same reason as in `from-content`.

## Inputs

The source content (roughly five hundred to thirty thousand words). The output format, installed or copy-pasteable, asked once if not stated. Optionally: which move to build (the source usually implies several; without direction, the mode picks the highest-leverage one and asks), a voice sample when the tool should keep the user's voice, and examples of similar tools the user liked or disliked.

## Steps

### 1. Digest

Read everything. Note every tool the source describes or implies, its frameworks and signature terms and step counts, the verbatim lines that would lose force if paraphrased, and the outcomes it promises.

### 2. Pick the move

Surface two to four candidate tools in a line each, recommend the highest-leverage one with the reason, and let the user confirm or pick differently. Highest-leverage means: the source's most actionable move, the clearest input-to-output transformation, the one the audience would use most often. When the user already named the move, skip this.

### 3. Confirm the format

Installed skill when the tool lives in the project, expects iteration, and loads project material. Copy-pasteable when it will be used in another model, shared with people who don't have the setup, or dropped into a one-shot context. The full tradeoff is `../references/output-format-tradeoffs.md`. Ask once if not stated.

### 4. Design

The tool follows the seven-section anatomy in `../references/microtool-anatomy.md`: task, persona (when relevant), constraints, process walk-through, success qualities, output format, inputs. That file says what each section does, when to skip one, and how the anatomy maps onto a mode file versus a code fence.

Apply `../references/craft-preservation-from-content.md`: mirror frameworks by name, lift the memorable phrases, keep step counts exact, stay inside the source, use its terms.

### 5. Output

Writes follow `../../_shared/references/skill-update-protocol.md`. For an installed skill: `SKILL.md` and `modes/<name>.md`, plus a reference only if the craft needs more depth than the mode holds. For a copy-pasteable prompt: one code fence with the seven labeled sections, a line above naming the source and the move, and a line in the surrounding message (not inside the fence) suggesting where to keep it. Copy-pasteable output doesn't touch the project, so no restore point is needed.

Show the tool. Iterate.

## Constraints

One tool per run. If the source implies several, the user re-runs for each.

Don't pad. The seven sections fit on one screen for most jobs.

Lift verbatim where it adds fidelity. Paraphrase flattens the source's voice and authority.

When producing an installed skill, follow the house style. A copy-pasteable prompt follows the source author's voice instead; that is the point of the portable format, and it is why the house style's punctuation and list restraint don't apply inside the fence.

## After this mode

Test on real input. Iterate by re-running with adjusted direction, by direct edits, or through `refine` once it is an installed skill. If the tool wants to grow into a multi-mode skill, re-run as `from-content`. Save a copy-pasteable prompt wherever the project keeps templates. Then `cleanup` for anything installed.
