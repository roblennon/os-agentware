# Skill update protocol

Shared write discipline for any operation that creates or modifies skill files: SKILL.md, mode files, references, templates. Loaded by every `os-skillify` mode that writes. Mode-specific concerns layer on top.

## Two write modes

Skill-file work splits into two shapes, and the protocol branches where they diverge.

**Modify:** an existing file changes. The original content is the starting state and the proposed change is computed against it. Customization respect applies. Used by `refine` (a tweak folds into an existing skill), `extend` (the parent SKILL.md gets its mode index updated), `enhance` (live skills get consolidated, split, or augmented), and `cleanup` (finished files get repaired).

**Create:** a new file is written where none existed. No prior state, no diff to compute, nothing customized to respect. Used by `extend` (the new mode file itself) and by all the generative modes.

A single operation often involves both. `extend` creates a mode file and modifies SKILL.md to register it. The protocol applies to each file write according to its shape.

## Show before write

Every write is shown before it lands, and the write waits for a clear yes. This is the one piece of the protocol that is a genuine requirement rather than advice, and the reason is simple: a skill file is the thing that writes the next files, and a wrong edit that lands silently propagates before anyone sees it.

**For Modify:** show a diff against the current file, with enough surrounding context that the user can judge intent. Show the whole file only when the diff would be harder to read than the result.

**For Create:** show the full proposed file with its target path. Frontmatter, body, structure, all visible before the write.

**For multi-file operations** (a new mode plus its parent's index update, or a generated skill with several modes and references): show the whole batch and confirm once for the batch. If one file in the batch fails its sanity check after writing, revert the batch where the file system permits, or surface the failure plainly so the user can fix and rerun.

The user's options after seeing a proposal: accept, accept with edits, reject, or set it aside for later. Trivial changes (a typo, a line added to a list) can be batched into one confirmation when the user has said that is fine for them. Moderate and large changes ask per item.

## Customization respect

For Modify operations, the discipline is always diff, never silent overwrite. Even when something automatic initiates the change (an upstream update to a skill the user has since customized), the user sees the diff and confirms before the file changes.

When a skill carries a `version` field (see `frontmatter-format.md`, Rule 4), that field is the comparison anchor: a file whose content differs from what shipped at its version has been customized, and a proposed update gets a heads-up to that effect before the diff. The show-before-write step still covers the actual change. The detection just adds the warning.

Create operations have nothing to respect, so this section does not apply to them.

## Sanity checks

After every write, run the checks that catch breakage before the user moves on:

- **Frontmatter parses.** YAML validates, `name` and `description` are present, `name` matches the directory name, and the description is at most 1024 characters. These are the rules in `frontmatter-format.md`, and getting one wrong means the skill fails to install.
- **Markdown structure is intact.** Headers nest sensibly, no truncated code fences, no orphan list items.
- **Cross-references resolve.** Every relative path mentioned in the file points at something on disk, including `../references/<name>.md` and `../../_shared/references/<name>.md` forms.
- **No broken sibling references.** A file that names a sibling skill or mode names one that still exists.

If a check fails, say so immediately rather than leaving broken state in place. A small failure (a typo in a path, a missing field) gets a proposed fix, a confirmation, and a rerun of the checks. A structural failure gets the write reverted where possible, or the bad state surfaced so the user can correct it before anything else is written.

For multi-file batches, run the checks per file after each write and halt the batch on the first failure. Writing more files on top of a broken one compounds the repair.

## Reference from consumer modes

Modes that write skill files point at this protocol rather than restating it. One line in the mode's operating principles is enough: writes follow `../../_shared/references/skill-update-protocol.md`, plus whatever concern is specific to that mode. The protocol covers how to write safely. The mode covers what it produces.

## See also

- `frontmatter-format.md`: the frontmatter rules the sanity checks enforce, and the `version` field convention
- `skill-vs-mode-vs-reference.md`: the destination decision tree for what gets created
- `scaffolding-patterns.md`: the three-question scaffolding assessment used during classification
