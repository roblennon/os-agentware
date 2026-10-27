# Mode: audit

Part of `os-agentware`. Selected when the operator asks for a checkup, when a project resumes after time away, or when a drift tell shows up: the same settled question asked twice, a rule that blocked work the operator wanted, output that sounds like the model's default, a file nobody can say is still true.

## Job

Look at the whole system, find what has drifted, bloated, duplicated, or gone stale, and hand the operator a short ranked list of what to fix first. Deciding what to do about it is theirs.

## Run

The mechanical checks (dead pointers, orphaned files, duplicated passages, skill count, always-loaded files carrying history) go to a worker with no context, who sees the system as it actually loads rather than as the map says it should. `../../os-showrunner/briefs/surveyor.md` is a ready brief and it is fresh eyes in a way the showrunner cannot be, since the showrunner knows where things are supposed to be.

The judgment tells stay with you. Each is a question, and a yes is a finding:

- **Re-deciding.** Does the system re-answer things it should already know? Where does this go, how do we name that, which branch. That is a missing rule, not a missing memory.
- **Blocked work.** Has a rule stopped something the operator asked for? That rule needs its because and unless, or it needs to go.
- **Correlation rules.** Is there a rule whose stated reason would not survive a counter-example?
- **Bloat.** Is there a file that only ever gets added to? Has state grown past what a session can usefully read?
- **Thin skills.** Are any registered skills thin enough to be a mode of another?
- **Register drift.** Do the system's most-used files sound like a model wrote them? That leaks into everything they produce.
- **Knowledge not used.** Is there a knowledgebase, and do the skills actually tell agents to search it?
- **Tooling gaps.** Are agents doing by hand, repeatedly, what a script should do?
- **System hygiene.** Stale worktrees, caches, containers, temp folders, logs nobody reads.

Rank what you found by how much daily work it touches, not by how easy it is to fix. Three to five things at the top, the rest below. For each, the file, the evidence, and who reads that file and what goes wrong when it lies.

Fixes go through `improve`, and register repair through the cleanup pass, after the audit rather than during it. Fixing as you go turns the audit into a different job halfway through, and the findings stop being comparable.

## Output

A short report. First line says whether the operator needs to decide anything. Then the ranked findings. Then, if the operator says go, the fixes run through `improve`.
