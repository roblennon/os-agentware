# Project state

Where a project keeps what a fresh session needs to pick up where the last one stopped. This is the default layout. A project that already tracks its work some other way keeps its own way; what matters is the behavior, not the file names: a session can orient from files alone, decisions do not get re-made, and the files stay short enough to actually get read.

## The default layout

```
<project>/agentware/
  state.md        the door: what this is, what is in flight, what is parked
  map.md          the shape: what runs the system, who the crew is, how asks route
  decisions.md    the why behind choices still shaping the work (optional)
  briefs/         this project's saved worker briefs (optional)
  archive/        settled state and decisions, out of the way but findable
```

The state lives inside the project, not in the harness or the showrunner's skill folder, because it has to survive a change of harness and travel with the thing it describes.

## state.md, the door

The one file a fresh session reads first. It holds what the system is (a short paragraph), the ask in the operator's words, what done looks like, the budget and the undo story, what is in flight right now (the current slice, the next checkpoint and what it decides), and what is parked, one line each with enough to resurrect it. Dated at the top, so a stale date on an active project is itself a finding.

It stays about a screen long. The whole job is fast orientation, and a door that takes ten screens to open is a corridor. When it grows, that is the signal to trim.

## map.md, the shape

The slow-changing picture: what the harness loads on its own, what the skills point at, which scripts and tools exist and what they are for, anything outside the repo that drives the system (a scheduler entry, a cron job) with its real path. The crew: each recurring worker, what it takes and returns, where its brief lives. Routing: for the asks the project gets often, the first worker or skill that usually takes it. A few lines, and the showrunner overrides a row when the case in front of it warrants. Update it when structure changes, not when content does.

## decisions.md, the why

Optional, and most useful on projects with real design choices. One entry per decision with its reason and the alternative that lost, because the alternative is the part a fresh session could never infer and the part that stops the question being asked again. Also where a rule's origin lives: a rule in the system that traces to nothing here is worth questioning.

It is not append-only. Once a decision's consequences have landed in the files, its entry shrinks to a line with a pointer back to where the full record went. Entries nobody has needed across a couple of checkpoints move to the archive. The file carries what still shapes the work.

## Trimming and archiving

Closing a slice is the trim moment. Finished work leaves the in-flight section, becoming one line under recently completed or a line in the archive. Settled decisions compress. Parked ideas get a look: promote one to a slice, keep waiting, or drop it with a line saying why. Archive files live in `archive/` by year or by slice, and nothing in them is forced into a session's context, but a pointer from the trimmed entry means anyone who needs the history can get it in one step.

The test for any trim is one question: could a fresh session reach the original in one step? Drop the page, keep the reference.

## Writing it

State changes happen at the moment of the decision, during the work. During a long dispatch, rewrite the top of the door file so returning attention re-anchors on the goal.

The showrunner writes the project's state. Workers report, and the showrunner folds reports in. A lieutenant owns the state of its own subtree and nothing above it. When several agents genuinely need to write, split the file so each owns one, and say so in the map.

## The cold-read check (optional)

If you want to know whether the door actually works, have a worker with no context read `state.md` alone and answer: what is this, what was asked, what is in flight, what was decided last, what is parked, what happens next and who acts first, what must this session not do. The brief is `../briefs/cold-reader.md`. Compare the answers to reality; every wrong or missing answer is something to fix in the file. Worth doing after a big slice, before a handoff, or when a project resumes after time away. Not a ritual.

## Finding the door

Orient looks for `<project>/agentware/state.md` or whatever the project's context file names as the first read. That line in the context file matters: a project whose `AGENTS.md` or equivalent never mentions the state means every session that opens without being told lands blind. A project kept somewhere unconventional can hold a one-line pointer at the conventional path.
