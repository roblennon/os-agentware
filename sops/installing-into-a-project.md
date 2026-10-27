# Installing into a project

How a project gets these skills so its sessions can find them. An SOP, not a skill: read it when you are doing this, which is rarely.

## Where skills go

Harnesses look in a few places. The portable one is the open skills folder in the project (`.agents/skills/`), which more than one harness reads. Claude Code also reads `.claude/skills/` (project) and `~/.claude/skills/` (user). Codex reads its own folder. If the project is meant to be harness-agnostic, use the portable folder and add a harness-specific link only where that harness does not read it. Check the harness's current docs; this moves.

## Link or copy

A symlink from the project's skills folder to this repo's `skills/<name>` keeps one source of truth: update the repo, every project sees it. That is the default.

A whole-folder copy is the fallback when the harness does not follow symlinks (some headless modes do not). If you copy, note it in the project's decisions with the refresh rule: re-copy from the repo, do not hand-edit the copy, or the two will drift and one of them will be wrong.

Before relying on a link for an unattended run, prove it: dispatch one minimal headless run that reads a file from the skill folder through the link and quotes a line back. `../skills/os-showrunner/references/unattended.md` says why.

## The shared references

The two skills refer to `os-skillify` by name for writing and cleaning up instruction files. Any skill-authoring skill that loads the shared prompting principles and runs a cleanup pass after writing serves the same job.

## What they load

`os-skillify` loads files from `skills/_shared/references/`. A link or copy of a single skill folder breaks those pointers. Link or copy the whole `skills/` tree, or at least the skill plus `_shared/`.

## The door line

The project's context file (`AGENTS.md`, `CLAUDE.md`, or equivalent) names the project's state door as the first read for any session. Without that line, only sessions explicitly told about the state will find it, and everyone else lands blind. One sentence is enough.

## Checking it worked

Open a fresh session in the project and ask it to be the showrunner. It should read the state and report where things stand without being told where anything is. If it asks where the state lives, the door line is missing. If it cannot see the doctrine, the link did not resolve.
