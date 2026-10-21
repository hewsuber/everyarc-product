# Everyarc — ADR 003: High support, high performance
*Decided by Hew, 2026-10-10. Changes `everyarc-curriculum-handling.md` §1.1, §4 and §5, `everyarc-competency-graph.md` §7 and `everyarc-semantics-and-feedback.md` §3 as named under "What changes". Everything else in those docs, ADR 002, and every other doc, stands.*
*v0.2 · 2026-10-10 · Shared. Change it through this doc's changelog.*

---

## Decision
Every child is held to an elite standard, and given the support to reach it. The engine works in the zone where a skill is hard but reachable (Vygotsky's zone of proximal development) and moves between two modes, item by item:

1. **High support, through concrete, pictorial, abstract (CPA, the Singapore approach).** When a child struggles, the next item moves one step toward the concrete (symbols to a picture, a picture to objects) and, if a prerequisite isn't solid, steps back to it at once, then returns.
2. **High growth, through variation (the Shanghai variation method).** When a skill is accurate and quick, support fades: the next items move one step toward the abstract and change one thing at a time (the numbers, the context, the representation, the unknown), so the child sees the structure, not one problem.
3. **A 100% gate, and "excellent" past it.** A skill opens what it leads to only when all of its last 20 first tries are right, across 3 sessions, 3 days and 3 ways (v0.2, Hew). The bar after a drop is the same. Past the gate, the engine keeps the skill in spaced checks and variation until the last 10 first tries are all right, answered at the skill's target speed, and held on at least two recent spaced checks with no miss among them. That is **Excellent**, a fifth state parents see on the Growth Map.

The engine reads three measures for each skill, all from evidence it already has:

| Measure | What it is | Where it comes from |
|---|---|---|
| **Accuracy** | First-try hits over the rolling window of the fluency bar (20) | `isHit` and the counting rules in §1.1 |
| **Automaticity** | The share of first-try hits answered at or under the skill's target speed | the attempt's duration bucket, counted from when the item is ready to answer (after read-aloud); assistive-input answers are left out |
| **Stability** | Hits on spaced checks (1, 3, 7 and 21 days) | attempts with `set_kind = spaced_check` |

| Mode | When | What the next item does |
|---|---|---|
| High support | accuracy under 80% over at least 5 counting tries, or 2 misses in a row | one CPA step toward the concrete; step back to the weakest prerequisite if one isn't solid; scaffolding at its fullest |
| Steady | neither | stays where it is; the §4 ladder and §5 redirects run as written |
| High growth | accuracy 90% or more over at least 10 counting tries, automaticity at least 60%, and no miss on a recent spaced check | one CPA step toward the abstract; a variation set that changes one parameter; hints offered later |

Every number is a starting default, declared in `packages/engine/defaults/curriculum.v0.json` under `pedagogy`.

## Why
- **It names what the engine was already reaching for.** Curriculum handling has the pieces: representations, step-backs to the first prerequisite that isn't fluent (R2), stretching within a skill (R6), spaced checks, the "settled" test for recall. ADR 003 makes them one policy with one trigger set.
- **High expectations need a safety net, and the net needs a trampoline.** Errors are pinned to the foundational sub-skill and fixed at once; success fades support right away, so a child spends their time where growth happens.

## What it keeps
- **No clock, ever, on a child's screen.** Automaticity comes from duration buckets the device already records. It never shows, is never praised as speed, and never decides a skill's state. Pressure takes the working memory fluency is meant to free (graph §7, Ramirez and others 2013).
- **Supports never block.** A child with read-aloud, no timers or assistive input reaches every state the same way. Automaticity counts from after read-aloud and skips assistive-input answers, so it measures recall, not reading or motor speed.
- **Drops stay calm.** A skill past the gate drops back to practice only on the existing drop rule (under 90% over its last 10, or 2 spaced misses in a row); one later miss moves an excellent skill back to ready for more, nothing harsher.
- **Kids see no numbers.** Parents see five states. "Excellent" names a skill, never a child: the parent-language validator rejects "Ezra is excellent".

## Later subjects
The same two-mode shape carries to new subjects; the methods change. These are recorded now and built when the subject is (ADR 002: math K–8, then reading).

| Subject | High support | High performance |
|---|---|---|
| Science | Inquiry first (5E): a real anomaly or simulation before the law, whenever a concept is new or needs no numbers | Modeling instruction, once a concept is at 85%: the child draws the diagram or the graph that proves the claim |
| Coding | Cognitive apprenticeship while syntax accuracy is under 85%: worked code with focused blanks, explained line by line | Project work once syntax is at 85% and on pace: an open spec, or a broken program to debug unaided |

## What changes

| Doc and line | Before | Now |
|---|---|---|
| Curriculum handling §1.1, competency graph §7 | At least 90% over the last 20 (18 of 20); 92% over 25 after a drop | **100% over the last 20 (20 of 20)**, the same after a drop, with the same spread. Past the gate, the engine works toward excellent with spaced checks and variation sets |
| Semantics §3, the skill states; bridge contract `skill_state` | Four states | **Five:** Exploring · Practicing · Showing confidence · Ready for more · **Excellent** (contract P8) |
| Curriculum handling §4, the ladder | Per item: hints, model, step back | Unchanged within an item. **New:** across items, the mode picks the next item's CPA step and scaffolding |
| Curriculum handling §5, R2 and R6 | R2 steps back after modeled or hinted runs; R6 stretches when 4 of 5 first tries are right | R2 also fires on 2 misses in a row or accuracy under 80%; R6 stretches as a one-parameter variation set |
| Content (turn 6) | Templates with variants | **New:** each template tags its representation's CPA step and which parameter a variant varies, so the engine can build variation sets |

## How it meets the standards
`everyarc-standards-and-safeguards.md` holds the engine to these; `standards/standards.json` tracks each.

| Standard | What ADR 003 does for it |
|---|---|
| STD-31 · mastery with honest uncertainty | The gate is a counting rule on independent first tries only; hinted, modeled and stepped-back attempts never count, and supports never block. Bayesian Knowledge Tracing joins in turn 5 as the uncertainty and ordering layer beside the gate, never instead of it (QUESTIONS Q-STD-1). |
| STD-50s · Art. 12, record-keeping | Every mode decision carries reason codes (`misses_in_a_row:2`, `accuracy_below_support`, `accurate`, `automatic`), so the decision log behind "next and why" writes itself in turn 5. |
| STD-50s · Art. 14, human oversight | The modes move only difficulty, representation and order. Direction (priorities, pauses, the daily target) stays the parent's. |
| STD-44 · no nudge techniques | Speed is never shown, timed or praised; the copy lint and the parent validator hold that line. |
| STD-42 · accessibility (COGA) | Concrete, pictorial, abstract is a support path, not a remedial one: a child with read-aloud or assistive input reaches every state the same way. |

## Settled by Hew (v0.2)
- **The gate is 100%.** The cost named at the time stands: a child repeats a skill until 20 first tries in a row are right, which slows pace on skills that are nearly held. Pace (ADR 002) reports what results.
- **Excellent shows to parents** as the fifth state.
- **Speed without a clock** is the line: duration buckets only, never shown, never praised, never part of the gate; assistive input and "no timers" take it out.

## Changelog
- **v0.1 · 2026-10-10 · Hew's direction:** adopted the high support, high performance framework for math; science and coding recorded for later.
- **v0.2 · 2026-10-10 · Hew's decision:** the gate is 100% (20 of 20, the same after a drop); Excellent is a fifth state shown to parents; speed is measured from duration buckets only.
