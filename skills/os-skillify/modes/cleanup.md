# Mode: cleanup

Part of `os-skillify`. Selected after AI has written or rewritten instruction files (skills, modes, references, principles files, SOPs, a context file) and the files need to come out sounding human and staying true. Also selected on request: "run hazmat on this skill," "this skill got too AI," "my skills don't sound like me anymore," "clean up after the loop rewrote things." Ordinary prose that isn't an instruction file wants the method in `../references/humanize.md` on its own rather than this whole mode. Structure, redundancy, and split-or-merge questions are `enhance`.

## Job

AI helps write skills, and self-improvement loops rewrite them. That is the point of the loops, and it has a side effect: with each rewrite, instruction files drift toward how a model writes by default. It gets more technical and more writerly, and less like a person talking. The drift matters beyond taste, because how an instruction file is written leaks into what the skill produces. A skill that reads like a compliance memo makes compliance memos. Left alone, everything the system touches sounds more like AI over time.

This mode is the counterweight: a pass over instruction files after AI has been through them, so the next rewrite doesn't inherit this one's tics. Its nickname is hazmat, because the material spreads, and the files it gets into are the ones every later file is written through.

## When to run it

After the writing is done. Let the generative mode, `extend`, `refine`, or the task's own authoring finish the draft or update first. Don't load this mode's catalog or method during that work; a model holding a list of tells while it writes produces different tells. Once the files exist, start a separate pass and load the material below. When the user invokes this mode on files that already exist, start here directly.

## What trustworthy means

Three different things, and they want three different kinds of attention.

**Correctness.** The file says things that are true. It doesn't contradict itself. Paths resolve. Counts match the thing the sentence is about. A correction applied in one place doesn't survive unapplied in a sibling. Sentences parse. Decisions the operator already approved actually landed. Best practices are stated with their why, not dressed up as absolute rules.

**Craft.** The file would still be a good instruction file if a careful person had written it by hand. A rule lives in one place and other files point at it. An example obeys every principle, not only the one it illustrates. The paragraph stating a rule is the first place to check for the rule being broken. The noun naming a rule matches how hard the rule really is: something called a gate should actually stop things, and advice should be called advice.

**Register.** The file doesn't sound like a model performing competence. That job has a method, `../references/humanize.md`, and a catalog, `../../_shared/references/ai-writing-patterns.md`. Call them; don't reinvent them.

## What to load

Skipping a reference is how this kind of work fails, so the list stays short.

1. This file.
2. `../../_shared/references/skill-prompting-principles.md`. How an instruction file is written leaks into what the skill produces. Skip this and the repairs will reproduce the register the pass exists to remove.
3. `../../_shared/references/ai-writing-patterns.md`, and `../references/humanize.md` when you reach register work.
4. The project's own before-and-after edits, when it keeps them: pairs of text the operator personally rewrote. A set of those in context pulls a model toward the operator's standard in a way no principle file can. Match the amount to the stakes, a curated handful for a quick pass and the whole collection for a high-stakes one, read in chunks when a tool has an output ceiling. Say which you loaded. If the project keeps none, say so and run on the principles, the catalog, and the method; the rewrites the operator approves in this pass are exactly what such a collection grows from.
5. Past cleanup entries, if the project keeps a decisions file or an archive and earlier passes wrote there. What the operator kept is as useful as what changed.

## The three piles

Sort every finding into a pile before acting, because one giant review table hands the operator a hundred mixed decisions at once and they stop reading at twenty. The piles are what lets each kind of finding get the right kind of attention.

**Taste.** Register changes that move meaning or voice, after dropping anything that fails the test *same meaning at the same length means leave it alone*. One file at a time. Present them as a three-column table (current, proposed, notes) using `../templates/review-table.md`, with verbatim text alone in the text columns. Copy the file to a `baseline/` beside the table before handing it over, and don't touch that file again until the operator says they are done. Apply their version the moment it arrives.

**Decide-once.** A choice that shouldn't be re-litigated file by file: whether quoted interview scripts stay as scripts, where a craft principle lives, what a repeated term should become. Bring one at a time, with no more than three options, and say which you would pick. If the operator asks for a batch so a longer stretch can run uninterrupted, batch them. Don't invent a fourth option.

**Leftover of an approved class.** Once the operator approves a taste table and says that kind of change may land elsewhere without a new table, apply that class across other files and report after. It covers the same tics and the same shop talk they already ruled on, not a first-pass rewrite of a file that never had a table. Search each term before closing it, including the sibling file the sentence points at.

**Routine cleanup**, as a quick final pass: typos, broken relative paths, sentences that no longer parse, stale counts, contradictions the operator already settled, and punctuation the project's own style rules out. No table, no permission, a mention in the report. Make these edits by hand, word by word, reading each site for sense. Find-and-replace produces fragments and misreadings.

## Run

Say what you are running and which references you loaded. If you notice you haven't read the files above, that is the moment to read them.

Name the set: a skill folder, a principles file, a family of references. Write it down once, with all of its files, and don't grow it mid-pass.

Verify corrections against the actual files, not against a worklist or an earlier report. Findings go stale while you work, and a fix applied where you noticed it becomes a contradiction in the sibling you didn't open. Search the term before closing.

Then craft: rules restated at several sites drift, examples get re-read last and start teaching the opposite, self-reference breaks exactly when a style changes. The paragraph that states a rule is the first place to check. A rationale section inside a loaded file is a craft finding too: it belongs in the skill's unlinked `RATIONALE.md`, with only the why a rule needs left beside the rule. `../references/rationale-extraction.md` says what goes where. In an agentware system, a rule written as an absolute where the doctrine would have written advice with a reason is a craft finding as well.

Then register, through the humanize method, with the instruction-file genre in mind. Headings, tables, numbered steps, and frontmatter are the format working, not tells. An instruction that hedges into a suggestion has failed at its job. Check every repair against the whole catalog, because a rewrite is generation and generation re-introduces tics: replacing a prefab contrast with an aphorism is a different item on the same list. Read your own proposed cells for the exact patterns the row is fixing.

Keep the operator's own words in mind. If the file came from material a person wrote, go back to it and use their words, cadence, and meaning. Ask whose word a flagged term is before proposing its removal: the catalog lists words to question, and the operator's vocabulary wins.

When a decision surfaces that no existing principle answers, isolate it and keep going on everything else. Don't keep rewriting around it.

At the end, if the project keeps a decisions file or an archive, add a short entry: what you found, what the operator ruled, what you would do differently next pass. The next run reads it first, and a pass that doesn't write down what it learned repeats itself. If the project keeps no such file, skip the entry rather than inventing a place for it.

## More than one agent

Taste tables and decide-once stay in the main thread, the only place that hands the operator either. Leftover of an approved class and routine cleanup may run in parallel on disjoint files, one writer per file, every agent loading the same references and the same corpus. An agent that measures its window and can't hold its assigned corpus says so, with the arithmetic, instead of quietly working without it. Don't give two agents the same file unless deliberately comparing them, don't give a parallel agent a first-pass taste rewrite, and don't let one open a decide-once. Pointer files stay pointer files.

## What this mode does not do

It doesn't silently rewrite taste-sensitive prose. It doesn't audit structure, redundancy, or split-and-merge, which is `enhance` doing a different job. It doesn't run punctuation scripts unattended, because mechanical passes produce fragments that letter-level checks can't see. And if a run only finds punctuation, it has probably looked at the wrong things: the valuable finds are contradictions between siblings, claims that quietly stopped being true, and register the operator never chose.

## Output

A short report whose first sentence says whether the operator is needed. If they are, name the decision, the trade-off, and the action. If not, say so in one sentence, then what changed in a few plain lines. Close with what the operator should do or expect next. When the pass produced review tables, those are the artifact, and the report points at them.
