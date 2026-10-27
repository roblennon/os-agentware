# Output format tradeoffs: installed skill vs copy-pasteable prompt

The microtool sub-modes produce tools in two output formats. The choice affects portability, integration, and iteration. This reference covers when each format wins and how to decide.

## The two formats

**Installed skill.** Full skill structure at `/skills/<name>/`:

- `SKILL.md` with valid frontmatter (name, description, triggers, negative triggers)
- `modes/<name>.md` for each mode (single mode for microtool, multiple for full skills)
- `references/<name>.md` for shared craft (optional)
- Loads of the project's own material where appropriate (voice samples, briefs, templates)
- Found by the harness's skill discovery, which matches the description against what the user is asking for

**Copy-pasteable code-fenced prompt.** A single markdown code fence containing the 7-section canonical micro-tool anatomy:

- Task / Persona / Constraints / Process / Success Qualities / Output Format / Inputs
- No frontmatter, no skill structure
- Drops directly into any LLM environment: ChatGPT, Claude, Gemini, a Notion doc, a colleague's hands

## When an installed skill wins

An installed skill is the right choice when:

**The tool will be used inside the user's own workspace.** When the user is the primary consumer and they work in that harness day to day, the skill format gives them automatic discovery, iteration through file edits, and composition with the rest of the project's skills.

**The tool loads project material.** When the tool benefits from loading a voice sample (voice-sensitive output), a brief (project-scoped work), or a template (structural shape), the installed format is the way. Copy-pasteable prompts can't load files.

**Iteration is expected.** Skills get refined through use: patches to constraints, additions to the process, adjusted output formats. Editing a skill file is clean and version-controlled. Editing a copy-pasteable prompt in place loses history and tends to drift.

**The tool will compose with other skills.** When the produced tool naturally chains with other skills in the project (drafting, editing, research), the installed format makes the chain easy.

**The tool needs negative triggers.** When the tool risks being invoked in adjacent contexts where another skill is better, frontmatter negative triggers prevent misrouting. Copy-pasteable prompts have no routing layer.

## When copy-pasteable wins

Copy-pasteable code-fenced prompts are the right choice when:

**The tool will be used somewhere else.** A colleague without this setup needs the tool. The user wants to drop it into a plain ChatGPT or Claude session for a one-off job. The tool will be embedded in documentation, a course, a tutorial, a blog post.

**The tool is a one-shot.** Some tools are single-use. The user runs the tool once, gets the output, and never thinks about it again. Building a full skill for that is overhead. A code-fenced prompt is faster to produce and faster to use.

**The tool is being shared with people who don't have your setup.** When the user wants to share a tool with their audience, their team, or the open internet, the portable format lives anywhere a markdown code fence does.

**The tool's voice should stay the source author's.** Copy-pasteable prompts follow the source author's voice rather than the house style. When source content has signature phrasing the tool inherits verbatim, that voice survives in the portable format. Installed skills lean toward house style, but source wording keeps its own voice in a quoted block (see `craft-preservation-from-content.md`). The idiosyncrasies are the thing worth keeping. The quoted-block exemption exists for them.

**The tool is meant to be visible and inspectable.** Copy-pasteable prompts are transparent. The user reads the prompt and understands what it does, where an installed skill keeps some of the structure in frontmatter and reference files. Transparency matters for trust, for teaching others how prompts work, and for auditing what a tool actually does.

## When the choice is genuinely ambiguous

Most of the time both formats would work, and the choice depends on the use case rather than on tool quality. Two rules of thumb help:

**Default to copy-pasteable for a personal one-shot.** When the immediate need is a tool for a job right now, with long-term storage figured out later, copy-pasteable is faster to produce and easier to iterate inline. Saving it as a template afterward, wherever the project keeps templates, is one move.

**Default to an installed skill for anything that lives in the project.** If the tool will be invoked many times, load project material, or compose with other skills, the installed format is the right starting point. The skill structure pays off across uses.

When the user specifies, honor the specification. When they don't, the mode asks once which format they want, with a one-line tradeoff for each. Don't over-explain. Most people decide quickly once given the choice.

## Format conversion after the fact

An installed skill can be exported as a copy-pasteable prompt by collapsing the SKILL.md and mode file into a single 7-section code fence, which is useful when sharing it with someone who doesn't have the skill installed. The reverse works too: a copy-pasteable prompt can be expanded into a full skill by routing it through `from-prompt`.

So the format choice isn't permanent. If the user picks copy-pasteable for an immediate job and later wants the full version, they can convert via `from-prompt`. If they pick the installed format and later want to share, they can collapse it to a code fence.

