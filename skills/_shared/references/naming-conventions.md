# Naming conventions

Keep skill names short, descriptive, and action-oriented where possible. Most harnesses use the skill name for both triggering and invocation, so the name should read well in both contexts.

## Voice and feel: favor language people actually use

A skill name is something a person says out loud and types into a prompt. Names throughout a project should match how its users would say things, not how a developer would label them.

**Favor:**

- **Conversational over technical:** *"good morning"* over *"daily-briefing-orchestrator,"* *"skillify"* over *"skill-conversion-pipeline,"* *"tracker"* over *"task-management-system"*
- **Evocative over functional:** *"loop"* (suggests cyclic improvement) over *"skill-evolution-engine"*
- **Verbs and short noun phrases people would type:** "good morning," "what's next," "make a skill"
- **Words that sound like something a friend would mention:** *"I just had the showrunner plan my day"* reads natural; *"I just invoked the daily-briefing-orchestrator"* doesn't

**Avoid:**

- AI-product suffixes: *-bot*, *-ai*, *-gpt*, *-engine*, *-pipeline*, *-orchestrator*
- Enterprise-software jargon in user-facing names: *workflow*, *protocol*, *framework* (fine inside reference docs and internal architecture, not in skill names)
- Compound technical phrases: *content-management-orchestrator*, *automated-task-routing-system*
- Implementation detail in the name: *shipped-version-tracker*, *log-rotation-handler*
- Acronyms unless they're already universal: nobody should have to learn a glossary

**Test it:** would the user say this name out loud naturally? *"I need to skillify this prompt"* reads fine. *"I need to invoke skill-conversion-pipeline on this prompt"* doesn't. Names that sound conversational earn trust. Names that sound like they came from a ticket erode it.

This applies to skills, modes, configuration keys, file names users will see, and anything else the user encounters. Internal artifacts (reference docs, technical conventions, plumbing) can use precise or technical language where it serves clarity. Anything user-facing leans natural.

## Skill names

**Good:** `os-skillify`, `os-showrunner`, `os-agentware`

**Bad:** `content_editor_bot`, `editor-v2-final`, `MyEditingPrompt`, `edit` (too generic)

Rules:

- lowercase, hyphen-separated
- a noun phrase or short verb phrase
- no version numbers in the name (versioning lives in frontmatter or a changelog)
- no "-bot", "-ai", "-gpt" suffixes
- not the user's name

**Prefixes.** A set of skills that travels together often carries a short prefix (the skills in this repo use `os-`). It prevents collisions with skills a user already has under the same root name, and it says at a glance where a skill came from. When a project uses a prefix, it is part of the canonical name: the folder, the frontmatter `name:` field, and every cross-reference carry it, and nothing rewrites it at install time. Prefixes are silent when spoken (a voice agent says "skillify," not "os-skillify") and always present in written, file, and frontmatter contexts. A project that has no reason for a prefix doesn't need one.

## Category skills vs. job skills

- **Category skill:** named for the category. `os-skillify` (many modes, one subject).
- **Job skill:** named for the specific job. `os-showrunner` (one role, done well).

Use a category skill name when the skill contains multiple modes. Use a job skill name when the skill does one specific job.

## Mode names

Inside a category skill, modes are named for the specific job they perform.

**Pattern:** `<verb>-<object>` or `<short-name>`

**Examples in an editing skill's `modes/`:** `copy-edit.md`, `developmental.md`, `redundancy-check.md`, `tone-scale.md`, `takeaway-extract.md`

Match the mode name to how the user would ask for it: "do a copy edit" → `copy-edit`; "extract takeaways" → `takeaway-extract`.

## Reference doc names

Descriptive noun phrases, hyphen-separated, `.md` extension. Examples: `copy-editing-checklist.md`, `voiceprint-definition.md`, `content-format-taxonomy.md`.

## Template names

Match the output they produce, suffixed with `.template` or `.md`. Examples: `issue-suggestion-report.md`, `voiceprint-output.md`, `decision-log-entry.template`.

## File structure

Skills live at `<project>/skills/<skill-name>/`, or wherever the harness discovers them (a `.agents/skills/` or `.claude/skills/` folder that links back to the source). The shape inside a skill folder:

```
skills/
├── _shared/
│   └── references/
│       └── <shared-ref>.md
└── <skill-name>/
    ├── SKILL.md
    ├── RATIONALE.md                  # optional, unlinked; why the skill is shaped this way
    ├── references/                   # skill-internal
    │   └── <topic>.md
    ├── modes/                        # category skills only
    │   └── <mode-name>.md
    ├── templates/
    │   └── <output-shape>.md
    ├── examples/
    │   └── <example-name>.md
    └── scripts/ or bin/              # executables the skill ships, optional
```

Absolute deployed paths (`~/.agents/skills/<skill>/...`, `~/.claude/skills/<skill>/...`) don't belong in skill bodies: they break the moment the skill moves. Where a script genuinely needs an absolute path at runtime, the script resolves the active skill directory itself.

## Shared references

When multiple skills need the same reference, it lives at `skills/_shared/references/`. Skills load it by relative path, and the depth depends on where the loading file sits:

- From `skills/<skill-name>/SKILL.md`: `../_shared/references/<file>.md`
- From `skills/<skill-name>/modes/*.md`, `references/*.md`, or `templates/*.md`: `../../_shared/references/<file>.md`
- From one skill to another skill's file: `../<other-skill>/...` from SKILL.md, `../../<other-skill>/...` from a nested file

The two-up form from nested files is a recurring drift surface. The one-up form silently fails because it resolves inside the skill's own folder instead of escaping to `skills/`. Check the depth when writing or editing a cross-reference.

Avoid duplicating reference content across skills. Promote a reference into `_shared/` the moment a second skill needs it for the same reason; the full promotion procedure is in `skill-vs-mode-vs-reference.md`.

## Frontmatter

Every SKILL.md has YAML frontmatter using the block-folded scalar form:

```yaml
---
name: <skill-name>
description: >-
  <trigger language. See frontmatter-format.md for the full rules.>
---
```

The `>-` block-folded scalar lets descriptions contain colons, double quotes, and apostrophes without escaping. Bare strings break on every one of those characters and fail validation. Always use `>-`.

Description length: aim for 400 to 800 characters. The hard cap is 1024. Per-mode breakdowns belong in the SKILL.md body, not the frontmatter.

Standard optional field: `version` (semver, represents what shipped, see `frontmatter-format.md` Rule 4). Other fields may be added for traceability, such as `source-prompts` for a skill converted from legacy prompts.

## Legacy prompt references

When a converted skill descends from one or more legacy prompts, record the source filenames in the decision log, not in the skill itself. This keeps the skill clean while preserving the audit trail.
