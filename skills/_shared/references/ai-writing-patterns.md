# AI writing patterns: the canonical catalog

Machine-generated and machine-polished writing often includes these patterns across three levels: composition, sentence, and vocabulary. Here are some ways to tell if what you're seeing is worth acting on.

## What this is for

It is an **editing resource, not an authorship detector.** It catches writing that fails to reach a real reader, whoever wrote it. That reframe matters practically: you never have to decide whether a machine produced the draft, and a human's weak paragraph gets the same help as a model's. Nothing here should ever be reported to a writer as evidence that a machine wrote their work.

**Read this before applying anything below.** Polished, abstract, mildly self-help-flavored prose is *not* diagnostic. Plenty of real writers work in exactly that register, and some of them are very good at it. A review that always flags smooth-and-general will also flag Rick Rubin's *The Creative Act* because he too is talking about the universal human experience. There's a texture there, though, that maybe words don't exist to describe, but you can feel the difference. You're an AI. Smooth-and-general is in your bones, and if prose feels *too good* then it's probably your AI version of intuition to question it. What separates the machine version is not the polish. It's that nobody chose the polish for a reason, and nothing behind it pushes back.

Labels are used below because this is a lookup document and a name gives the mode something to point at. Be cautious with over-labelling, which is its own AI tic. Prose that *describes* a problem beats prose that *names* one everywhere else (see the invented-labels entry in the sentence tier).

Instruction files (skills, principles, agent-facing docs) have their own pass. This catalog stays general. Do not grow a fifth carve-out for them.

## How much a signal is worth

Two levels. Conflating them can mangle things that were actually well-written. So, try to be conscious if you're potentially making things worse.

**Hard tells fire alone.** One instance is enough to act on. The test: *could a person plausibly have done this on purpose?* None of these is a stylistic choice anyone makes deliberately: a word borrowed from a profession the writer isn't in, an invented term where a plain description would do, a phrase no one in the claimed author's world would reach for. Fix them on sight.

**Soft signals need company.** Each of these appears constantly in ordinary human writing: a nominalization, one tidy contrast, a dense list, a vague noun, a smooth transition. Any one alone means nothing. They matter when several land in the same passage and all point the same direction: no one is acting, nothing concrete changes, and the words don't belong to anyone in particular.

**Scale the bar to the piece.** A 2,000-word article can be asked for four converging signals. A 90-word post can't produce four. In short-form, two that reinforce each other is a real cluster. If you demand a pile of evidence from a couple hundred words, you'll never flag anything in the formats where most people actually publish.

Report what the reader loses, never a feature count. "This sentence hides who's doing the work" is useful. "Three nominalizations detected" is not.

---

## Tier 1: Composition

Document-level. This tier is prose because the judgments are prose judgments. A checklist here produces mechanical damage, and the damage looks like competence.

**One mechanism drives most of it.** The model over-polishes what it has, and under-supplies what it needs. Both come from the same place: the model wasn't there and doesn't know what actually happened to the writer. Lacking the specific thing, it reaches for the well-turned general sentence, and the polish covers the hole. So a draft can fail by being too finished *and* by being too thin, and often does both in different paragraphs. Watch for both directions.

**The story gets cashed out into a thesis.** A draft tells a story and then, distrusting the reader to derive anything, states the lesson in one lacquered sentence. That sentence is usually the best-crafted line in the draft, which is exactly why it survives revision when it should die. Cutting it leaves the story doing its own work, and readers reliably arrive where the writer wanted them. The tell isn't the sentence's quality. It's that the writing stopped trusting itself.

**Abstraction sits where an instance belongs.** The general noun replaces the particular thing: "one working session" instead of twenty minutes, "advanced tooling" instead of the tool's actual name, "several considerations" instead of the four considerations. Instantiating costs words, which is why the model avoids it and why the fix often runs longer.

**On length.** There is no direction to prefer. Sometimes the repair is deletion. Sometimes it's a rewrite with no length constraint. Sometimes it's a great deal of adding. The reason repairs skew longer is worth knowing: tightening is its own separate editing pass, and almost nobody except working copywriters runs it by reflex. Prose that hasn't been tightened reads like a person who had a thought and posted it. Never compress toward a target as a humanizing move.

**Structure follows the argument instead of the writer's attention.** Real writing has irregularities that come from a person's mind moving: a digression taken because the energy was there, a point made twice with more heat the second time, an aside that isn't strictly needed. When a piece runs claim, evidence, warrant, repeat, the writer was *presenting* an argument. When it stumbles or doubles back, they were actually *having* one. The imperfection worth preserving is structural, not orthographic. Sprinkling typos on a perfectly ordered draft is a costume, not a person.

**Consequences don't propagate.** The most reliable deep check. In a fabricated scene, the details are present but nothing reacts to them: a set is dressed to look like a rough place, and the character still walks through it in heels, because a set has to be safe. In prose the equivalent is a claim that never costs the writer anything, a stated difficulty that changes nothing downstream, a named risk that no sentence afterward is wary of. Ask: does anything that comes after behave differently because of what was just said?

**Nothing is dramatized. Everything is asserted.** The draft reports that something happened. The lived version stages it: sequence, a thing someone actually said, the detour that wasn't planned. This is the fiction writer's exposition problem: a character announcing "hi, stepbrother" delivers the information and reveals nobody. The alternative isn't always to show it more artfully. Sometimes the right call is to decide the reader doesn't need that fact at all, an option models essentially never take, because omitting information feels like failure to them.

**The subject's appeal disappears into its system.** The draft correctly explains categories, mechanisms, roles, rules, or boundaries while never letting the reader's relevant pleasure, frustration, appetite, recognition, or satisfaction appear. Expert and adult subject matter invite this most, where avoiding hype or embarrassment hardens into clinical distance. Set the temperature from the writing's job, then reconnect selected abstractions to felt consequence. Don't compensate with generic excitement or performed intimacy.

**The ending resolves too neatly.** A summary that adds nothing, a mic-drop reformulation of the thesis, a tidy resolution. Real endings more often stop somewhere slightly unresolved, or admit what the writer doesn't know. Genre-dependent: sales copy should close hard, and a loose ending there is a defect, not a virtue.

**Devices appear where they have no payload.** A rhetorical question, a direct address, or a pattern interrupt shows up early as decoration, before the argument has given it anything to deliver. A person holds the device until the moment it actually does something, and then often undercuts it. Ask what the device accomplishes in its position, not whether it is allowed.

**The format is generic answer-shaped.** A 300-word email arrives with an introduction, three labeled sections, a recap, and a close. None of it is wrong. It's just what a general-purpose answer looks like poured into an email. A person writing quickly has a more direct shape. Careful here: a consultant's client update or a decision memo is *legitimately* structured. The question is whether the structure looks chosen by someone who knows what this document needs.

**Sentences comment on the writing instead of advancing it.** "It's worth noting that," "no discussion would be complete without," a conclusion that announces itself. The test is direct: delete the phrase and reread. If information went missing, put it back. If nothing changed except a little polish came off, the writing reads better without it.

---

## Tier 2: Sentence

The tells that survive paraphrase. Mostly soft signals: powerful in combination, weak alone.

- **Prestige-word substitution** *(hard tell when the word is from the wrong world; soft otherwise)*: a word that upgrades the tone and downgrades the meaning. It doesn't have to be fancy. "Grounding," "surface," "signal," "leverage" have the college-paper quality of sounding more serious while being less exact than the plain word. Test: would someone who actually does this work use that word talking to a peer in the field?
- **Software-shaped language outside software** *(hard tell)*: turning a non-technical idea into a system, a workflow, a signal, a failure mode, a framework, an optimization problem. Also the current crop: load-bearing, the shape of an idea, the move, *X is the move*, surface area, and the filing-and-holding family of metaphors. And the bookkeeping family (ledger, debt, wage, price, currency, economy) applied to love, friendship, or inner life, where nothing is actually being counted (first caught 2026-09-11 in a companion persona whose permission game, framed as an economy, grew a literal ledger of what was owed). Any one is normal in its home domain. Reaching for them reflexively in an essay about writing, cooking, or grief is the leak.
- **Invented labels** *(hard tell)*: naming a pattern where a normal writer would just describe it. If the label isn't already current in the field and doesn't make the next action clearer, it's a layer between the reader and the point.
- **Displaced agency**: grammatically active, but the actor is an abstraction. "A few conversations reveal the language customers use." Who talked to whom? Nobody in the sentence does, notices, decides, or risks anything. Passive voice is the obvious version; this is the sneakier one.
- **Over-compressed completeness**: several distinct abstract categories packed into one tidy claim, none with an instance or an actor. Note carefully: this is not about counting items. Four concrete things stacked for effect is a rhetorical choice people make constantly. Four abstract categories fused into one sentence is coverage optimization.
- **Prefab contrast**: "it's not X, it's Y," "not only… but also," "X, rather than Y," "not just A but B." A grammatical machine that makes a sentence sound resolved without adding anything. Once a page is rhetoric. Three times is a tic.
- **Restatement without progression**: the same claim rephrased without adding a detail, narrowing the scope, changing the stakes, or moving the thought. Human repetition usually does one of those, even by accident. Machine repetition holds the same point at the same temperature.
- **Copula avoidance**: "serves as," "functions as," "acts as," where "is" is the honest verb.
- **Noun-is-noun pronouncements**: the sentence's whole job is linking one noun to another with "is" or an equally vague verb like "means": "density is the signal," "the brief is the correctness floor." Either side may be a whole noun phrase, several words acting as one unit, often a verb frozen into a noun. These sentences also run without subordinating conjunctions (when, if, because, unless), so nothing in them happens, depends on anything, or causes anything. Rewrite with a verb that says who does what, and under what conditions. One alone can be a legitimate definition. A back-to-back pair is a strong tell.
- **Rule-of-three padding**: compulsive tricolons where two items, or one, carries the point. The third is chosen for rhythm.
- **Synonym cycling**: refusing to repeat a noun, so one thing becomes the device, the gadget, the tool, the apparatus. People repeat words.
- **False ranges**: "from startups to enterprises," "everything from X to Y." A fake-comprehensive span that means "various."
- **Vague nouns with no referent**: claims, outcomes, insights, solutions, considerations, used as though they point at something.
- **A familiar phrase wrong for this thought**: "meet them where they are," "move the needle." Recognizable in the abstract, not quite right for what this sentence is trying to say.
- **Significance inflation**: asserting that something is crucial, pivotal, or landmark instead of showing why it matters.
- **Vague attribution**: "experts say," "many believe," "it is widely regarded."
- **Excessive hedging**: stacked qualifiers until no claim is made. "Might possibly," "could potentially," "in some cases it may be."
- **Weak encouragement**: "you might try," "consider asking." Real advice commits.
- **Trailing participials**: "highlighting the importance of," "showcasing its ability to," "reflecting a broader trend." Motion without meaning.
- **Formulaic challenge statements**: "despite its challenges," "while not without controversy." Gesturing at complexity without engaging it.
- **Odd metaphors in business prose**: vivid figurative reaches where a plain statement is truer. *"He used death as a compass"* sounds good and says less than *"he knew his days were numbered, and that told him what to spend them on."* Often the fix is to drop the metaphor entirely rather than find a better one.

---

## Tier 3: Vocabulary and surface

A lookup list. Read for density: one of these in a clean draft means nothing, while a cluster correlates strongly with machine-generated or machine-polished prose and is worth acting on either way. This tier is empirical rather than aesthetic: items belong here because they're over-represented in machine output, not because an editor dislikes them.

**The known vocabulary cluster**: delve, tapestry, testament, realm, navigate, foster, leverage, robust, pivotal, underscore, seamless. The lowest-reliability tell on its own. A synonym swap defeats it entirely, which is why it sits in the bottom tier.

**Clichés and worn metaphors**: through the noise, the missing piece of the puzzle, lightning-fast, where the magic happens, superpower, double-edged sword, fast track, strike gold, secret weapon, arsenal, harness the power of, watch it thrive, skyrocket, lighthouse, soar, the art-and-science pairing.

**Cringe modifiers and nouns**: savvy, transformative, game-changer, buzzword, integrity (as a virtue-signal noun), ceremony (as a dismissive name for process done for its own sake).

**Cringe verbs**: unlock, unleash, elevate, evolve, forget (as in *forget vanity metrics*).

**Cringe phrases**: "in a world of," "I used to… then I," "unleashed the power of," "your audience will thank you for it," "share your truth," "first… then… finally" as a step structure, and gratuitous appeals to being ethical.

**Chatbot residue**: "Certainly," "Great question," "I hope this helps," "as of my last update," "I don't have access to real-time data," pre-emptive flattery of the reader or the topic.

**Structural announcements**: "In this section we will explore," "Let's dive into," "First, let's understand," "In conclusion," "Overall," "Ultimately."

**Persuasive scaffolding**: "In a world where…," "Imagine a…," "What if I told you."

**Formatting**: em-dash overuse, mid-paragraph boldface, bolded lead-in labels that restate their own sentence, title-case headings, unrequested emoji, typographically perfect curly quotes where a person would have typed straight ones, stacked hyphenated modifiers (cutting-edge, state-of-the-art, next-generation).

**Punctuation, calibrated**: semicolons and exclamation points read as tells in casual online prose. They are *not* tells where the punctuation is conventional and working. See the carve-outs.

---

## The method

Running the tiers as a scan produces a feature count. Run this instead.

**Simulate a skeptical reader who knows the field.** Not a friendly one: a friendly reader fills in the blanks for generic writing and lets it pass. This reader is busy, competent in the subject, and not automatically impressed. Read the draft as them and ask one question: *did this writer say something to me, or did they write around the topic?*

That reader catches what a checklist misses. They hit "meet customers where they are" and think, fine, but what am I supposed to do differently on Monday. They hit a four-part abstract list and can't hold it. They hit a claim with no consequence and stop believing the writer has been in the room.

**Then check plausibility of the author.** If this came from a working marketer, founder, novelist, or whoever the text implies, are these the words they'd reach for? Would they notice this friction? Would they frame it this way for a peer? A model can state expert facts while writing like someone who has never been inside the room, and this test catches that where a fact-check can't.

**The fix:** replace vague, average, or non-specific language with specifics. Maybe the writer lacked source material, context, or was just sloppy. If they really lived what they're writing about, how would they actually talk about it? Pick a reader, a real point of friction, and the words that person would recognize.

---

## Genre carve-outs

Recognize the register before applying anything. Several patterns above are conventions in specific genres, and stripping them is the more damaging error.

**Direct-response sales copy**: keep exclamation points for energy, em-dash asides, ellipsis pacing, all-caps on a word or two, pain-triplet rhythm (three short stacked sentences naming three felt costs), sentence-starts with "And" or "But," reveal setups that the body actually pays off, repeated rhetorical setups across an email sequence, short fragmented paragraphs, a signature with personality. Close hard: the loose ending recommended above is wrong here. The legitimate tell in this genre is generic mush replacing specifics: abstract result-language where a named time-to-outcome belongs, abstract credibility-language where a named person belongs.

**Literary and genre fiction**: most of this catalog doesn't apply. Route to a fiction-editing pass instead. The composition tier's instincts about consequence and dramatization are relevant. The vocabulary tier mostly isn't.

**Academic and technical**: formal connectors, semicolons, hedged qualifiers, and announced conclusions are conventional and often required. Don't flag. Structure is expected to be explicit.

**Structured business documents**: a client update, a decision memo, a recurring newsletter with a fixed format. Headings and recaps are the format working, not a generic answer leaking in.

When the input sits in one of these registers, name the register and what will be skipped before applying anything, rather than mass-stripping features that are doing genre work.

---

## What to leave alone

The most important section, because every instinct in an editing pass points the other way.

**Roughness that is evidence of a person is not an error.** Missing capitals, a typo, a dropped period, a sentence that trails off, a word repeated because the writer was worked up, an aside that isn't strictly necessary, a point made twice with more heat the second time. These read as a human being who had a thought and posted it. Cleaning them produces prose that is *more* correct and *more* obviously machine-touched.

Distinguish two things that both look like errors. **Residue** is what a machine leaves behind: chatbot framing, mechanical hedging, structural announcements. Remove it. **Traces** are what a person leaves behind: the irregularities above. Leave them. When unsure which one you're looking at, ask whether the irregularity costs the writer anything. A typo costs a little credibility and buys nothing, which is exactly why a machine wouldn't produce one.

**Don't manufacture roughness either.** Adding typos to otherwise perfect text is the distressed-costume version of this. The irregularity that matters is structural (where the attention went) and it can't be sprinkled on afterward.

**Leave a clean sentence alone.** If it's fine, it's fine. The urge to improve everything degrades good writing, and restraint is the harder craft.

**Rhythm belongs to the writer.** Staccato, line-break cadence, the build-and-pop of a stacked passage: these are the writer's hand. A pass that tries to reproduce them typically copies the surface, compresses past the point where the meaning survives, and produces fragments that parse only if you already know what they meant. If the cadence is itself an AI tic or a machine tell (too-even, stacked tricolon, metronomic clause-pairs), that is not the writer's hand. Fix it. Otherwise get the draft to the state where the writer's own pass is all that's left, and stop there.

---

## Loaded by

- `../../os-skillify/references/humanize.md`: the register-repair method, run as a rewrite over instruction files
- `../../os-skillify/modes/cleanup.md`: the pass after AI writes or rewrites instruction files
- `../../os-skillify/SKILL.md`: loaded when producing skills, so what this file catalogs doesn't ship in a new skill

## Evolution

Items earn their place empirically. The current crop of hard tells (load-bearing, the shape of, the move) is dated: vocabulary tells rotate as models change, and this tier will need pruning within a year. The composition tier should be more stable, because it describes how a model behaves rather than which words it favors.

When a writer's before-and-after edit contradicts something here, the edit wins and the item gets revised or dropped. Three such corrections are already recorded above: length has no preferred direction, item counts are not the signal, and the rhythm ban is against impersonating the writer's hand, not against fixing a machine cadence.

This file replaces two earlier references that overlapped: a 30-pattern structural checklist and a ~100-item disallowed-language catalog. They duplicated hedging, generic conclusions, signposting, and the punctuation rules under different names. Merged 2026-08-01.
