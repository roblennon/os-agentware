# os-agentware: decisions

Newest first. One entry per decision with its why. Entries whose consequences have landed in the files get trimmed to one line or moved to `archive/decisions-<year>.md` at checkpoints, so this file only carries what still shapes the work.

## 2026-10-27 — License: Apache 2.0 plus the Commons Clause

Rob: "i want people to use my agentware skill to do commercial work. i just don't want them to resell the agentware github itself." MIT would have allowed resale. A non-commercial license (PolyForm NC, CC BY-NC) would have blocked a consultant using the skills for client work, which Rob wants to allow. Apache 2.0 with the Commons Clause rider permits commercial use and forbids selling the software or a product whose value is substantially the software. The MIT draft is replaced.

## 2026-10-27 — State files are trimmed, not append-only

Rob: "the decision log may be getting too much prominence here. For things that always get added to and never get trimmed or archived (this includes state.md) there is bloat. I would rather some of these things be optional and auto-cleaned/archived so that only what is actively relevant or recently completed is forced into context." So: state.md carries what is in flight and recently completed; decisions.md is optional and gets trimmed or archived at checkpoints; the showrunner does the cleanup as part of closing a slice. The old skill's "append-only, nothing gets edited" rule is dropped.

## 2026-10-27 — Hazmat is a mode of skillify

The cleanup pass after AI writes instruction files travels as a mode of `os-skillify`, not a separate skill. Why: Rob's ruling; fewer skills, one place for everything about writing instruction files.

## 2026-10-27 — Doctrine retained near-verbatim from Rob's write-up

`skills/os-agentware/references/agentware.md` is Rob's 2026-10-27 write-up with light edits only: typos fixed (achieving, involves, lieutenant), "unconstrained in the way that normal software is" rephrased to "free of the constraints normal software lives under", a dangling empty bullet removed, headings normalized, and one opening paragraph added saying a system's own doctrine wins over this one. Everything else is his words. Why: the rewrite exists because the old skill drifted into a model's register; the doctrine is the one file that must sound like the operator.

## 2026-10-27 — Companion skills travel stripped, not slimmed to nothing

os-skillify, os-hazmat, and the shared references they load come along in as much fullness as is useful. What gets removed is the Personal OS inheritance (user profile, inbox, tracker, org rules, setup philosophy paths). What stays is the method. Why: Rob's ruling; the authoring method is what keeps the next skill from coming out in the model's default register, and it is useless if it can only run at home.

## 2026-10-27 — Primitives become suggestions that flex

The state/map/decisions/briefs layout, the brief anatomy, and the rest of the old skill's structures are kept as the default shape and written as things the agentware considers, not mandates. A project with its own conventions keeps them; a harness with its own surfaces gets them; otherwise stay agnostic and portable. Why: most agentware gets built inside projects that already have a way of doing things, and the old skill broke exactly where it met one.

## 2026-10-27 — No outside research pass

Built from Rob's own writing, corrections, and the four live projects (pets, therapist-sites, game-dev-lab, supercar-game). The August foundations doc's research citations are not carried forward. Why: Rob's ruling: research is how the last version went wrong.

## 2026-10-27 — Two skills, not one

`os-agentware` is the concept and the craft of building and improving a system. `os-showrunner` is the role that runs one. A lieutenant is a showrunner with a narrower brief, so it needs no skill. Why: Rob's framing: the show is the concept, the showrunner is the person making it happen.

## 2026-10-27 — New repo, prefix kept

Home is `~/gh_projects/os-agentware`, to be published on GitHub under roblennon. Skills keep the `os-` prefix. Why: Rob's ruling.

## 2026-10-27 — Dropped from the old skill

"Nothing executes, this is not software" (contradicts the doctrine: agentware is AI plus skills plus agents plus code plus process). "Single writer, workers never write" as architecture (the supercar-game lanes commit by path on one tree; coordination through files on shared main is the doctrine). The required cold-read check, the SELF-READ (weak) status, the closure surveyor, and the ratchet as gates (Rob's 2026-10-13 correction: proof-shaped friction makes a system oversteer itself; the showrunner's judgment is the gate). Why: each was either contradicted by the doctrine or by a correction on record.
