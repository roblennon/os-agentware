# Unattended runs

Read this while writing the frame (the ask, done, budget, undo) for a project that will run without the operator watching: a heartbeat, a scheduled pass, a block of hours it gets to itself. Everything here was paid for on real autonomous builds, one early one in particular, so each piece carries the failure that taught it.

## Prove the run can read what it needs

A headless run usually sees only what is inside the project plus what the harness resolves through the project's skill links. Before the first unattended run, dispatch one minimal headless run that reads a file from the skill folder through the project's own link and quotes a line back. If that fails, install the skill as a whole-folder copy and note it in the decisions, with the refresh rule (re-copy, do not hand-edit the copy). That early build lost its whole doctrine to this assumption and only noticed while improvising around the gaps.

Working files stay inside the project, in a gitignored temp folder. Headless modes tend to reject reads and writes outside the workspace, and the rejection kills the run rather than degrading it. Pass this to every worker the run spawns.

## One engine

Exactly one thing dispatches autonomous work on a project, and the state file names it. When a supervising session and a heartbeat both hold "continue the build," they will eventually work the same slice. Depth comes from cadence and multi-slice runs, not parallel streams. A supervising session may watch, adjudicate, and edit doctrine; it does not start slices while the engine lives.

## Slices sized to the cap

An unattended run has a hard runtime cap, and work that is mid-slice when the cap lands dies uncommitted. Size slices so one fits with room to close: update state, note the decision, commit. Rewriting the top of the door file during long detours matters double here, because the next reader is not you.

When a run dies mid-slice anyway, the next run reconstructs from artifacts: the working tree, the temp folder, the last committed state. Treat that as normal, not an incident. Log what was reconstructed and close the slice properly.

## Stop conditions get tested

The engine stops by checking something: a status line in the state file, a deadline, a lockfile. Test each stop condition against the real artifact in its real format before the run starts, and again after any change. Prove it fires on the stopping state and does not fire on the running state. That build's stop check searched for a plain status line while the state file wrote it in bold, and the engine kept dispatching full sessions at an idle project until a human noticed. Stop conditions written from the format the author imagined rather than the format the file uses are the signature failure of this whole mode.

Lock discipline has its own trap: if the script's exit trap releases the lock, and the script also releases early to chain a successor, the parent's trap can fire after the child has taken the lock, deleting it and opening the door to a second engine. Clear the trap before releasing and chaining. Give any chain a backoff for short runs and a hard deadline after which only the scheduled tick remains.

## The engine's config is part of the system

A scheduler entry or cron job lives outside the repo, which puts it outside every check the system runs on itself. Give it a row in the map with its real path and interval, keep its logs inside the project, and hold it to the project's own rules. That build's scheduler logged outside the project in violation of a rule four in-repo files repeated, and no pass could see it.

## Keep the dispatch prompt small

The prompt is the only instruction an unattended run is guaranteed to get, and restating the project's rules inside it starts a divergent copy. That build ended up with three rules lists, and the prompt carried the weakest one, missing exactly the rules that protected real people's data. Name the engine's identity, point at the state file as its first read, and point at wherever the project's hard rules canonically live. Inline only what the run needs before it can read anything.

## Honesty when nobody is watching

Unattended runs feel pressure to record green. When a check could not be run the designed way, record the substitute and the gap at the moment of the substitution, so the next attended session knows what still owes a real look. A self-graded pass over a defect is worse than no pass.

## Budget

An unattended window burns quota with nobody to notice. The frame sets the budget in slices and wall-clock; the engine's cadence, cap, and chain deadline are how that becomes mechanical. When the budget is spent, the engine stops and the status line says so. New work needs a fresh frame from the operator, not a quieter continuation.

## A reference engine shape

A small script the scheduler fires: take the lock; check the stop conditions; dispatch one harness run with the small prompt above; enforce the runtime cap; log inside the project; release cleanly (trap cleared first) and optionally chain. Every environment-bound value is a slot the frame fills: project path, harness binary, cap, cadence, chain deadline, stop pattern. Write it fresh per project against this shape rather than copying the last project's constants.
