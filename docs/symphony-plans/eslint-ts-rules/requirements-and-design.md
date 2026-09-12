# ESLint TypeScript syntax awareness: requirements and design

This is the canonical requirements/design input for [100-119, Plan project](https://linear.app/1000lines/issue/100-119/plan-project-seed-ticket), produced by [100-118](https://linear.app/1000lines/issue/100-118/create-requirements-and-design-doc). It preserves the [confirmed project brief](https://linear.app/1000lines/project/eslint-core-rules-typescript-syntax-awareness-0b1144238612). The planning ticket owns the rule inventory, reviewed dependency graph, and subsequent fan-out; this document does not select implementation lanes or create tickets.

```yaml
project-code: eslint-ts-rules
project-color: pink
repository: 1000lines/eslint
base-branch: main
human-lead: jeremycarroll
```

Source snapshot: 2026-09-12. Repository observations below refer to fork `main` at `deb40ba5e663767b2df5000b1260d10acfae57d8`. Requirements remain subject to later explicit human decisions recorded with their source. GitHub lead `jeremycarroll` resolves to Jeremy Carroll, the assigned Linear lead.

## Goal and expected outcome

Advance [eslint/eslint#19173](https://github.com/eslint/eslint/issues/19173) in the fork by making existing core rules behave correctly when TypeScript syntax changes the meaning of the JavaScript AST patterns they inspect. The intended result is fewer false reports, fewer missed problems, and appropriate handling of TypeScript-only constructs without requiring a type checker. This reduces the need for extension rules to duplicate core behavior; changing or coordinating with typescript-eslint is outside this project.

The enabling AST support already exists. The work is to discover remaining rule-specific gaps and address them independently. The brief identifies `no-redeclare` (#19563) and `no-unused-vars` (#19812) as its two open upstream leads, and describes sixteen previously merged lanes. Its examples include `class-methods-use-this` (#19498), `default-param-last` (#19431), `max-params` (#19557), `no-shadow` (#19565), `no-useless-constructor` (#19535), `no-unused-expressions` (#19564), and `no-empty-function` (#19551). These are discovery context and precedents, not a complete or current inventory for the fork.

The brief estimates roughly forty lanes and 10,000–14,000 changed lines. These are sizing assumptions, not delivery quotas. Work continues while human review capacity exists; completing every candidate is not required. A recorded, clean stopping point is required.

## Scope and boundaries

The project includes a source-derived inventory, a reviewed DAG, independent changes to existing rules, regression tests and corresponding rule documentation, configuration-only CI narrowing and later widening, a replan checkpoint, and an activity log with final reconciliation.

The following exclusions are locked:

- No changes to `.github/workflows/ci.yml`. Required-check selection belongs in `.symphony.cfg.json`.
- No type-checker-dependent rules or behavior. Cancel a lane discovered to need type information; do not retrofit type checking into it.
- No work in or coordination with the typescript-eslint repository. Using the fork's existing TypeScript parser dependency in tests remains part of the established pattern.
- No new lint rules, rule option changes, or documentation restructuring.
- No upstream submission or dependence on upstream acceptance. Any later upstream contribution is a separate human decision; its CLA obligations do not gate fork work.
- No repair of unrelated failures already present on `main`.
- No parallel project-local planning or review infrastructure. Use the shared Symphony tooling and existing review process.

For **100-118 specifically**, the deliverable is this requirements/design artifact and necessary links. Inventory derivation, a fan-out plan or manifest, implementation tickets, the activity-log implementation, CI configuration edits, and rule code are outside this ticket.

## Locked design decisions and implementation contract

### Derive the inventory before fan-out

The planning ticket must inspect `lib/rules/`, using `lib/rules/index.js` to cross-check coverage and the corresponding tests and documentation to establish current behavior. For each candidate, record the affected TypeScript syntax, the current failure or missing behavior, the expected result, evidence that syntax alone suffices, and the owned files. Record a reason for every exclusion, including existing support, no relevant syntax difference, or a requirement for type information. Do not equate an upstream task list or a typescript-eslint wrapper list with the inventory.

Human review of this inventory precedes implementation fan-out. The initial graph should preserve genuine parallelism between per-rule lanes. Introduce a dependency only for a demonstrated prerequisite; scheduling preferences are not hard blockers. The planning ticket must supply the reviewed Mermaid graph, standalone graph, manifest, branch declarations, decisions, and direct blocker relations required by the shared DAG contract. This document deliberately supplies no speculative graph.

### One rule per implementation branch and PR

Each implementation PR owns one `lib/rules/<rule>.js`, its `tests/lib/rules/<rule>.js`, and its `docs/src/rules/<rule>.md`. The brief's shorthand about one rule and one test describes the code boundary, not permission to omit user-facing documentation. Keep JavaScript behavior and existing options stable while correcting the identified TypeScript behavior.

The reference [max-params PR #19557](https://github.com/eslint/eslint/pull/19557) changed those three files plus `lib/types/rules.d.ts` (+260/-7, merged 2025-05-06). Its type-file edit accompanied a new option. Preserve that conditional file-shape precedent, but do not treat it as authorization to add options here: the explicit option-change exclusion controls. A lane that cannot fit that boundary needs a recorded scope decision through replanning before expansion.

Use the existing rule visitor and reporting architecture. Tests already use `RuleTester` with `languageOptions.parser: require("@typescript-eslint/parser")`; add valid and invalid cases covering the motivating syntax and applicable report locations, suggestions, or fixes, while retaining JavaScript regression cases. Use AST and parser-provided syntactic scope information, without a TypeScript Program or type checker.

The inspected sources illustrate established techniques, not proposed lanes:

- `max-params` handles explicit `this` parameters and TypeScript function declarations/types; its current options have evolved beyond the 2025 reference.
- `no-shadow` handles type/value declarations and TypeScript scope definitions.
- `no-useless-constructor` accounts for parameter properties, access modifiers, decorators, and absent constructor bodies.

Rule documentation must describe changed user-visible behavior and contain executable examples. `tools/check-rule-examples.js` already selects the TypeScript parser for TypeScript examples. Follow existing metadata and generation conventions; review generated changes from pre-commit hooks and keep unrelated files out of a lane. If multiple lanes need a shared helper or generated-file ownership overlaps, resolve ownership and prerequisites through the checkpoint rather than silently breaking independence.

### Fork, branch, and review contract

All task branches start from the fork's selected `main` and all task PRs target `1000lines/eslint:main`. No task may commit predecessor work that has not landed on that base. Dependency edges control dispatch, not branch ancestry.

Hosted task names use `symphony/eslint-ts-rules/<ticket-id>/<description>` and PR titles use `[<ticket-id>]: <brief-title>`. These explicit issue/runtime requirements control fork execution. The brief's `ts/<rule-name>` branch convention, including the historical `ts/max-parens` spelling, remains reference context. Preserve Conventional Commit summaries without scopes and at most 72 characters: `feat: support TS syntax in <rule-name>` for implementation and `docs:` for this artifact. The hosted PR-title prefix differs from ESLint's upstream title convention; do not remove the ticket association or change the workflow to reconcile it in a rule lane. Record an actual title-check conflict if one appears.

Use `Refs eslint/eslint#19173` in PR bodies rather than a closing keyword. Every project PR carries `symphony` and `pink`, is assigned to `jeremycarroll`, and begins as a draft with a recorded reason until validation/review closes. Apply the repository's AI disclosure requirement. The fork's explicitly commissioned Symphony execution governs automated rework; any later upstream submission must separately satisfy upstream contribution policies.

Normal handoff requires current-head required CI, a fresh review from the configured Cadence reviewer, closure of mandatory feedback, a clean task branch, and a ready PR. Record the actual reviewed SHA and verdict; provider configuration alone proves no review. Human acceptance owns merge and Done. Loss of review credentials must leave explicit state and an owner, not an invented approval.

## CI narrowing and widening

### Locked policy

During per-rule delivery, require exactly these two application checks, subject to any additional repository branch rules:

1. **Verify Files**, including rule-file consistency and executable documentation examples.
2. **One ordinary `test_on_node` leg on `ubuntu-latest`**, which runs `node Makefile mocha` (as well as the workflow's existing additional test steps).

Implement the selection only in `.symphony.cfg.json` under `ci.requiredChecks`. Keep the workflow intact: every matrix leg continues running with visible results, while the other checks are non-gating during narrowing. This trades early cross-environment gating for shorter per-lane waits and strong rule/example validation; it is deliberately reversible.

The initial plan must contain an explicit **CI widening node** that restores the full required set after the first wave has merged to `main`. It depends on those merged lanes because their cross-version and cross-platform behavior is the evidence being evaluated. Widening must land before project finalization. Failures exposed in merged lanes become defects for the replan process; they are not grounds to revert the narrowing decision retroactively.

### Observed configuration and concrete execution inputs

At the source snapshot, `.symphony.cfg.json` specifies team `100`, setup via `npm install --no-package-lock`, and tests via `node Makefile.js mocha`. It omits `ci.mode`, so the configured and effective mode is **native**. This ticket has no Docker override. Its `ci.requiredChecks` is currently **empty/unconfigured**; neither narrowing nor widening is implemented by this document.

The fork's [CI run 34719070868](https://github.com/1000lines/eslint/actions/runs/34719070868) on the recorded base emitted `Verify Files` and `Test (ubuntu-latest, 24.x)` from `.github/workflows/ci.yml`, with producer `github-actions`, App ID `15368`. The latter is an observed ordinary Ubuntu leg and a suitable concrete selection for the already-authorized narrowing. The implementation should re-observe names and provenance on its current head before accepting this proposed configuration:

```json
{
	"requiredChecks": [
		{
			"name": "Verify Files",
			"workflow": ".github/workflows/ci.yml",
			"appId": 15368
		},
		{
			"name": "Test (ubuntu-latest, 24.x)",
			"workflow": ".github/workflows/ci.yml",
			"appId": 15368
		}
	]
}
```

This fragment belongs under `ci`; retain the other configuration fields. The exact Ubuntu version is an execution input within the approved policy, not another product decision. An empty list never means CI passed.

The observed full CI set comprises `Verify Files`; Ubuntu tests on `26.x`, `24.x`, `22.x`, `20.x`, and `20.19.0`; the additional Node 24 transform-types leg; Windows and macOS LTS legs; `Browser Test`; `Test Types`; `Test pnpm Type Support`; and the `Test Package Managers` build-tarball, bun, npm, yarn, yarn-v1, and pnpm child jobs. Before narrowing lands, record the exact full set and branch requirements so widening can restore it without guessing. The fork also runs Docs CI and Symphony Client CI; establish applicable requirements separately rather than silently counting advisory routing/review checks as application CI.

### Validation requirements

Use the selected-base commands and repository toolchain (currently Node `^20.19.0 || ^22.13.0 || >=24`). For rule work, run targeted tests during iteration and `node Makefile.js mocha` for the accepted suite, plus applicable rule-file, example, formatting, and documentation checks. The brief's `node Makefile mocha` and the config's explicit `.js` spelling address the same repository runner. The full-suite iteration cost is accepted and must be logged as workflow friction; do not build a workaround into a lane.

For native mode, validate locally, use Docker for environment gaps, then require published-head GitHub CI. Passing local checks mean `Docker: skipped — passed locally`. If a later selected-base mode or explicit ticket Docker requirement differs, follow that contract and record configured/effective modes and the override source.

Record command, tested SHA, result, artifact/run link, workflow and emitting App, run attempt and required child jobs, limitation, and next owner. Base-branch CI observations above are source evidence only; they do not validate a future task head. Known failures caused by a lane must be fixed; unrelated baseline failures must be evidenced and logged without claiming a pass. Pending or missing checks use `Unhappy` with `wake:15m`, failed checks require rework in `Active`, and passing CI waits in `Inactive` for review. Empty check configuration needs a concrete configuration handoff before claiming required-CI closure.

## Replan checkpoint and open decision

The plan must position an explicit checkpoint **after the first wave reaches human review**. This is distinct from widening, which waits for first-wave merges. Collect at least:

- Lanes that require type information: cancel them.
- Shared behavior needed by two or more lanes: add a prerequisite helper node and redirect the affected dependencies. The amended graph may gain depth.
- Incorrect lane boundaries where changing one rule forces another to change: cancel and replace with explicitly expanded scope rather than stretching existing lanes.
- CI flakes, fork runner behavior, gaps missed by narrowed checks, later widening failures, and every reusable-workflow intervention.
- Inventory mistakes and rules missed in the first pass.

The checkpoint produces an amended graph through a **replan ticket plus a dependent re-fan-out ticket**. Do not reopen the original planning ticket. Record every finding in the activity log even when it does not change topology. Route later widening findings through the same replan process if they arrive after the initial checkpoint.

**Open decision O1 — first-wave size:** the confirmed brief proposes **six lanes** but leaves the count open. Jeremy Carroll must settle the count when reviewing the inventory/plan, before fan-out fixes the checkpoint's coverage. The decision affects the graph and the amount of review evidence; six is not an accepted completion quota.

The 100-119 seed currently says “six-lane replan decision,” which is stronger than the owning project's explicit Open Decisions section. With no later human resolution in the sources read for 100-118, preserve the brief's open status. The planner must record the eventual decision and align its plan/ticket wording. No answer is needed to finish this requirements artifact.

## Activity log and clean stopping state

The project must produce `hackathon/1000lines--eslint.md` in the working fork using the [symphony-client-template log layout](https://github.com/1000lines/symphony-client-template/blob/main/hackathon/repo-log-template.md): project/participant and source/working repositories, setup path, Linear and plan/PR links, intended outcome, timestamped activity, decisions, blockers, help requested, and an end-of-day result with completed work, remaining work, retrieval links, and follow-up.

Log what worked and every point needing human intervention, including full-suite latency, CI configuration gaps, credentials/review failures, cancellations, and replans. The planning ticket must assign explicit ownership for the log and final reconciliation; do not let each rule lane compete for the same shared log file.

Preserve the brief's execution constraint that review automation credentials are revoked at **16:00 local event time**. The event timezone/date and live credential availability are execution inputs to verify with the lead; the worker's UTC clock is not evidence of revocation. The project must tolerate abrupt loss of Cadence. Close work or record its remaining state, reason, and next owner without abandoning a transition.

Before stopping, reconcile every ticket and PR: no ticket remains Active without a PR, and no PR remains draft without a recorded reason. Record incomplete lanes and resumption actions; do not manufacture completion to meet the event cutoff. Widening must have landed before the project is called finalized, even if delivery stops earlier.

## Acceptance and planning handoff

| ID  | Requirement                                                                     | Evidence and responsible handoff                                                                                                                  |
| --- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| AC1 | Review the source-derived inventory before implementation fan-out.              | 100-119 records candidate rules, affected syntax, expected behavior, inclusion evidence, and exclusion reasons; human inventory review is linked. |
| AC2 | Preserve a genuinely parallel per-rule DAG.                                     | The plan declares disjoint ownership and only justified hard dependencies, using shared Symphony graph/manifest validation.                       |
| AC3 | Each implementation PR covers exactly one rule with tests and user-facing docs. | PR diff contains the rule/test/doc files and motivating TypeScript parser cases; no option change is inferred from historical type-file edits.    |
| AC4 | Each implementation PR passes the narrowed required checks.                     | Configuration is established, both current-head checks have matching workflow/App provenance, and branch requirements are satisfied.              |
| AC5 | Restore the full required set after first-wave merges and before finalization.  | Explicit widening node, merged configuration, and current required-check evidence; resulting defects enter replanning.                            |
| AC6 | Replan after first-wave human review.                                           | Explicit checkpoint, resolved O1 before fan-out, recorded findings, amended graph, replan and dependent re-fan-out artifacts.                     |
| AC7 | Maintain the repository activity log as a deliverable.                          | `hackathon/1000lines--eslint.md` follows the source layout and records successes, defects, and every intervention.                                |
| AC8 | Finish or stop cleanly within available review capacity.                        | Reconciliation identifies every remaining ticket/PR, draft reason, owner, and next action; no Active ticket lacks a PR.                           |
| AC9 | Preserve metadata, scope, and fork/base policy throughout delivery.             | Task branches and PRs use fork `main`, required labels and lead assignment, no unmerged predecessor commits, and no excluded work.                |

100-119 consumes this document alongside the confirmed brief and current repository sources. It should establish inventory and exclusions, resolve O1, declare ownership for CI narrowing/widening, log and reconciliation, then produce the reviewable DAG and downstream handoff. This document is complete when those requirements, locked boundaries, source availability, and open decision are explicit; it does not assert that project acceptance has already been achieved.

## Source availability and provenance

All required sources listed in the confirmed brief were readable for this document. Source access is distinct from passing validation. The brief's GitHub/docs links contained trailing colons; links below use the canonical resource URLs.

| Source                                                                                                                                                                                                                                                                                                | Availability and use on 2026-09-12                                                                                                                                                                                                                                                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Linear project brief](https://linear.app/1000lines/project/eslint-core-rules-typescript-syntax-awareness-0b1144238612), [100-118](https://linear.app/1000lines/issue/100-118/create-requirements-and-design-doc), and [100-119](https://linear.app/1000lines/issue/100-119/plan-project-seed-ticket) | Read through authenticated Linear GraphQL, including issue comments and the direct blocker relation. Project has no attached documents. The project content supplies the confirmed brief; the planning seed's old human-workspace relative paths are not portable artifact links.         |
| [Upstream tracking issue #19173](https://github.com/eslint/eslint/issues/19173)                                                                                                                                                                                                                       | Read primary GitHub issue and reference list. Used for motivation and discovery context, not a substitute for the fork inventory.                                                                                                                                                         |
| [max-params #19557](https://github.com/eslint/eslint/pull/19557)                                                                                                                                                                                                                                      | Read primary PR and GitHub API file list/merge metadata; verified the four-file precedent.                                                                                                                                                                                                |
| [no-shadow #19565](https://github.com/eslint/eslint/pull/19565) and [no-useless-constructor #19535](https://github.com/eslint/eslint/pull/19535)                                                                                                                                                      | Read primary merged PRs, then inspected representative current fork source/tests. Historical examples do not authorize copying unrelated options or stale behavior.                                                                                                                       |
| [ESLint contribution guidance](https://eslint.org/docs/latest/contribute/pull-requests)                                                                                                                                                                                                               | Read primary guidance and local `CONTRIBUTING.md`, `AGENTS.md`, `CLAUDE.md`, and `docs/src/contribute/ai-policy.md`; preserve applicable conventions and the explicit fork execution contract.                                                                                            |
| [Fork source snapshot](https://github.com/1000lines/eslint/tree/deb40ba5e663767b2df5000b1260d10acfae57d8)                                                                                                                                                                                             | Read `README.md`, `SYMPHONY.md`, config, package/toolchain and formatting files, rule index, representative rule/test/doc files, `Makefile.js`, example checker, docs README, PR template, CI workflows, and `.github/symphony/REVIEW.md`. Full per-rule inventory remains planning work. |
| [Fork baseline CI](https://github.com/1000lines/eslint/actions/runs/34719070868)                                                                                                                                                                                                                      | Read successful run/jobs and check-run App provenance on the recorded base. Observed check identities only; no claim of validation for this document's commit.                                                                                                                            |
| [Hackathon README](https://github.com/1000lines/symphony-client-template/blob/main/hackathon/README.md) and [log template](https://github.com/1000lines/symphony-client-template/blob/main/hackathon/repo-log-template.md)                                                                            | Read canonical raw files over HTTPS. Initial browser cache retrieval failed; direct source retrieval succeeded. Used for event context, log layout, human review capacity, and clean shutdown.                                                                                            |
| Shared Symphony guidance                                                                                                                                                                                                                                                                              | Read installed repository, coding, Linear, and proof skills plus proof/review/PR guidance under `SYMPHONY_TOOLING_ROOT`. Planning must reuse `tools/symphony-dag/` there; this ticket creates no DAG or local replacement.                                                                |

No required Google Doc or unavailable primary source remains. If a later required source cannot be read, record its exact access failure and pause dependent work rather than replacing it with an inferred summary.
