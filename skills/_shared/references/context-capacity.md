# Context capacity: keeping the skill listing inside the harness's budget

Every skill in a workspace costs something in every session, whether or not it runs: its name and description sit in the model's standing context so the model can decide to use it. Most harnesses cap that listing, and past the cap they degrade it in ways the interface doesn't show. On the operator's side it looks like the assistant forgetting procedures it used to follow, skills that stopped triggering, work getting lazier for no visible reason. This file explains the mechanism, how to check for it, and the levers that bring a library back under budget. It suggests. The numbers and the choices belong to the operator.

## The mechanism

**Claude Code** loads every skill's name and description into a listing capped at 1% of the model's context window by default. When the listing overflows, it removes descriptions starting with the skills invoked least, leaving bare names. A skill listed by name alone can still be invoked, and the model can still choose it, but it is much less likely to on its own, so it gets invoked less, so it stays stripped. The cycle runs quietly: `/doctor` estimates the listing's cost and names its biggest contributors, the Skills row of `/context` shows its size after the budget, and a warning goes to the debug log under `--debug`. Nothing in the ordinary interface says a word. Each entry's `description` plus `when_to_use` is capped at 1,536 characters regardless of budget, which sits above the 1,024-character platform limit a shipped description already obeys.

**Codex** caps the same listing at 2% of the model's context window, or 8,000 characters when the window is unknown. It shortens descriptions first, then omits skills entirely with a warning. Two skills with the same name both appear; it does not merge them.

**OpenCode** documents no cap. In the installed build, a skill found under several paths with the same name collapses to one entry; that is observed in the binary, not documented, so treat it as current behavior rather than a promise.

Plugins add their skills to the same listing under a namespace prefix, so a plugin skill sits beside a local one of the same name rather than replacing it. Skills uploaded to claude.ai sync back into Claude Code on the same account and land beside the local install rather than replacing it. In the audit this file came out of, every uploaded skill was reaching the model twice, once from the workspace and once from the cloud copy, and a copy uploaded under a name since renamed or folded kept its old slot with stale text. MCP connectors are cheaper, since their tool schemas load on demand, but their tool names still occupy the standing context; in one measured setup a handful of connectors added around two hundred names.

**A stock Personal OS install is over the default Claude Code budget on the day it is installed.** The shipped skills' descriptions total several times the 1% listing on a 200,000-token window. This is not a problem that arrives with growth. It arrives with setup, and it gets worse with growth, because a library that works earns more skills with fuller descriptions. The setup step that raises the budget or tiers the listing is part of installing, and the check below is how to notice when the library has outgrown whatever was set.

## How to check

Worth running after installing, after adding a plugin or a batch of skills, on a schedule (the weekly tuneup carries it as a step), and any time the assistant seems to have stopped reaching for skills it used to use. A subagent can run it from these steps without the conversation's context.

1. **Measure the listing.** In Claude Code, `/doctor` gives the listing's cost and top contributors, and the Skills row of `/context` gives its size after the budget. Outside an interactive session, sum each skill's `description` plus `when_to_use` (capping each at 1,536 characters) across every skill directory the harness reads, and compare against the cap for the window in use. Expect to find the total well over; the ratio is the finding.
2. **Count the duplicates.** Plugin skills beside local ones, cloud copies under old names, the same skill reachable under two paths. Each is a slot spent on a stale or redundant entry.
3. **Rank by use.** When the usage log is wired (`skill-usage-logging.md` describes the channels, and the harness hook is opt-in), it shows which skills are actually invoked; the ones a harness would strip first are at the bottom, and some of those are the ones other skills call by name. Without a log, ask the operator which skills they reach for by name in conversation, treat the rest as candidates, and wire the hook so next week's check has data.
4. **Sort into tiers.** Which skills does the operator reach for in natural language? Those want full descriptions. Which are called by name from other skills, or run on a schedule? Those need only a name. Which are never called by anything and rarely by the operator? Those can stay hidden until typed.
5. **Look at the plugins and connectors.** Which are enabled for every session but matter in a few repositories? Which connectors are on everywhere and used a few times a month?
6. **Report the arithmetic and a proposed tiering.** The operator decides. A skill's description is also its public face in some setups, and hiding a skill changes what the assistant reaches for, so the proposal names the cost of each move.

## The levers

None of these is required. Each has a cost worth weighing.

**Raise the budget.** Claude Code accepts `skillListingBudgetFraction` in any settings file (0.04 is 4%), or `SLASH_COMMAND_TOOL_CHAR_BUDGET` as a fixed character count; `skillListingMaxDescChars` caps each entry. The listing then costs more context in every session. Raising the budget without also trimming the listing moves the cliff rather than removing it.

**Thin the descriptions.** What belongs in a description is `frontmatter-format.md` Rule 3: the job, the distinctions that affect selection, the modes, the trigger phrases, and a negative trigger where confusion with a sibling is real. What the budget adds is order: the harness truncates from the end, so the key use case and the trigger phrases go first, and a long list of everything the skill does not do is the part most likely to be cut. Codex and the cloud surfaces read the same text, so this lever works everywhere.

**Tier the listing.** In Claude Code, `skillOverrides` in any settings file sets each skill to `on`, `name-only`, `user-invocable-only`, or `off`. Name-only costs a few tokens and still runs when another skill or the operator invokes it by name. User-only costs nothing until the operator types its slash command. Plugin skills are not covered by `skillOverrides`; those are managed through `/plugin` and `enabledPlugins`. Codex has no name-only tier: it can disable a skill by path in its config, or a skill can carry `agents/openai.yaml` with `policy.allow_implicit_invocation: false` to stop auto-triggering while staying invokable by name.

**Fold skills into modes.** Two skills that always run together, or one that exists only to be called by another, can become one skill with modes. The mode body loads only when used; the listing pays once.

**Install plugins where they matter.** A framework plugin installed at project scope loads only in the repositories that use that framework; `enabledPlugins` is accepted in a project's `.claude/settings.json`. Installing at user scope puts every plugin skill in every session.

**Turn connectors off where they aren't used.** `disableClaudeAiConnectors` applies to the connectors Claude Code fetches for itself in terminal, IDE, and SDK sessions; a desktop-app session governs its connectors from the app's own settings. `deniedMcpServers` removes named ones. When one is needed for a task, the operator turns it back on for that session. At a few uses a month, the restart is cheaper than the standing cost.

**Keep cloud copies in sync or don't keep them.** A skill synced from claude.ai doesn't update when the local file changes, and deleting the synced directory by hand only gets it re-downloaded. The skill has to be removed on claude.ai. What that audit settled on: put only the skills you actually use on the web there, and the rest come off claude.ai, because a library uploaded wholesale costs its whole listing twice. When the operator wants some skills on the web, work toward one copy of each in the listing: local for everything, cloud only for the few that earn it, and the second slot for those few taken knowingly rather than by default. `os-skill-deploy` owns the sync story and can report which cloud copies are behind.

## The costs, so they get weighed

Hiding a skill that another skill reaches by description rather than by name breaks that caller; the callers are worth checking before a tier changes. Shortening a description by cutting its trigger phrases removes the routing the exercise was meant to protect. A bare name in the listing means the harness cut the description, not that the file is broken. And the cap differs by harness and by context window, so the measurement that matters is the one for the setup in use, not a number from this file.

## Where this came from

On 2026-09-01 the operator's own library, 67 skills plus a 30-skill plugin plus 17 stale cloud copies, was nine times over Claude Code's listing budget. About 50 of 67 skills were arriving as bare names, including the ones that run the capture, tuning, and delivery loops. The assistant had been getting lazier for two weeks across three harnesses and two model families, and the cause was the listing, not the models. The fix took a day: tier the listing, thin eighteen descriptions, fold four skills into modes, turn off a plugin and the connectors, delete the cloud copies. This file exists so the next operator finds it in an hour.
