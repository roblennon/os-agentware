# Mode: from-content

Part of `os-skillify`. Selected when the input is a body of knowledge (an article, a transcript, a book chapter, lecture notes, a talk) that covers a domain with several jobs in it, and the user wants an installed skill that operationalizes it. One tight job from the same content goes to `microtool-from-content`; a working prompt goes to `from-prompt`; a need with no content goes to `microtool-from-job`.

## Job

Design a full skill from content: `SKILL.md`, one or more modes, references where they earn their place. The mode count flows from what the content actually contains. The skill mirrors the source's frameworks, terminology, and step counts, and lifts the phrases that would lose force if paraphrased.

## Before the phases

The parent skill's read-the-room step has run. Load `../../_shared/references/skill-prompting-principles.md` before writing any produced file. It matters acutely here: the source is usually prose written for people, so the produced skill should be written that way too, and not get flattened into bullets and sample phrasings on the way through.

Load `../../_shared/references/self-extending-skills.md` and decide additive or complete. Content-derived skills lean additive more often than not, because long-form content usually encodes a domain where the user's needs keep producing new shapes, but decide per skill.

When the content arrives as anything but clean text (a PDF, HTML, scanned pages) and will be kept as a reference, convert it to clean Markdown first, stripping page numbers, running headers, and interleaved blank lines in the same pass. Citations captured against a raw extraction break when the kept copy is later cleaned.

## Inputs

The content, typically a thousand to fifty thousand words. Optionally: who the skill is for (the user, their clients, the public), which calibrates tone and assumed context; how wide to go (just the core moves, or every angle the content covers); related skills in the project the new one should compose with; and a voice sample when the content is in the user's own voice and the skill should keep it.

## The six phases

### Phase 1: Read

Read the content fully and identify what carries its authority: named frameworks, signature terminology, exact step counts, verbatim phrases that drive a concept home, promised outcomes, worked examples. `../references/craft-preservation-from-content.md` says how to find each and what to do with it.

Show this analysis to the user briefly before designing. It confirms you read the content the way they did, and lets them catch a missed signal while it is still cheap.

### Phase 2: Classify

Single mode or multi-mode? Single when the content captures one tight job with a clear input-to-output transformation. Multi when it covers a domain with distinct jobs, each with its own input and output. Most multi-mode skills land at three to five modes; a count outside that range wants a specific reason.

References are worth creating when a craft pattern is shared across modes, when a canonical structure is used by several modes, or when a framework needs more depth than a mode file should carry. Otherwise fold the material into the modes.

Where does the skill sit in the project? Standalone, or a mode added to a category skill that already exists? When in doubt, prefer adding a mode to an existing skill over adding a skill. Say which you recommend.

Show the classification (single or multi, the mode list, the references, standalone or fold-in) and get a yes before drafting.

### Phase 3: Design

For each approved mode: frontmatter or an opening sentence with triggers and where to route instead; inputs; the run procedure, with the source's own phrasing lifted where it sharpens; constraints, mirroring the source's step counts and framework structure; the output shape; where the user usually goes next; and a note on what is preserved from the source versus what is new design.

For each reference, the canonical content the modes consume.

### Phase 4: Build

Writes follow `../../_shared/references/skill-update-protocol.md`: show the batch, confirm, write, sanity-check each file. Take a restore point first if the project keeps them.

Check each file against the house style the parent skill loaded: punctuation, whether a list is the right shape, the frontmatter rules. Check that every path mentioned resolves. If the source uses three pillars, the mode uses three pillars.

### Phase 5: Verify

Show the produced skill. Common adjustments: mode boundaries (split, merge, rename), constraints tightened or loosened, output format, more verbatim or less, which existing skills it composes with. Iterate until it feels right. Do this before logging; logged work the user then revises creates documentation drift.

### Phase 6: Log

A decision-log entry wherever the project keeps them (`../templates/decision-log-entry.template`): what was built and where, why the mode shape, what is preserved from the source, what is new, open questions for the next version.

## Output

A complete skill folder: `SKILL.md`, `modes/`, and `references/` when warranted, plus the log entry.

## Constraints

Even thin content produces at least one mode. If no mode emerges, the content wanted `microtool-from-content` or `microtool-from-job`.

Mode count tracks what is present. Two distinct jobs means two modes, not a padded five.

Stay inside the source. Working out what it implies is fine. Adding a framework it doesn't have is not.

Loading project material (voice samples, briefs) is opt-in per mode, where it helps, not bolted onto every mode by reflex.

## After this mode

Battle-test the new skill on a real input and fold adjustments in through `refine`. If classification surfaced a fold-in candidate, `extend` the existing skill instead. If the content has more useful moves than the skill captured, `microtool-from-content` can pick them off one at a time. Then `cleanup`.
