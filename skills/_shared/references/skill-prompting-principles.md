# Skill prompting principles: how to write instructions a frontier model actually follows well

Modern models are competent skill-writers by default. They're also overfitted to certain patterns: bulleted everything, copy-pasteable example phrasings, rule-heavy specificity. Those patterns work fine for code, analytics, and structured data, and badly for prose, judgment, and craft. This reference exists so that every skill made or modified with it in hand avoids those traps.

The principles below are roughly in the order they matter when you're writing or editing a skill.

**This list grows.** New traps get named as they turn up, so actually load this file rather than working from memory. When you reference it elsewhere, point at it rather than restating what's in it (principle 6).

## 1. Let the shape of the instructions mirror the intended output

**"Shape" here means more than just format or layout or register.** Every attribute of the writing: style, register, voice, tone, word choice, complexity. And everything downstream of those, like sentence length, rhythm, how much it hedges, how certain it sounds, how it handles an example, idiosyncrasies, punctuation, AI tics and giveaways. All of it transfers from the instructions into the output. When the rest of this file says shape, read that whole set, and read style, register, voice, tone, word choice, and complexity as the ones doing most of the work.

Everything about how a prompt is written influences the output. By prompt I mean anything in your input: instructions and context are all part of it. A skill written as a wall of bullets teaches the model to produce bullets. A skill written in prose with a recognizable cadence teaches the model to produce prose with that cadence. The shape leaks.

This is fine, desirable even, when the output really is structured: code, schemas, analytics summaries, tables, anything where the consumer is another machine or a developer scanning for fields. Lists belong there. That is what the output actually looks like.

But for skills whose output is for human consumption (writing of any kind, content, fiction, articles, marketing, business strategy, conversational replies, anything where voice and flow matter), bias the skill itself toward prose. Use the patterns, sentence rhythms, and tonal range you want the output to have. If the skill is supposed to produce warm, paced writing, the skill should read as warm, paced writing. If the skill is supposed to produce sharp, opinionated writing, the skill should read as sharp, opinionated writing. The model will pick this up whether you mean it to or not, so compose skills and context intentionally.

When in doubt, read the skill aloud and ask whether it sounds like the thing it's supposed to produce.

**Before:** A copy-editing skill written as fifteen nested bullets describing what to check. **After:** The same skill written as three short paragraphs that *demonstrate* the kind of attentive, judgment-led editing the skill is supposed to produce.

### House style

**Punctuation.** Em-dashes and semicolons both read as machine-polished when they accumulate, and both usually have a plainer replacement: a period, a colon, parentheses, a comma. Neither is banned. Use one where it is genuinely the right mark. What to avoid is reaching for them by reflex, which is what produces three em-dashes in a paragraph and a semicolon joining two sentences that wanted to be two sentences. One exception worth knowing: a semicolon separating list items that already contain commas is doing a job nothing else does.

**Bullets are principle 1 in practice.** A list is right when the content is a list, meaning parallel items someone will scan. If the order matters, the list should be numbered. Prose chopped into fragments is not a list, and a skill written as a wall of bullets teaches the model to produce bullets. Restraint here is about the shape of the output, not tidiness.

**Let lines wrap.** Write a paragraph as one line and let the editor wrap it. Hard-wrapping prose at a fixed column makes a file read like code, and it makes every later edit produce a reflow diff that buries the real change. Line breaks belong where they mean something: between paragraphs, in a list, inside a fenced block, in frontmatter.

None of this applies to copy-pasteable prompts, which follow the source author's voice instead. That is the point of the portable format.

### Sub-principle: keep your commentary out of anything the user will paste

Some outputs are meant to be used in one piece. A rewritten draft. A shortened paragraph. A positioning statement copied into a strategy doc, a scored verdict pasted into a review thread, a hook dropped into the opening of an article. The user selects the whole thing and moves it somewhere else.

For those, anything you want to say *about* the output belongs in the message around it, never inside it. Suggestions about what to run next, notes on what you changed, pointers to another mode: all of it gets pasted along with the output and lands in the user's draft.

A mode that says "no preamble" and then ends with a postamble has fixed half the problem. The test is simple. If the user copies everything below your first line, is what they paste clean? If not, move the commentary out.

Those pointers are still worth giving. They just belong in a separate message after the output, or in the reply text around it. Or the output needs to be wrapped as a plain text code block or a linked file.

This covers more than text. It applies to anything the user may copy, save, or reuse as a single unit, whatever shape it takes.

## 2. Capture the why behind the why, not the rule

Models follow instructions almost too well. When a skill spells out a specific rule, the model can latch onto the rule and miss the lens behind it, applying it past its useful range, or failing to adapt when the situation is adjacent but not identical.

The fix is to write principles, not rules, wherever the underlying craft can be expressed as a mental model. State the *why*. Name what the move is protecting, what goes wrong without it, what the operator was trying to preserve. A model holding the principle can handle the edge cases the rule didn't anticipate. A model holding only the rule cannot.

Hard-and-fast rules still have their place: frontmatter syntax, file paths, validator constraints, anything where there's literally one right answer and the cost of getting it wrong is breakage. Use rules there. But when the move is a craft move (a sequence, a phrasing pattern, a rule of thumb), prefer the principle. The user's preference for a certain shape almost always has a *why* underneath it that's more durable than the surface preference. Capture that.

**Before:** "Always start the intake with three questions about goals, audience, and constraints." **After:** "Open by asking about whatever you'll need in order to decide well later: usually what the user is trying to accomplish, who it's for, and what they can't change. Skip questions whose answers are already obvious from context."

The first version gets executed verbatim every time. The second version teaches the model to ask the right question for the situation in front of it.

## 3. Use placeholder-based examples, not verbatim sample text

Whatever you write as a literal example (a greeting, a hook, a question, a section heading, a stock phrase) has a strong chance of being reproduced verbatim, no matter how clearly you frame it as "just an example." This is the mistake that most often slips through unnoticed. The user reads the instruction as "here's the *kind* of thing." The model reads it as "here's the thing."

The fix is to describe the *intent* of the example rather than supplying the text. Use a placeholder that names what the slot is supposed to do, what effect it's supposed to have and what role it plays, instead of filling it with a string the model can grab.

This applies in two places: instructions that tell the model what to say (greetings, prompts, opening lines, transitions, signoffs) and instructions that describe the shape of an output field (hook, headline, takeaway, summary). In both cases, the verbatim version is the trap.

**Before (instructions for what to say):** Open with a greeting like "What's been on your mind today?" **After:** Open with an easy-to-answer question about what they've been thinking about, working on, figuring out, or preoccupied with.

**Before (field description in an output spec):** `Hook: <how the post would open, the angle that grabs attention>` **After:** `Hook: <a statement that creates a dopamine spike for the reader: curiosity, pattern-break, or stakes>`

The "before" version describes the field by name. The "after" version describes the effect the field is supposed to have. The effect-description survives the model's instinct to reach for the nearest concrete phrasing.

When a verbatim example genuinely *is* the right teaching tool, because the move is so specific or so subtle that no description captures it, keep it, and surround it with explicit framing about why this exact phrasing is the craft itself and shouldn't be copied. That framing is the difference between a sample and a script.

One pattern leaks more than any other: blockquoted italic example-answers inside instruction text. The pattern `> *"sample answer phrasing"*` (often appearing under instructions to "think about questions like" or "the kind of answer you're looking for") combines two strong reproduction signals. The blockquote visually presents as an example, and the italic phrasing reads as direct quotation. The model treats both as text-to-reproduce, not pattern-to-emulate. When the underlying intent is to teach the *kind* of answer or the *role* of an answer in a sequence, the placeholder should describe that role explicitly ("a softer reframing answer in the writer's voice, specific enough to anchor a follow-up but informal enough to lower the stakes") rather than supply sample phrasing the model will copy.

## 4. Write for a smart human in plain language

Skills are read by two audiences at once: the model that executes them and the person who installs, audits, or adapts them. Writing that only the model can comfortably parse (compressed jargon, insider shorthand, abstraction stacked on abstraction) fails the second audience silently. The person stops reading, and a skill nobody reads is a skill nobody trusts, fixes, or extends.

So explain complex ideas simply where a simple explanation exists. Prefer the concrete word to the abstract one, the short sentence to the clause-chain, the example to the definition. When a piece of jargon is genuinely doing work (a term of art from the source, a specific term used by professionals commonly despite being jargon where no other word describes the idea properly, or a framework users already know by name), keep it, and define it once in plain words the first time it appears.

The test: could a smart person outside the domain read the skill top to bottom and say what it does and why? If a paragraph needs the author present to explain it, the paragraph isn't finished.

This isn't dumbing down, and it isn't a ban on precision. Plain writing travels: across harnesses, across users, and across the gap between whoever wrote the skill and whoever debugs it a year later.

## 5. Calibrate the force of a rule to how often the exception is right

Absolute words (never, always, every, only, none, must) steer a model much harder than their literal meaning suggests, and they cost nothing to type. That combination makes them the easiest thing in a skill to overspend.

Spend them where there's genuinely no circumstance under which the exception would serve the process: irreversible actions, safety floors, syntax that breaks if it varies, the things that have to hold when nobody's watching. Everywhere else an absolute costs twice. It suppresses a legitimate move the author never thought to allow, and it devalues the real absolutes elsewhere in the file, which start reading as merely emphatic.

The sharper version of the trap is an absolute bolted onto a condition. Checking a condition takes effort. Obeying an absolute takes none. So a rule shaped like *never do X when Y might be true* collapses in practice into *never do X*. The model routes around the whole category rather than evaluating whether Y actually holds. When the checking is the point, the checking has to be the instruction, not a caveat hanging off one.

For everything that isn't absolute, reach for the word that matches the real frequency. Most of the time. Generally avoid. Rarely. Usually prefer. Unless the circumstances warrant it. A calibrated word carries two pieces of information, what to do and how much room there is. An absolute deletes the second one.

The noun carries force too. "Gate", "requirement", "always" and "never", and many other phrases promise something non-negotiable, and they read that way even when the sentence around them allows an exception. Guideline, tendency, and rule of thumb promise something to weigh. "Generally favor" or "Consider" may feel weak or they may be just right. Not everything is "load bearing". Pick the noun that matches what you're trying to convey, the same way you pick the verb. And check the noun is accurate: a step called a gate will stop the user from getting what they want. Always question whether something is actually required 100% of the time.

**Before:** "Never require a prerequisite the user might not have." **After:** "Prerequisites get a quick check, not a preemptive dodge. Look and see whether it's already there, or ask in one sentence. What you're steering around is the twenty-minute side-quest, not the prerequisite itself."

The first version reads as *avoid prerequisites*, so the model quietly downgrades the work rather than asking a one-line question. The second names what's actually being protected, which lets the model tell a cheap check apart from an expensive detour.

## 6. Point at a list, don't restate it

A file that links a reference and also names its contents has made a promise to update itself every time that reference changes. The promise gets broken, quietly, because nothing fails when it does. The enumeration just becomes wrong while still reading as authoritative. That's the damage: a consumer that enumerates reads as *complete*, so whoever loads it trusts the inline list over the canonical file sitting one link away.

The test is one question: **can this list grow?**

Describing a file is not restating it. Because loading a reference is a choice the model makes, a pointer has to carry enough for that choice to be a good one: what the file covers, and when it matters. "Apply its principles" gives no reason to spend the read. "The principles every produced skill follows, including the house style" gives one. Borrowing a phrase or a representative example to make that concrete is fine and often necessary.

What goes stale is a pointer that reads as complete: a count, a full enumeration, a summary that stands in for the file. The test is whether a reader who stopped at your pointer would think they had the whole thing. If yes, cut back to a description. If no, you are describing, not restating.

If the list can grow, point and stop. Name the reference, say what it's for, and let the file be the list: *"the principles every produced skill follows"*, not *"the three principles (a, b, c)"*. When the enumeration carries routing weight the reader genuinely needs on the spot, keep it and add a short note saying which file is canonical, so a future reader knows what wins when the two disagree.

If it can't, as with a framework from a published book, a fixed rubric, or a closed set the design deliberately pins, leave it inline. The names carry the meaning there, and stripping them to satisfy a rule costs information and buys nothing. Most enumerations in a mature pack are this kind. The sweep is for the ones that aren't.

The other half of this lives at the source. **A list that's designed to grow says so in its own file**, near the top, where anyone about to copy it will see. That way the warning travels with the thing being copied instead of depending on every consumer independently knowing better.

**Before:** "Load `skill-prompting-principles.md` and apply its three principles (shape mirrors output, principle over rule, intent over verbatim)." **After:** "Load `skill-prompting-principles.md` before writing any skill file. It covers how instructions should be shaped, how examples should be written, and the house style. It is the current list, so don't work from memory."

The "before" went stale twice in one day: once when a fourth principle was added, once when a fifth was. The "after" cannot.

## Notes

**Frontmatter is not style.** It follows `frontmatter-format.md` and it is a hard requirement: get it wrong and the skill fails to install, with an error that doesn't tell you which rule fired.

## Used by

- `os-skillify`: every generative mode loads this before writing a file, `extend` and `refine` load it before editing one, and `cleanup` checks finished files against it.
- `os-agentware`: loads it before writing any rule, SOP, or principle into a system.

## What you might change and what to generally leave alone

Canonical: the principles themselves and their ordering. Each names a different way a skill goes wrong, and ignoring several at once compounds the damage.

Adaptable: how strictly each principle applies in a given skill. A purely structural routing skill with no prose output and no judgment calls may legitimately be all bullets, all rules, and no examples. That is what its output actually looks like. The principles aren't a style rule. They're a way to match how a skill is written to what it produces. A skill that diverges from one or more principles should note the reason in its `RATIONALE.md`, the unlinked file at the skill root that os-skillify's rationale-extraction reference describes.

## Source

Surfaced as a workspace principle on 2026-05-24 after the operator noticed that earlier skill-generation runs over-applied list-heavy and rule-heavy patterns to writing-domain skills. Promoted to a shared reference because it applies to every skill-authoring or skill-editing operation.

The fourth principle (plain language for the human reader) was added 2026-08-01 after the operator flagged that skill prose was drifting toward high-level compression that reads well to a model and poorly to a person.

The fifth principle (calibrated force) was added 2026-08-02 after a register pass on a setup skill produced the rule "never require a prerequisite they might not have." The operator flagged that an absolute attached to a soft condition collapses into an absolute on the category. The model would dodge prerequisites wholesale rather than spend a sentence checking. Noted as a recurring authoring trap, not a one-off.

The sixth principle (point, don't restate) was added 2026-08-02, immediately after the fifth exposed the cost: thirteen consumer files across nine skills had enumerated this reference's contents inline, so a principle added the day before had been invisible to every one of them. The fix at each site was to point. The fix to the class is this principle plus the grow-warning at the top of this file.
