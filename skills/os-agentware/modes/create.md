# Mode: create

Part of `os-agentware`. Selected when there is no system yet, or when a project exists and the work is to give it one: a showrunner, a place for state, the first skills and scripts, a way for learnings to flow back in.

## Job

Stand up a system that does one real thing end to end, inside whatever conventions already exist, and leave it shaped so the next thing is easier to add than the first.

## Run

**Start from what exists.** Before designing anything, look. The project's context file, its folder layout, any skills or scripts already there, how it tracks work, which harness it runs in and what that harness natively provides. Most of a system's first draft is already lying around in the form of things the operator does by hand or has half-automated. Inventory that honestly. Then look at the operator: what they are trying to achieve, what they do over and over, and what makes them wince when they open the task list. The first target sits where those three overlap. Think big about the workflow and small about the first build.

**Map the workflow before building any of it.** Lay the whole thing out, every stage, and mark who does each one today: the operator, the AI, both, or a script. Then decide, stage by stage, which ones move. Some stages want a skill (judgment, repeated, varies by case). Some want an SOP (rare, long, needs reference material). Some want code (deterministic, exact, fast, or run a thousand times). Some stay with the operator because the judgment is theirs and the decision is where the value is. Nothing has to move on day one. Improving the worst step of a real workflow counts.

**Build the worst step first, rough.** Run the whole pipeline badly before polishing any part of it. Cross-step dependencies only show up when the thing runs: the outreach step discovers the research step never captured what it needed. A polished first step is usually a polished guess about how the later steps will use it. When a step turns out to be deterministic, write the script then and there rather than having an agent do it by hand again next time. Scripts are cheap and they do not drift the way prose does.

**Put the showrunner in from the start, but build capabilities one at a time.** The showrunner is the operator's interface, so it exists from the first conversation. What it can delegate grows one capability at a time: get one reliable, then the next. An assistant that can do twelve things badly is worse than one that does two things every time.

**Set up state the way the project already does it, or use the default.** If the project has a tracker, a decisions file, a way of marking what is in flight, use that. If it has nothing, the showrunner's default layout (`../../os-showrunner/references/project-state.md`) is a reasonable start: a short door file for what is in flight, a map of the structure, and a decisions file that gets trimmed as things settle. Whatever you choose, the point is that a fresh session can orient from files alone, and that the files stay short enough to actually get read.

**Install so the harness finds it.** Skills go where the harness looks. For a portable install that is the open skills folder; for a harness-specific one, its own surface. Symlinks keep one source of truth; a whole-folder copy is the fallback where symlinks are not followed (some headless modes). The project's context file should name the state door as the first read, or every session that opens without being told will land blind. Say which harness you set up for and which parts are portable.

**Write the first rules from real corrections, not from imagination.** Seed the skills with a little craft, run a real session, and harvest what the operator had to say twice. That is the material. `../references/encoding-the-operator.md` has the method, and `../references/rules-and-gates.md` has the shape a rule takes so it does not harden into a gate nobody wanted.

**Hand the writing to skillify.** The skills, SOPs, and briefs you decide the system needs get written through `os-skillify`, then cleaned with the cleanup pass. You decide what and why. It makes the file sound like a person wrote it.

## Output

A working system that runs one real thing: the state files, the installed skills and SOPs, any scripts, the context-file line that points at the door, and a short note to the operator saying what runs, what still runs by hand, and what the next capability should be.
