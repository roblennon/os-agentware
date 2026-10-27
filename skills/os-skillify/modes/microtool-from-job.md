# Mode: microtool-from-job

Part of `os-skillify`. Selected when the user has a need and no source: a pain point, a concept they want operationalized, a job-to-be-done described in their own words. Content to build from goes to `microtool-from-content`; a multi-mode skill goes to `from-content`; a working prompt goes to `from-prompt`. This is also the mode a tool-wrapper skill routes through.

## Job

Design a single-purpose tool from a stated need, with a short clarification interview when the need is too thin to design from. Output is an installed single-mode skill or a copy-pasteable prompt.

## Before the steps

The parent skill's read-the-room step has run. Load `../../_shared/references/skill-prompting-principles.md` before writing. Because this mode designs from a need rather than from source text, the pull toward filling placeholders with concrete sample phrasings is unusually strong. Placeholders name the effect each slot should produce.

Load `../../_shared/references/self-extending-skills.md` and decide additive or complete. Asking the user whether the need is likely to recur in new shapes, or is stable as described, usually settles it.

When the need is an external tool the session just learned to drive, load `../references/tool-wrapper-skills.md` too. It says what a wrapper has to contain to be worth more than a doc-dump.

## Inputs

A statement of need, in whatever shape it comes. The output format, installed or copy-pasteable, asked once if not stated. Optionally: who the tool is for, tone or stylistic direction, similar tools the user liked or disliked, a voice sample.

## Steps

### 1. Read the need

Try to identify three things: the input (what the user has when they want to use the tool), the output (what it should produce), and the transformation (the move between them). If all three are clear, skip to step 3.

### 2. Clarify, only if needed

When one of the three is missing or ambiguous, ask about it. One question per turn, biased toward the missing piece, two to four questions to reach design-readiness, and no drift into a full requirements session. The question shapes and the draft-when-asking-stops-working move are in `../references/interview-the-need.md`, scope A. If the conversation goes recursive, show a best-guess draft with its assumptions labeled and let the user redirect; a draft to react to is easier than questions to answer in the abstract.

### 3. Confirm the format

Installed or copy-pasteable, per `../references/output-format-tradeoffs.md`. Ask once if not stated.

### 4. Design

The seven-section anatomy in `../references/microtool-anatomy.md` applies. Without source content the tradeoffs differ: there are no frameworks to mirror, so the structure comes from the job (borrow a well-known framework when the user names one; don't invent one); there are no verbatim phrases to lift, so the voice comes from the user's direction or a plain professional default; and the input and output sections carry more weight, because nothing else anchors the transformation.

### 5. Output

Writes follow `../../_shared/references/skill-update-protocol.md`. Installed: the full single-mode skill folder. Copy-pasteable: one code fence with the seven sections, a line above naming the job, and a suggestion in the surrounding message about where to keep it.

Show the tool. Common adjustments: tighter constraints, a different persona, a sharper process, a cleaner output format.

## Constraints

Don't design from a thin need; clarify first. Don't over-interview either; two to four questions is usual, and past that a draft beats another question.

Don't invent frameworks. Borrow a named one when the user names it.

One tool per run. Other jobs that surface during the interview get noted as candidates for later.

## After this mode

Test on a real input and iterate (through `refine` for an installed skill, direct edits for a prompt). If the user later finds content that captures the framework better, re-run as `microtool-from-content`. If the job turns out bigger than one tool, `from-content` once there is content. Then `cleanup` for anything installed.
