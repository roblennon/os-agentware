# Humanize: the register-repair method

How to take the machine fingerprints off a piece of writing and put it back in a person's voice. The `cleanup` mode calls this for the register part of its work; it is written generally because the method is the same whether the text is an instruction file or a draft for a reader. The catalog it works from is `../../_shared/references/ai-writing-patterns.md`. Load both.

## What this is for

Many de-AI passes match on vocabulary: swap "delve" for "explore," strip the em-dashes, call it done. That fails, because the tells that actually give a draft away are more than patterns in specific words or punctuation. They are patterns in everything lexical, from word choice to register to sentence and paragraph construction to the use of literary devices. Most of these survive a synonym swap. This method works from the full catalog at composition, sentence, and vocabulary level, and fixes composition first, so the result reads as written by a living person.

The second thing it protects is voice. A generic cleanup produces generically clean prose: competent, characterless, and still pulled toward how the model usually writes. So the pass resolves a specific voice (the broad sense of voice, everything about how this one person writes) and makes the cleaned text feel written by just that individual.

Hold the framing from the catalog: this is an editing resource, not an authorship detector. It catches prose that fails to reach a real reader, whoever wrote it. Findings are never reported to a writer as evidence that a machine wrote their work.

## What the pass may change, and what it may not

It may restructure. Reorder sections, cut a passage, delete a strong sentence that is over-polished, expand a thin point into the specific thing it is standing in for. A pass restricted to swapping words cannot fix the failures that matter most.

It may not impersonate the writer's rhythm. Staccato, line-break cadence, the build-and-pop of a stacked passage: that is the writer's hand. Attempts to reproduce it copy the surface, compress past the point the meaning survives, and produce fragments that parse only for someone who already knows what they meant. If the cadence is itself a machine tell (too even, stacked tricolon, metronomic clause pairs), that is not the writer's hand. Fix it.

The target is not the writer's final draft. It is the version where the writer's own pass is all that is left: everything mechanical handled, the piece's own hand still to be added.

## Inputs

The text, pasted or as a file path. Whose voice the result lands in, when the project keeps voice samples or a style note; with none on file, say so and run voice-neutral rather than inventing a voice. The genre and destination, because they change what counts as a tell; ask if it isn't obvious. And whether the user wants a rewrite or only a diagnosis.

## Run

### 0. Identify the genre and who the piece is supposed to sound like

Before applying anything, name the register and the implied author. The genre carve-outs in the catalog are not a footnote. Direct-response copy may legitimately keep exclamation points and hard closes, academic prose may keep semicolons and announced conclusions, structured business documents may have headings, and instruction files have headings, tables, numbered steps, and frontmatter as the format working. Overdone is still overdone. The genre changes the lens, not the standard.

### 1. Composition pass

Read the whole text first. Local edits made without the global picture produce inconsistent voice and broken argument.

Work the composition tier of the catalog. In practice the recurring moves: cut the over-polished sentence that states the lesson after the story; replace the general noun with the particular thing it stands in for; stage what is merely asserted; loosen an ending that resolves too neatly for its genre; move a rhetorical device to where it pays, or drop it; strip the sentences that comment on the writing rather than advancing it; and check whether the piece has any shape other than a general-purpose answer poured into its format.

Two disciplines while doing this.

**Length has no preferred direction.** Sometimes the repair is deletion. Sometimes it is a rewrite that runs much longer because spelling the specific thing out costs words. Never compress toward a target as a humanizing move; shortening is a separate, deliberate pass. Repairs often skew longer for a reason worth knowing: tightening is its own editing pass that almost nobody but working copywriters runs by reflex, so untightened prose reads like a person who had a thought and wrote it down.

**Consequence is the deep check.** Does anything in the piece behave differently because of what it just said? A point that costs the writer nothing, a difficulty named and then ignored, a risk that no later sentence is wary of. Those survive every surface fix.

### 2. The skeptical-reader audit

Step away from your own edits and read the result cold, as a reader who knows the field, is busy, and is not automatically impressed. One question: did this writer say something to me, or write around the topic?

Then the author-plausibility check: if this came from the person it is supposed to have come from, are these the words they would reach for, and would they frame it this way for a peer?

The audit asks a different question than the composition pass did. That is deliberate. It reads the output on its own terms rather than re-checking your own work.

### 3. Line pass

Now the sentence and vocabulary tiers, gated by confidence.

**Hard tells get fixed on sight.** A word borrowed from a profession the writer isn't in, an invented label where a description would do, wording no one in the claimed author's world would use. One instance is enough.

**Soft signals get fixed only when they cluster.** Nominalizations, tidy contrasts, dense abstract lists, vague nouns, restatement that doesn't progress. Any one is ordinary human writing. Act when several land in the same passage and point the same way: nobody acting, nothing concrete changing, words that belong to no one. Scale the judgment to the piece. In a short passage, two reinforcing signals is a cluster.

**A lone soft signal gets left alone.** This is the rule that keeps the pass from mangling good text.

Take replacement vocabulary from the text itself. If the writer says "stupid simple" in paragraph four, that beats "important" as a replacement for "transformative" anywhere else. Don't import words the writer doesn't use. In an instruction file, ask whose word a flagged term is before proposing its removal: the catalog lists words to question, and the operator's own vocabulary wins.

### 4. Final check

**Re-injection.** A rewrite is itself an act of generation, and it reliably introduces fresh tells: a new tidy closer, a fresh tricolon, cadence rebalanced until it is too even. Replacing a prefab contrast with an aphorism is a different item on the same list. Sweep for what step 3 added, and read your own proposed lines for the exact patterns they were meant to fix.

**Nothing dropped.** List what the input said that the output doesn't. The list should be empty, or every item on it should have a stated reason. Cuts target over-polish and redundancy. If a cut would remove information, it becomes a flag for the writer rather than a cut. In an instruction file this check is the whole game: an instruction that hedges into a suggestion during a register pass has failed at its job.

## What to leave alone

Every instinct in an editing pass points the other way, so this is explicit.

Roughness that is evidence of a person is not an error: missing capitals, a typo, a dropped period, a trailing-off sentence, a word repeated in the heat of a point, a digression that isn't strictly needed. Cleaning those produces prose that is more correct and more obviously machine-touched.

The distinction to hold: what a machine leaves behind (chatbot framing, mechanical hedging, structural announcements) goes. What a person leaves behind stays. When it is unclear which one you are looking at, ask whether the irregularity costs the writer anything. A typo costs a little credibility and buys nothing, which is exactly why a machine wouldn't produce one.

Don't manufacture roughness either. Sprinkling typos on an otherwise perfect piece is a costume. The irregularity that matters is structural, where the writer's attention actually went, and it can't be added afterward.

And if a sentence is fine, leave it. A change has to earn itself. If the meaning and the length would both stay the same, leave the sentence alone. Reading slightly better to you is not a reason. The cost of a same-same revision comes out of the writer's voice, their idiosyncrasies, the texture of what makes them them, and that is often the part worth keeping, even if slightly imperfect.

## Output

For a rewrite: the rewritten piece only. No preamble, no commentary inside it, no change summary. The user pastes it back. Anything that turned into a flag rather than a cut, and any judgment call worth naming (something left because it read as the writer's real voice, a genre rule skipped), goes in the surrounding message, kept short.

For diagnosis: which patterns appear, where, at which confidence level, and for each, what the reader loses. Reader-level failures, never a feature count.

## Sources

Distilled from the Wikipedia *Signs of AI writing* taxonomy, field-tested rewrite practice, blind-sample testing against fresh writers with no context, and before-and-after diffs of a working writer's own hand edits of AI drafts. The composition tier comes almost entirely from the diffs; the sentence tier from the blind samples; the vocabulary tier is the older empirical catalog. Full account in `../../_shared/references/ai-writing-patterns.md`.
