# Mode: interview

Part of `os-skillify`. Selected when the user wants to think a skill through before anything gets drafted, or when another mode finds the input too thin to work from (no spec, no existing skill, vague intent, no named output, no boundaries). Not selected when a complete brief already exists; then the requested mode runs directly. The short clarification inside `microtool-from-job` is a narrower cousin, not this mode.

## Job

Build a skill brief conversationally. The brief bounds everything downstream: it is the correctness floor for `consolidate`, the divergence target for `dual-lane`, the scope for `from-prompt` and `from-content`, and the record of intent a later `enhance` run reads. Building it is craft, not setup overhead.

## Before the phases

The parent skill's read-the-room step has run, and it matters more here than elsewhere: the project's conventions, existing skills, and voice samples decide which questions are worth asking and which are already answered. This mode doesn't write skill files. The brief itself, when persisted, follows `../../_shared/references/skill-update-protocol.md`.

Quoted questions in the question bank are samples of the kind of question, not wording to reproduce.

## Phases

### 1. Sufficiency check

Read what the user already gave you. A complete brief, a thorough spec, or a skill stub that captures purpose, modes, inputs, and outputs means no interview is needed. Say what you have and confirm you can proceed to the target mode.

### 2. Settle the type

If the type lens isn't specified, settle it first, because the question pools differ: creative-leaning (variety, voice, subjective quality), technical-leaning (precision, invariants, verifiable results), or hybrid. When the user is unsure, asking which failure they fear most (output that sounds like AI, output that breaks in production, or both) usually settles it.

### 3. Targeted questions, paced

One at a time, or a small cluster of two or three that naturally go together. Wait for answers. Let answers shape the next question. A person can answer twenty-five questions at once, and the answers get worse with every one.

The core questions, in rough order, with the full bank in `../references/interview-the-need.md` (scope B): the one-line purpose; one concrete request the skill should handle and one adjacent request it should not; what good output looks like and what the model would produce by default that the user wants to prevent; what the skill doesn't touch and where it hands off; and what existing material (prompts, docs, examples, sibling skills) you should read first. The last one is often the biggest leverage in the interview. People have more than they remember to mention.

Type-specific follow-ups come from the same bank: for creative skills, the anti-collapse mechanism, persona and voice, the craft discipline, where variety helps and hurts, the per-output judgment points; for technical skills, invariants, test fixtures, boundaries, the production-breaking failure, edge cases; for hybrid, which sections want which lens, then the relevant follow-ups per section.

Skip any question whose answer is evident from what you already have.

### 4. Assemble the brief

Write it as a Markdown file wherever the project keeps working drafts (a scratch or experiments folder is usual). Standard sections, adapted to the project's house style: project context and reading order; the target skill's purpose and any existing stub; source material pointers; hard constraints; required capabilities and outputs; what runs at run time (inputs, loaded material); the hard things to get right, meaning the decisions that hinge on judgment; a test fixture if there is one; form and style expectations; output paths; and divergent-strengths instructions if the brief is headed to `dual-lane`.

### 5. Confirm

Show the brief and ask whether it captures what they want, what is missing, and what is wrong. Revise and re-confirm.

### 6. Hand off

Return the brief's path and name the next mode. The brief is now a first-class artifact the downstream mode consumes.

## Principles

Pace the questions. Skip the evident ones. Settle type early. Frame the question that draws out the user's judgment rather than the one that lets them rubber-stamp a generic skill; the goal is to get what they know onto the page, not to generate something for them to approve.

Don't manufacture scope. If the request is "a skill that helps with writing," don't expand it into a five-mode orchestration. Most thin requests are thin because the user hasn't decided yet, and the interview's job is to surface their thinking, not to scope it up.

When answers go short and noncommittal and the conversation turns recursive, stop asking and show a draft brief to react to.

## After this mode

The brief goes to whichever mode it was built for. `interview` then `dual-lane` (which ends in `consolidate`) is the most thorough path for a foundational skill. `interview` then `from-prompt` fits a legacy prompt whose conversion needs scoping first.
