# Rationale Extraction

This is the phase that makes converted skills trustworthy under edge cases. A template tells the agent *what* shape to produce. The rationale tells the agent *why*, which is what it needs when the user asks for a variation and the agent has to decide whether deviating breaks the thing.

Rationale is also the tacit craft hiding in the author's head. Much of what made the original prompts work has never been written down. The conversion is our chance to surface it.

## Goal of this phase

For every chunk tagged as a **craft move** or **judgment heuristic** in classification, produce a one-liner:

*"[move] works because [reason]."*

These one-liners go to `RATIONALE.md`, a file at the skill root that nothing in the skill links to (shape below). They stay short, not a history lesson, just enough that the person maintaining the skill, or the next rewrite pass, can make judgment calls consistent with the author's intent.

One split matters before anything is filed. The model never loads `RATIONALE.md`, so the one sentence of why that a rule needs in order to be applied well stays inline, next to the rule, where principle 2 of the prompting principles puts it. This file is the one place that split is spelled out. The templates and modes point here. What goes to the file is everything else: history, dropped alternatives, what an earlier version did, adaptation notes, and the reasons behind structural choices the model executes without having to weigh.

## Where rationale comes from

Three sources, in order of preference:

1. **Stated in the source.** The original prompt sometimes includes rationale as an aside. Lift it verbatim. Example: *"Return the voiceprint in its own style. Yes, this is very meta, but we've found that the closer a voiceprint is to the style it is trying to emulate, the better."*. The second sentence is rationale. Capture it.
2. **Inferable from structure or context.** Sometimes rationale is implicit in how the prompt organizes steps or which constraints it emphasizes. Infer with care, but flag the inference in the decision log so the user can confirm.
3. **Only in the author's head.** Most important category, and the one that requires explicit elicitation. Ask.

## Eliciting tacit rationale

When the rationale isn't stated, ask the user directly. Don't batch too many at once, three to four questions per round, each focused on one move.

**Good question framing:**

- Specific to the move: "This prompt requires analysis to come before the final output. What does that ordering buy you?"
- Action-oriented: "Under what circumstances would you deviate from this rule?"
- Counterfactual: "If a future version of this skill dropped the 'ratings out of 10' and used 'low/medium/high' instead, what would be lost?"

**Avoid:**

- Vague questions ("Why is this here?"): produces vague rationale.
- Leading questions ("This is because of X, right?"): you'll get agreement even when wrong.
- Asking about every single line: only ask about the moves that genuinely shape the output.

## How much rationale to capture

Target: 3–8 rationale one-liners per skill. Enough to cover the non-obvious moves. Not so much that the file becomes a treatise.

If a skill needs more than 8 rationale notes, either (a) some of them are actually domain knowledge that belongs in a reference, or (b) the skill is doing too much and should be split.

## The RATIONALE.md file

`skills/<skill-name>/RATIONALE.md`, no frontmatter. It opens with a one-line header naming the skill, then one line saying what the file is for and that nothing points to it on purpose, then the notes: paragraphs or bullets, each a move or choice and the reason behind it. Rationale that belongs to one mode or reference sits under a heading naming that file. The scaffold is `../templates/RATIONALE.md.template`.

Nothing in SKILL.md, a mode, or a reference links to the file. It ships with the skill because it lives in the folder, and it never loads on trigger because nothing points at it. Any path written in it has to exist in a shipped copy of the skill; the authoring workspace's decision log and output folders do not ship.

Keep each note to one or two sentences. The goal is enough clarity to act on, not comprehensive documentation. Domain knowledge the model needs at run time belongs in a reference, not here.

Until 2026-10-16 these notes lived in a Design Rationale section inside SKILL.md, and often inside modes and references too, which put them in front of the model on every trigger. A rationale section still sitting inside a loaded file is now a finding for `enhance` and for Hazmat: move it out, and leave inline only the why a rule needs.

## Worked example: rationale notes from a voiceprint-generator prompt

A plausible pass through a voiceprint-style source surfaces a handful of consequential moves and their rationales, some stated, some elicited:

- A meta-instruction telling the model to return the voiceprint in the same style it's describing, *stated in source*, with the rationale already in the next sentence (the closer the rendering is to the style being emulated, the truer the voiceprint reads). Lift both.
- An invitation to add "one or two factors that aren't on the checklist": *not stated*. Ask the author what this buys. A typical answer surfaces *prevents the output from going rote* as the rationale.
- A caution about scoring figurative language too high for everyday writing contexts: *stated in source*, lift.
- An ordering choice (analysis section before the voiceprint itself): *not stated*. Ask why this order. A typical answer is *forces the model to do the linguistic work first so the voiceprint synthesizes rather than guesses*.
- A specific rating scale (out of 10, not low/med/high or out of 5): *not stated*. Ask what the scale buys. A typical answer is *granularity without false precision, and inter-voiceprint comparability*.

Result: five rationale notes, each one line, covering the non-obvious moves.

## What not to capture as rationale

- Mechanics that are obvious once stated ("we output markdown because that's readable"): skip.
- Rationale for scaffolding we're dropping: dropped content doesn't need rationale, it needs a log entry.
- Domain knowledge dressed up as rationale ("we check for active voice because passive voice is weaker"), that's domain knowledge, belongs in the reference, not in `RATIONALE.md`.

## When the user can't articulate the rationale

Sometimes a move worked for reasons the author never explicitly understood. That's fine. Record it as: *"[Move]: empirically produces better output. Specific mechanism unclear. Do not remove without testing."* This is honest documentation and signals future converters to treat the move as essential, don't remove it casually.
