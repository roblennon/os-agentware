# os-agentware

Agentware is a new operating category, next to software and middleware. It combines harnesses, AI, agents, code, applications, GUIs, sub-agents, skills, processes, and documentation into one system for doing work and achieving outcomes. This repo is the doctrine and the skills for building and running one.

Start with the doctrine: [`skills/os-agentware/references/agentware.md`](skills/os-agentware/references/agentware.md).

Then the two skills:

- `skills/os-showrunner`: the showrunner runs an agentware system. Orients from the project's state, delegates to workers and lieutenants, keeps the state true, keeps the operator's goals and momentum in view.
- `skills/os-agentware`: creating, modifying, maintaining, and improving an agentware system. The showrunner calls it when the stack itself needs work.

The companion skills (`os-skillify`, `os-hazmat`) and `skills/_shared/references` are what the two need to write good skills and keep them sounding like a person wrote them. Nothing here reaches outside the repo.

This repo keeps its own state in `agentware/`, the same way any project built with it would.
