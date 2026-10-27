# Cleanup at milestones

What to clear when a slice closes, a milestone lands, or a project pauses. Written as an SOP: read it when you are doing this, and copy its list into the project's own instructions. Agentware runs a lot of processes and leaves a lot behind, and a machine that fills up gets slow in ways that look like the agents getting worse. Bake the list below into the project's own context file so it happens without anyone remembering.

## The machine

- Git worktrees that no lane is using. List them, confirm the branch is merged or pushed, remove the worktree and then the branch.
- Branches already merged.
- Docker containers and images from experiments; volumes nobody mounts.
- Package caches, build caches, model caches that have grown past what the project uses.
- Temp folders inside the project (the gitignored working folder), logs nobody reads, scratch outputs that were never promoted.
- Background processes and scheduled jobs that belong to finished work.

Confirm before removing anything that is not reproducible. A worktree with uncommitted changes gets looked at, not deleted.

## The files

- The state door: finished work leaves the in-flight section.
- Decisions whose consequences have landed compress to a line; stale entries move to the archive.
- Parked ideas get a look: promote, keep, or drop with a reason.
- Always-loaded files (the context file, the most-used skills): anything only a few sessions need moves to an SOP or a reference.

## The skills

Every so often, not every milestone: count the registered skills, notice which have not been invoked in months, and consider rolling thin ones into modes of a neighbor or demoting them to SOPs. `os-agentware`'s audit mode does the fuller version.
