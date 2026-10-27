# os-agentware: map

The shape of the repo. One line per piece, what points at it, what it points at. Pieces marked (planned) do not exist yet.

## Layout

```
os-agentware/
  README.md                        the door for a stranger; points at the skills and the doctrine
  AGENTS.md                        lean, always loads; points at agentware/state.md and the skills
  agentware/                       this repo's own state: state (the door, kept short), map, decisions (trimmed; settled entries move to archive/)
  skills/
    os-agentware/                  the concept: create, improve, and audit an agentware system
      SKILL.md                     anatomy, the three modes, the principles that run through them
      modes/                       create, improve, audit
      references/agentware.md      the doctrine, from Rob's write-up
      references/                  rules-and-gates, encoding-the-operator
    os-showrunner/                 the runner: orient, delegate, keep state true, keep momentum
      SKILL.md                     arriving, working with the operator, scope, delegating, state, unattended
      references/project-state.md  the state/map/decisions/briefs layout, as a default that flexes; trimming and archiving
      references/delegation.md     workers, lieutenants, briefs, several agents on one tree
      references/unattended.md     heartbeats, one engine, stop conditions, dead-thread recovery
      briefs/                      reusable worker briefs: surveyor, cold reader
    os-skillify/                   (planned) portable skill authoring, Personal OS mandates stripped; hazmat (the cleanup pass after AI writes instruction files) is a mode of it
    _shared/references/            (planned) prompting principles, frontmatter rules, naming, skill-vs-mode-vs-reference, self-extending, work orientation, AI writing patterns, SOP completeness
  sops/                            installing into a project, cleanup at milestones
```

## Crew

- Showrunner: this session (Claude Fable 5.1), single writer for the skills in this slice.
- Reviewers (planned): Fable 5.1 subagents for fresh eyes on each skill and a cold read of state.md. Reports only; the showrunner folds them in.

## Routing

- Changing the doctrine: edit `skills/os-agentware/references/agentware.md`, log the why in `agentware/decisions.md`.
- Changing how a project is run: `os-showrunner`.
- Changing how skills are written: `os-skillify` and `_shared/references/skill-prompting-principles.md`.

## Thresholds

- A fresh agent with only this repo can orient from `README.md` and run as showrunner on a new project without reaching into Personal OS.
- No file in `skills/` references a path outside the repo.
- Skill count stays small: the doctrine says under 50, this repo ships a handful.
