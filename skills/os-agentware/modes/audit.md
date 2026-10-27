# Mode: audit

Part of `os-agentware`. Selected when the operator asks for a checkup, when a project resumes after time away, or when a drift tell shows up: the same settled question asked twice, a rule that blocked work the operator wanted, output that sounds like the model's default, a file nobody can say is still true.

## Job

Look at the whole system, find what has drifted, bloated, duplicated, or gone stale, and hand the operator a short ranked list of what to fix first. The operator decides. This mode finds.

## Run

Survey the system as it actually loads, not as the map says it should. Which files does the harness read on its own, which do the skills point at, which exist but nothing reaches. A worker in a clean context does this better than the showrunner, who knows too much about where things are supposed to be; `../../os-showrunner/briefs/surveyor.md` is a ready brief for it.

Then run the tells. Each one is a question, and a yes is a finding:

- **Re-deciding.** Does the system re-answer things it should already know? Where does this go, how do we name that, which branch. A rules gap, not a memory gap.
- **Blocked work.** Has a rule stopped something the operator asked for? That rule needs its because and unless, or it needs to go.
- **Correlation rules.** Is there a rule whose stated reason would not survive a counter-example?
- **Bloat.** Are always-loaded files carrying commands or history only a few sessions need? Has state or the decisions file grown past what a session can usefully read? Is there anything that only ever gets added to?
- **Duplication.** Does the same instruction live in two files? One of them is wrong, or will be.
- **Dead pointers and orphans.** References to files that moved. Files nothing points at, which may as well not exist.
- **Skill count.** Near or past fifty registered, and are any of them thin enough to be a mode of another?
- **Register drift.** Do the system's most-used files sound like a model wrote them? That leaks into everything they produce.
- **Knowledge not used.** Is there a knowledgebase, and do the skills actually tell agents to search it?
- **Tooling gaps.** Are agents doing by hand, repeatedly, what a script should do?
- **System hygiene.** Stale worktrees, caches, containers, temp folders, logs nobody reads.

Rank what you found by how much daily work it touches, not by how easy it is to fix. Three to five things at the top, the rest below. For each, the file, the evidence, and who reads that file and what goes wrong when it lies.

Fixes go through `improve`. Register repair goes through `os-skillify`'s cleanup mode. Do not fix during the audit; finding and repairing are different jobs and the clean eyes are for the finding.

## Output

A short report. First line says whether the operator needs to decide anything. Then the ranked findings. Then, if the operator says go, the fixes run through `improve`.
