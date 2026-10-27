# Cluster coherence signals

Patterns that indicate when a set of skills (or sources, in `from-prompt` mode) is *truly cohesive* (consolidate into a category skill) vs. *adjacent but distinct* (leave as siblings) vs. *intentionally divergent* (don't touch). Used primarily by `enhance` mode but informative for `from-prompt`'s cluster decisions and for any cross-skill `consolidate` work.

## Signals indicating consolidation

A cluster of skills is cohesive (= should be modes of one category skill, with shared references) when:

### Heavy mutual cross-references

The skills cross-reference each other extensively. Skill A says "use `$skill-B` for X"; skill B says "use `$skill-C`" or "when running under `$skill-A`"; etc. The reference graph is dense, not sparse.

In the v0.1 bug-investigation pilot, **9 of 14 sources** cross-referenced 3+ siblings. That density was the strongest cohesion signal.

**How to detect:** grep each source for `$<skill-name>` patterns, standard `.agents/skills/<name>/` paths, and legacy or harness-specific paths such as `.codex/skills/<name>/` and `.claude/skills/<name>/`.

### Shared vocabulary

Multiple skills use the same labels for the same concepts: severity rubrics, status vocabulary, classification taxonomies, lane vocabularies, output formatting rules.

In the v0.1 pilot:

- **Atomic hypothesis method** (Observed facts / Hypotheses with confidence / Ruled out / Unknowns) appeared in 3 sources.
- **ROOT / PARTIAL_ROOT / SYMPTOM classification** appeared in 2 sources.
- **Lane status (`complete/partial/blocked/pending`)** appeared in 4 sources.
- **User-attribution rule** ("unknown (not tracked)") appeared in 3 sources.

Each of these crossed the two-skill threshold for promotion to a shared reference.

**How to detect:** grep for canonical phrases (`atomic hypothes`, `ROOT`, `PARTIAL_ROOT`, `complete/partial/blocked`, etc.). Multi-skill matches → promote.

### Same job-shape

Skills that have similar workflow shapes (similar input → similar processing arc → similar output structure) are sibling-mode candidates. Different job-shapes → separate skills.

In the v0.1 pilot, all 6 modes of `dev-investigate` had a similar job-shape: scope → evidence/inputs → hypotheses or analysis → output (handoff package, verdict, hunt findings, mutation pressure-test, etc.). The shared shape made the consolidation natural.

**How to detect:** Read the workflows side-by-side. If the section headers in their `SKILL.md` or workflow files are similar (Scope / Inputs / Run / Output / Guardrails), they're shape-aligned.

### Cluster-shared craft moves

Specific craft moves that recur across siblings: *lead with plain language*, *never claim 100% certainty*, *include "what this cannot be"*, *prefer one stronger property test over many weak examples*. When these appear in 2+ skills, they're cluster-shared.

**How to detect:** During `enhance` Survey phase, build a per-skill craft-move list. Cross-check for overlapping moves.

## Signals indicating split

A single skill should split when:

### Two distinct job-shapes inside one skill

The skill's workflow has two clear phases that don't share inputs / context / output discipline. Example from v0.1: `investigate-and-update-bug` did atomic-hypothesis investigation AND cross-system posting, different inputs, different output disciplines, different safety constraints. Split into `evidence` (mode) + a bug-comms style coordination skill (standalone).

**How to detect:** Look for the skill's prompt body having two largely-independent halves with different vocabulary, different output shapes, or different guardrails.

### Different reference sets per mode

In a category skill with modes, if the modes draw from disjoint reference sets, the skill might benefit from splitting into two category skills.

Example: a hypothetical `editing` skill where some modes load prose-editing references and others load code-editing references → split into `prose-editing` and `code-editing`.

**How to detect:** Per-mode reference-load matrix. If two cluster-modes have <30% overlap in references, that's a split signal.

### Different invocation patterns

If users would invoke part of the skill very differently from another part (e.g., one part wants a `/<name>` slash-command, another wants description-match triggering), they may be different skills.

## Signals indicating drift (legacy patterns to review)

These indicate that a source may be carrying assumptions from another harness, an older tool version, or a private setup. They are review candidates, not automatic rewrites. Preserve the job and the user's actual constraints, then fit the implementation to the target harness.

### Custom scheduling / heartbeats

The source has its own RRULE-based scheduling, custom heartbeat task creation, or polling-style loops.

**Adaptation:** Keep the per-cycle behavior in the skill. Let the target harness's documented recurring-task or wake-up mechanism own cadence when one exists. If it does not, keep the process explicit and run it manually rather than naming another harness's command as the portable answer. Document any native adapter in `RATIONALE.md`.

### Subagent restrictions

The source carries delegation rules that may have come from an older harness policy or a particular user's setup. The substantive guidance, such as splitting work by disjoint risk surface rather than arbitrary file chunks, may still be valuable.

**Adaptation:** Check the target harness's capabilities and the active user or workspace instructions. Keep real policy constraints. Translate capability names when only the terminology changed. Remove a restriction only when it no longer applies.

### Codex case-system mirroring

References to `lanes.json`, `hypotheses.jsonl`, `timeline.jsonl`, or `case.yaml` may belong to a specific DeliveryOps implementation rather than to the skill's job.

**Adaptation:** Check whether the target workspace actually uses that case system. If it does, keep the integration and label the dependency. If it does not, keep useful concepts such as lane status and hypothesis tracking without inventing replacement files.

### Hard-coded harness paths

Separate two cases before changing anything:

- Skill and bundled-resource paths should resolve relative to the skill where possible, or use the Agent Skills standard when an install location must be named.
- Native harness config, state, and credential paths stay in that harness's documented location and are labeled as harness-specific. Do not translate one harness's config path into another and call that portability.

Drop a path only when it was incidental scaffolding. If current behavior is uncertain, check the harness's official documentation.

### Codex skill cross-references that don't exist in the current library

References like `$swr-quality-gate`, `$observability-harness-loop`, `$stateful-conformance-lab`: Codex skills that haven't been converted. The conceptual lanes are real. The specific names aren't valid in the current library.

**Adaptation:** Replace specific Codex skill names with conceptual references (*"invoke a proof-strategy skill when the gap is proof quality"*) OR keep as inert pointers (*"when `$swr-quality-gate` is converted, this lane will invoke it"*) with decision-log noting.

## Signals indicating intentional divergence (`NO-OP`)

Sometimes apparent overlap is intentional:

### Same vocabulary used for different reasons

Two skills use the term `FIX_NOW` but mean slightly different things in their respective contexts. If consolidating would force one to inherit the other's nuances incorrectly, leave them divergent (with a `NO-OP` decision-log entry explaining the choice).

In the v0.1 pilot, Cursor's `RISKY` triage state and Duck Hunt's `DEFER` triage state were close-but-not-identical. Phase 2 user input clarified: unify to four terminal states (`FIX_NOW / HUMAN_DECISION / DEFER / DISMISSED`), with `RISKY` collapsing to `HUMAN_DECISION` or `DEFER`. That's a `CONSOLIDATE` outcome, but the question of whether to consolidate was real.

### Domain-specific tuning

Skills serving different domains may have parallel structures with intentionally different parameter tunings (e.g., a *mutation-scout for code* might generate 3-8 mutants, a *mutation-scout for prose* might generate 5-15 because the surface is denser). The shared shape doesn't mean the values should align.

### Stylistic divergence reflecting different audiences

Some skills lead with technical detail (developer-facing). Others lead with plain language (cross-system / user-facing). Both styles can be right for their audiences; consolidating rules across them would lose the audience-fit.

## How to use these signals

In `enhance` Phase 2 (Detect signals), bin findings by signal type:

| Signal type | Example finding | Default disposition |
| --- | --- | --- |
| Heavy cross-references | "Skill X says use $Y for Z; Skill Y has Z too" | Investigate consolidation |
| Shared vocabulary | "User-attribution rule appears in 3 skills" | Promote to shared (`CONSOLIDATE`) |
| Same job-shape | "Skills A, B, C all follow Scope→Evidence→Hypothesis→Output" | Investigate category-skill structure |
| Two-jobs-in-one | "Skill X does investigation AND posting" | `SPLIT` |
| Harness-bound scheduling | "Skill embeds its own recurring-task mechanism" | `ADAPT` to the target harness when supported |
| Harness-bound delegation rule | "Skill assumes a specific subagent policy" | Review active policy, then `ADAPT` or `NO-OP` |
| Hard-coded harness path | "Skill installation or private data path is fixed to one machine or harness" | `ADAPT`; keep correctly labeled native config |
| Stale Codex skill cross-ref | "References `$delivery-ops`" | `NO-OP` with note (until DeliveryOps converts) |

Then surface to user via `AskUserQuestion` for borderline calls. Apply non-borderline ones directly.

## Used by

- `enhance` mode: Phase 2 (Detect signals).
- `from-prompt` mode: Phase 1 cluster-grouping (when classifying multiple sources for a category-skill conversion).
- `consolidate` mode: Phase 1 (cataloging vocabulary differences and coverage overlaps between two drafts).

## Source

Distilled from the v0.1 bug-investigation pilot. Encoded here so future runs can identify these patterns faster than the pilot did.
