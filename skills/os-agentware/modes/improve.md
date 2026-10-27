# Mode: improve

Part of `os-agentware`. Selected when something needs to go back into the system: a correction the operator made, a lesson a session paid for, a step that keeps getting done by hand, a tool that would retire a class of mistakes, research that should be findable later, or a rule that turned out to block work the operator wanted. Also selected when the system has grown and needs consolidating.

## Job

Fold the learning into the right place in the system, in the right form, so that a fresh agent next week does the thing the better way without being told.

## Run

**Find the root before writing anything.** A correction tells you what went wrong once. Before encoding it, ask why it went wrong, and then why that was possible. The fix usually belongs upstream of where the symptom showed: in the shared helper rather than the one call site, in the brief template rather than the one brief, in the principle rather than the instance. Fixing the symptom where you saw it is how a system accumulates twenty patches for one cause.

**Decide the form.** Each learning has a home that fits it:

- A judgment the operator holds, generalizable, with a reason: a principle in the relevant skill or SOP, written in the calibrated shape from `../references/rules-and-gates.md`.
- A check that can be stated exactly (a count, a format, a reference that must resolve): a script or a lint, with the reason in its failure message. Code holds its shape far better than a paragraph an agent has to re-read and re-interpret.
- A procedure done more than a couple of times: an SOP first. A skill once it has earned a registered slot by being needed often.
- A finding, a source, a thing that was true on a date: the knowledgebase, with the source cited and the noise left out.
- A decision the operator should not have to re-make: the decisions file, with the why, until it has landed in the files and can be trimmed to a line.

Pick the lightest form that does the job, and notice that a paragraph asking the agent to please remember something is the form that fails most often.

**Test the rule you are about to write.** Is it the cause or a correlation? If every good edit in a batch happened to be longer, "write longer" is a correlation wearing a cause; the real principle might be "be specific." Would the rule block work the operator asked for in a case you did not think of? If so it needs its because and its unless. Is it a gate or advice? Most lessons are advice. Write them as how we do things, not as what we refuse to do.

**Keep count.** Before adding a skill, check whether it is really a mode of one that exists. Before adding a reference, check whether one already covers it. When the skill count climbs toward the doctrine's limit, consolidate: related skills become one skill with modes, overlapping references become one shared file, skills nobody has invoked in months get retired or demoted to SOPs. Fewer, well-described skills get routed to. Many thin ones get ignored.

**Improve the tooling too.** When an agent has done the same manual steps three times, that is a script waiting to be written. When the operator keeps asking to see the same thing, that is a small GUI or a report command. Treat these as part of the system, documented in the skill or SOP that uses them.

**Trim as you go.** Folding a decision into the files is the moment to shorten its entry. Closing a slice is the moment to move settled state out of the door file. Archive rather than delete when there is any chance someone wants the history. What a session is forced to read should be what is active or recently finished.

**Write through skillify, then clean.** Changes to skills, modes, SOPs, and references go through `os-skillify` (its extend and refine paths), followed by the cleanup pass. The cleanup pass is what keeps the system's own files from drifting toward how a model writes by default, and that drift is the one failure that spreads.

## Output

The change itself, landed in the files, plus one plain line to the operator per learning: what went where and why that home. If something could not be placed (the lesson is real but the right home does not exist yet), say so rather than wedging it somewhere wrong.
