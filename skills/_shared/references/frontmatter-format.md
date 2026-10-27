# Frontmatter Format

YAML frontmatter rules for SKILL.md. Get them wrong and the skill fails to install, often with a generic "validation failed" error that doesn't say which rule fired.

## The required shape

Every SKILL.md starts with YAML frontmatter delimited by `---` on its own line above and below:

```yaml
---
name: <skill-name>
description: >-
  <Description text. See rules below.>
---
```

Two required fields: `name` and `description`. Optional fields can be added. The validator only checks the core two.

The recommended optional field for any skill that ships in Personal OS is `version`: see Rule 4 below.

## Rule 1: `name` must equal the directory name

If the skill lives at `skills/os-audience/SKILL.md`, the frontmatter `name` must be exactly `os-audience`: the full folder name, prefix included. The validator surfaces a mismatch as a generic failure with no specifics, so this is easy to overlook. Use lowercase, hyphen-separated, no version suffixes.

## Rule 2: wrap descriptions in a block-folded scalar

Use `description: >-` followed by the text on the next indented line. Like this:

```yaml
description: >-
  Edit existing prose: content writing, articles, blog posts, emails. Routes
  across seven editorial modes: copy-edit, redundancy, active-voice, specificity,
  developmental, what-why-how, takeaway. Triggers on "edit this," "review this
  draft," "tighten this up." Do NOT trigger for drafting new content.
```

The `>-` indicator makes YAML treat the indented content as a single string with newlines folded into spaces and trailing newlines stripped. Inside that block, **none of these characters need escaping**:

- Colons (`:`): used in *"three modes: from-sample, from-book"*
- Double quotes (`"`): used to wrap trigger phrases like `"draft a hook"`
- Apostrophes (`'`): used in contractions like `what's` and possessives
- Em-dashes (`—`), parens, backticks, slashes, all literal

Bare strings (`description: <text>`) break on a colon followed by a space, on a leading quote, and on a `#`, all of which turn up constantly in descriptions. A plain YAML scalar handles apostrophes and em-dashes without complaint. Single-quoted strings (`'...'`) break on internal apostrophes. Double-quoted strings (`"..."`) break on internal double quotes. The block scalar avoids all three traps with a single rule that always applies.

**Use `description: >-` for every SKILL.md, even short ones.** Uniformity prevents future edits from accidentally introducing a colon or quote that breaks the parser.

## Rule 3: descriptions are routing prompts with a shipping budget and a hard limit

The platform limit is 1024 characters. Some upload paths reject anything longer, so no installed description may cross it. Shipped Personal OS descriptions use a lower 900-character budget, leaving at least 124 characters for modes and routing language the user adds later. Release lint enforces the shipping budget. A customized installation may use the full platform allowance.

Descriptions are injected into harness context for routing decisions, so every detail should earn its place. The goal is reliable selection, not minimum length. When a description approaches either limit, report its current length and the characters remaining before 1024 instead of saying only that it is "too long."

Treat the description as a *routing prompt*, not a TL;DR. The model uses it to decide whether to invoke this skill. It does NOT use it to understand what the skill does in detail (that's what SKILL.md body is for, loaded only after invocation).

### What belongs in the description

1. **Job in plain language**: what the skill does, in one sentence
2. **Architectural or method distinctions when they affect selection**: include the placement, method, or inheritance pattern that distinguishes this skill from a plausible alternative. For example, a skill builder's map-before-make or inheritance behavior may be part of why the harness should choose it over a generic skill creator.
3. **Mode names, terse but complete enough to route**: list modes whose jobs widen the parent's trigger surface. Skip parentheticals when names carry meaning. Use short explanations when a mode name alone would not help the harness choose.
4. **Trigger phrases**: quoted user-likely phrasings. Cover all the modes' distinct triggers so the harness can route to the parent.
5. **Negative triggers when adjacent-skill confusion is real**: *"Do NOT trigger for X (use other-skill instead)"*. Skip these when no adjacent skill is genuinely confusable.

### What doesn't belong

Move these to SKILL.md body **when they do not change which skill the harness should choose or reject**:

- **Internal architecture / dependencies that matter only after selection** (e.g., storage adapters or write contracts with no routing consequence)
- **File path references** (*"Read references/X.md for the mental model"*)
- **Operational guardrails** (no-delete, no-overwrite, dry-run discipline, the model doesn't route on these)
- **Philosophy / mental model notes** (the SKILL.md body is where philosophy lives)
- **Deferred-feature notes** (*"X is deferred to v0.2"*, irrelevant to routing)
- **Migration / historical context** (*"Replaces the prior Y skill"*)
- **Implementation details with no routing consequence** (configuration paths, incidental integration mechanics)

The test: *would removing this change which skill the harness picks or rejects?* If yes, keep it. Whether it is a trigger, mode, method, architectural distinction, or negative boundary. If it is only useful after the skill has been selected, move it to the body.

### Length is flexible when the content earns it

Aim for 400-800 characters as authoring guidance, not a quality score. Shipped descriptions may use up to 900 when modes, trigger coverage, method distinctions, or sibling boundaries materially improve routing. User-customized descriptions may use the remaining space through 1024. Trim further when the trigger surface is narrow. Do not shorten a description merely for aesthetic consistency. Broad reductions are routing migrations and should be checked against representative prompts before rollout. **Violate the template any time it isn't serving the routing decision.**

### Mode files

Mode files have their own `description:` (loaded only when the parent skill is invoked, used for intra-skill routing). They follow the same discipline but tighter: no architectural context (parent has that), no cross-skill relationships, just job + sibling-disambiguation + triggers. Aim for 300-600 chars per mode.

When a mode has distinct triggers that aren't on the parent SKILL.md, surface them on the parent. Otherwise the harness can't route to the parent in the first place.

## Rule 4: `version` tracks what shipped, not what's currently running

Every skill that ships in Personal OS carries a `version` field in `SKILL.md` frontmatter, between `name:` and `description:`:

```yaml
---
name: os-email
version: 0.1.0
description: >-
  ...
---
```

Use semver. Initial release for the curated default is `0.1.0`. When a skill genuinely revs (substantial behavior change shipped through os-tune), it bumps independently.

**The semantic: `version` represents the version that shipped, not the user's currently-modified version.** If the user customizes a skill (via `extend`, `refine`, or direct edit), don't bump `version`: the field continues to reflect what was originally shipped. User customization is tracked separately when needed (currently behavior-only via always-diff discipline. Eventually via content comparison if Personal OS ships auto-updates).

Mode files don't carry `version`: only the parent `SKILL.md`. One version per skill. Modes ship together with their skill.

Versioned archive files (`SKILL-v0.1.md`, etc.) are historical records, not active skills. They don't carry `version`.

## Validating before shipping

Before declaring a SKILL.md ready, run its frontmatter through a YAML parser. If Python is handy:

```bash
python3 -c "
import yaml, sys
text = open(sys.argv[1]).read()
fm = text.split('---', 2)[1]
data = yaml.safe_load(fm)
assert data.get('name'), 'missing name'
assert data.get('description'), 'missing description'
assert len(data['description']) <= 1024, f\"description too long: {len(data['description'])} chars\"
print('OK:', data['name'], '-', len(data['description']), 'chars')
" path/to/SKILL.md
```

If it parses and the description fits, it will install.
