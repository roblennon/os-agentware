# Delegation

How the showrunner hands work out and gets it back: workers, lieutenants, briefs, splitting broad work, and keeping a shared tree sane when several agents commit to it. Read before the first dispatch of a session.

## Workers

A worker is anything with a bounded job: a subagent in a clean context, a skill, a script, a tool, a one-off brief written at dispatch time. Most of what a showrunner dispatches is the last kind, and the brief does not need saving afterward. A line in the state saying the dispatch happened and what it settled is enough. When the same shape recurs, save the brief in the project's `briefs/` folder, through `os-skillify`, and list it in the map.

A worker gets its brief plus the inputs the brief names, and that is its whole world. A reader with no history reads harder and catches more than the main thread, which knows too much. The brief carries only what the worker cannot infer: the job in a sentence, the inputs, the procedure where it has to be exact (a search pattern, a count, a format), the report shape, and the boundaries. Restating things any capable agent already knows just makes the brief longer.

Reports come back as files or structured replies. Ask for where it looked, how it went about it in a line, what it concluded, and what it could not resolve. The gaps matter as much as the conclusion, because the next dispatch starts from them, and the line on method is how you notice a worker that reached the right answer the wrong way.

Workers can write files, including code and documents in the project. What keeps that sane is that two agents do not edit the same file at the same moment, which the shared-tree rules below handle, and that the showrunner is the one who folds results into the project's state.

## Lieutenants

A lieutenant is a showrunner for a specialty: one book inside a fiction catalog, one subsystem inside a build, one research lane. It earns its place when the specialty carries more state than the top showrunner should hold, recurs enough that continuity matters, and has worker shapes of its own. One long task is not a lieutenant; it is a worker with a longer brief.

A lieutenant's brief names the outcome it answers for, what is deliberately not part of that outcome, the decisions it brings back to the operator instead of making, and how many passes it has before reporting regardless. How it does the work is its own judgment and the project's skills. It owns the state of its subtree and nothing above it.

The top showrunner decides whether another pass starts. This is where long work goes wrong: a lieutenant that keeps going because nobody told it to stop drifts one reasonable step at a time, and from inside, drift reads as progress. Read each return against the ask, the done point, and the budget in the state file. A return that still answers to the ask continues. One that has quietly started answering a better question goes to the operator, because following the better question is their call.

One practical thing: a lieutenant that spawns background children and then goes idle can get ended by the harness, which leaves the children ownerless. Spawn children in the foreground, or have the lieutenant poll for their files.

## Splitting broad work

Some asks are too wide for one worker: a question about a whole catalog, a system-wide audit, an investigation across several subsystems. Reading it all yourself spends the one context window the project cannot replace. Dispatching one worker with the whole ask gets back a report too big to fold.

Turn the ask into the questions it actually contains. Check what the project already holds before spawning anything: an earlier finding, a decision, a result from a previous slice. Reusing it is a read, and redoing it is a whole context window. Start with the smallest overview that could settle the easy questions and let its gaps decide what the next workers chase. Independent questions run in parallel, one per worker, scopes that do not overlap, each pointed at what already exists. Dependent ones run in sequence. As reports land, the state gets a line each with a pointer, so a later session reuses them.

## Several agents on one tree

The doctrine favors everyone working on the same main branch and reconciling often. That works when a few rules are in the project's own instructions, because several lanes committing to one checkout will otherwise sweep each other's half-done work:

- Commit by path, naming the files, and leave staging alone. A blanket add picks up another lane's edits.
- Pull with rebase before pushing.
- Keep the tree compiling (or whatever the project's equivalent is) between steps, so a check that looks at the working tree does not block every lane whenever one lane is mid-edit.
- When two pieces of work genuinely overlap on the same files, separate them: a worktree or a branch for the duration, merged back as soon as the overlap ends. Separation is for real overlap, not a default.

Put these in the project's `AGENTS.md` once and every lane inherits them.

## Keep the pen moving

While workers run, keep going. Dispatch a review of the piece that just landed and start the next piece. Fold the review in when it arrives. The main thread's job is judgment and the operator; the workers' job is the reading, the checking, and the bounded building.
