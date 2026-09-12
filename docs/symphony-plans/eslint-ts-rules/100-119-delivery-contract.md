# Delivery contract for the 100-119 DAG

This is executable ticket scope for [plan revision 2](../fan-out-plan-100-119-eslint-ts-rules.md), based on `1000lines/eslint:main@4f6a3cc87297ee83a06767d5a492c41cd521abfb`. Read it with the [candidate inventory](100-119-rule-inventory.md) and [reserved continuation](100-119-reserved-candidates.md). The original requirements/design remains read-only; the plan’s Human amendment section supersedes its narrowing/widening and two upstream-owned lane requirements.

## Common contract copied into every generated ticket

- Target `1000lines/eslint`; project `eslint-ts-rules`; Linear team `100`; color `pink`; human lead Jeremy Carroll, GitHub `jeremycarroll`. All task branches and PRs use `main` as base. Branch `symphony/eslint-ts-rules/<actual-issue>/<node-slug>`; PR `[<actual-issue>]: <brief-title>`. Commit summaries are Conventional Commits without scopes, at most 72 characters; rule changes use `feat: support TS syntax in <rule-name>`. Add `Refs eslint/eslint#19173` and the actual model's AI disclosure.
- Each ticket inspects its exact owned files (including existing tests/docs), accepted requirements/design, this plan, selected-base config, root instructions, Makefile and relevant read-only helpers. `source_files` are its owned existing files; shared context is `source_notes`. Do not expand ownership from a source link.
- For each rule, `owned_files` is exactly the rule/test/doc trio enumerated in its inventory entry. One rule per branch/PR. No new options, type definitions, rule registry or recommended-config changes. Readonly type references and parser scope data are allowed; creating a TypeScript Program or using a checker is not. Cancel a type-dependent lane and record the reason through replanning.
- First-wave lanes use the existing interfaces and have `integration_pattern: none`; no TODO, stub, adapter or disabled path is planned. If one is needed, update the plan before implementing it with exact marker/path, seam owner, isolated/composed validation and finalizer responsibility. Shared utilities are not first-wave ownership. A dependency never authorizes committed predecessor work absent from `main`.
- Preserve generated-file conventions. Rule hooks regenerate `packages/js/src/configs/*.js` and `lib/types/rules.d.ts`; doc hooks can update `docs/src/_data/further_reading_links.json`. Verify the diff. Unrelated generation must stay out of a lane; a required shared-file change needs an accepted ownership amendment before publication. Do not hand-edit generated files or change workflow infrastructure to escape checks.
- Open a draft PR once independently reviewable work exists; record the draft reason. If a prerequisite is absent from main, independent investigation or a dependency-note draft may be published; pause dependent implementation/validation, keep the dependency-gated issue Active, and name the prerequisite, missing result, owner and resumption event. Never use another task branch as the PR base.
- Every PR requires verified `symphony,pink` labels and lead assignment. Resolve labels before issue/relation writes, create missing definitions with existing permissions, and use the shared `ensure-pr-labels.mjs` plus actual label readback. No credential or scope expansion. Generated tickets must retain named label failures, unresolved state/assignee/endpoint/SHA failures and the stop condition.
- Each rule records timestamped successes, failures, interventions and review links in its own Codex workpad. Log owners copy these events into the one repository activity log; rule branches never compete to edit it.

## Validation and review

Configured mode is native (omitted); effective mode is native; there is no ticket Docker override. Inspect the selected-base mode again at dispatch. Run local checks, use Docker only for a local environment gap, then require actual current-head GitHub CI. If local checks pass, record `Docker: skipped — passed locally` for that workload. A container fallback must use an explicit command/image digest, mount only the issue workspace, preserve UID/GID, remove task containers and bind any test ports only to localhost.

Executable/argument arrays for a rule lane, from the repository root:

```json
[
	["npm", "install", "--no-package-lock"],
	["npm", "run", "test:cli", "--", "tests/lib/rules/<rule>.js"],
	["node", "Makefile.js", "checkRuleFiles"],
	["node", "Makefile.js", "checkRuleExamples"],
	["node", "Makefile.js", "mocha"]
]
```

Substitute the one owned rule name; do not pass a literal placeholder. Follow repository formatting/lint hooks on the touched files. `checkRuleExamples` covers executable TS documentation; `mocha` covers existing regression/coverage gates. These are planned commands, not claims that future lanes passed. A lane must prove its motivating baseline fails the new assertion without the fix, then passes with it. Cover applicable report locations, options, suggestions/fixes, and unaffected JS cases. Keep parser and dependency updates out of lanes. Record unrelated baseline failures instead of repairing them here; never relabel a known failed assertion as a pass.

For planning/log tickets, use Prettier/markdownlint on owned Markdown, the shared DAG parser for graph changes, and the selected-base configured `node Makefile.js mocha`. Configuration and docs changes also need current-head CI.

For every proof record target SHA, command/environment, criterion, durable artifact or run link, actual result, limitation, next owner. CI needs workflow, event/ref, emitting App, run/attempt and child results; missing, skipped, stale, canceled or pending checks never pass. The selected-base empty config is unconfigured; the full-CI contract below must be copied into each generated ticket and evaluated from current-head runs, never treated as an empty green set. Jeremy's [administrator comment](https://github.com/1000lines/eslint/pull/2#issuecomment-5648910128) confirms no fork required-check configuration; it does not waive mandatory CI.

Normal handoff requires all applicable current-head checks plus a fresh `1000lines-cadence[bot]` review, reviewed SHA/verdict and matching Cadence workpad, closed mandatory feedback, a clean branch and PR ready from draft. Inspect submitted reviews, top-level comments, inline comments/threads and Linear comments before handoff. Apply `mature` to the blocker only at that point. Remove it for request-changes, rejected/stale evidence or a severe regression, not ordinary edits alone. A new head or review-relevant activity requires fresh acceptance evidence. Cadence is advisory to human acceptance and is not a required application CI check. Human merge/acceptance owns Done. At the three-pass review-loop cap, summarize the remaining decision for the lead rather than inventing approval.

Pending/missing CI: Unhappy with `wake:15m`; failed CI/conflict: Active; checks passed but review/input outstanding: Inactive. The server owns CI waiting. Metadata-only fan-out writes use API readbacks, but a published mapping document still requires its own CI. Read current state/head before transitions; preserve concurrent and terminal changes.

## Full CI from the first lane

Jeremy's [late review](https://github.com/1000lines/eslint/pull/3#issuecomment-5649230270) cancels the narrowing optimization. **TS-CI-N and TS-CI-W are removed from the graph; no CI setup PR gates implementation.** Preserve `.symphony.cfg.json` and all workflows. Each rule and artifact owner must require the complete existing CI workloads at its current PR head, and TS-FINAL must verify their applicable equivalents on composed main. This carries the former widening coverage throughout delivery.

At the accepted revision 1 head `4846cc26113e2a720b8f51a31ffe6d875b9ef047`, [CI run 34723170776](https://github.com/1000lines/eslint/actions/runs/34723170776), attempt 1, passed all 18 application children below. Producer is `github-actions`, App `15368`; parent `.github/workflows/ci.yml`, including its existing reusable package-manager call. These are identity/baseline observations, not evidence for a future head:

- `Verify Files`
- `Test (ubuntu-latest, 26.x)`
- `Test (ubuntu-latest, 24.x)`
- `Test (ubuntu-latest, 22.x)`
- `Test (ubuntu-latest, 20.x)`
- `Test (ubuntu-latest, 20.19.0)`
- `Test (windows-latest, lts/*)`
- `Test (macOS-latest, lts/*)`
- `Test (ubuntu-latest, 24.x, --experimental-transform-types)`
- `Browser Test`
- `Test Types`
- `Test pnpm Type Support`
- `Test Package Managers / build-tarball`
- `Test Package Managers / bun-install`
- `Test Package Managers / npm-install`
- `Test Package Managers / yarn-install`
- `Test Package Managers / yarn-v1-install`
- `Test Package Managers / pnpm-install`

Also require the existing **Docs CI** (`.github/workflows/docs-ci.yml`, `Verify Docs Files`, when docs paths trigger it), **Symphony Client CI** (`.github/workflows/symphony-client-ci.yml`, `commands / Client Commands`), **Types Integration CI** (`.github/workflows/types-integration.yml`, all type-integration/package children), **Test Ecosystem Plugins** (`.github/workflows/ecosystem-tests.yml`, every plugin matrix child), and **CodeQL** (`.github/workflows/codeql-analysis.yml`, analysis check). Read each run's child names, emitting App, head SHA and attempt at dispatch and handoff; do not equate an aggregate count with full coverage. The human's timing observation motivates retaining these workflows, not a hardcoded 39-check contract.

Refresh repository branch rules too; this plan cannot waive them. Required workloads must actually succeed; missing, pending, skipped, canceled or stale workload evidence is not passing. A conditional reporting-only job such as `Report Failures`, or review/wakeup cleanup, is not an application workload and may legitimately be skipped; record that distinction rather than counting it as a passed test. Cadence remains a separate current-head review gate. A future renamed/added check requires refreshed provenance, never silently dropping a failure. No workflow or repository configuration mutation is commissioned by this revision.

Every first-wave PR now exposes platform/Node failures before its own acceptance. Attribute failures to the lane, unrelated baseline, or infrastructure with evidence, and carry unresolved defects into TS-REPLAN. TS-FINAL keeps the separate merged-main gate and full composed validation; cancellation requires an accepted amended disposition. A clean early stop does not count as project finalization.

## First-wave node acceptance

Each node owns exactly its inventory trio, uses the common validation/review contract, starts directly from selected main, and has no setup or other-rule prerequisite. Split criteria: locality, validation-surface, independently reviewable rule behavior.

<!-- prettier-ignore -->
| Node | Additional acceptance focus |
| --- | --- |
| TSR-01 | Effect-free `satisfies` is reported; wrapped side effects remain allowed; nested wrappers and existing short-circuit/ternary settings retain meaning. |
| TSR-02 | Report async executor functions/arrows through nested TS `as`, assertion, non-null and `satisfies` wrappers; preserve global Promise detection, shadowed/disabled Promise and non-async valid cases, and the async-token report location. No fix or option changes. |
| TSR-03 | Report discarded constructor expressions through nested TS wrappers at the statement location; keep assigned, returned, compared and otherwise consumed instances valid. Preserve existing JS behavior; do not broaden to unrelated expression contexts or add fixes/options. |
| TSR-04 | Import-equals reads are valid; assignment/update/destructuring writes report at the existing locations. Do not assume a `require` alias has the ES namespace object's readonly-member semantics. |
| TSR-05 | Restricted named TS exports report with existing exact-name/pattern options; allowed names and existing default/type/re-export behavior remain correct. |
| TSR-06 | Leading namespace/module vars are valid, trailing/nested-block vars still report; nested namespaces, exported vars, declarations without runtime statements and JS/static-block cases are covered. |

## TS-LOG: initialize the activity log

Owns `hackathon/1000lines--eslint.md`. No hard prerequisite; can run beside all six rule lanes. Use the [event README](https://github.com/1000lines/symphony-client-template/blob/main/hackathon/README.md) and [log template](https://github.com/1000lines/symphony-client-template/blob/main/hackathon/repo-log-template.md), read at planning time. Record participant, source/working repositories, fork setup, Linear/plan links and intended outcome; then timestamped activity, decisions, blockers/help and end-of-day result. Record the source-file access interruption, supplied attachment, empty required-check discovery, late upstream-ownership exclusions and removal of narrowing, setup/test latency and any new intervention with actual links. Never copy credentials.

Acceptance: the real file follows that layout and includes observed events; its PR passes applicable validation/review. Once merged, hand ownership to TS-REPLAN; rule agents continue logging events in their own workpads. This node is real documentation work, not an agent that stays running to watch the project. Split criteria: proof-of-work-boundary, shared-file ownership.

## TS-REPLAN: first-wave review checkpoint

Owns `docs/symphony-plans/eslint-ts-rules/first-wave-replan.md`, its `.mmd`, and (after TS-LOG merges) `hackathon/1000lines--eslint.md`. Read all six actual PRs/workpads, this plan/inventory, current main and CI outcomes. Trigger when all six lanes have current-head normal review readiness (`mature`) or an explicitly recorded terminal disposition requiring amendment. It does not wait for every merge. The six lane edges are hard review-evidence prerequisites; TS-LOG's edge requires its merge for file ownership.

Collect cancellations requiring type information, multi-rule boundary failures, shared helper needs, missing inventory, full-matrix failures and timing, runner/flake defects, review latency and every human intervention. Record all findings in the activity log even if topology is unchanged. Known reserved helper candidates are input, not permission to modify `ast-utils.js` here.

Use the installed `symphony-replan` skill and existing client planning template. Produce an amended graph and exactly one manifest for that new plan, retaining useful work and identifying replacements/cancellations. Choose additional lanes only from reviewed evidence and available capacity; zero additional lanes is valid. If two selected lanes need a helper, give it one exact owner plus tests and make genuine consumers depend on it. Cancel/replace invalid boundaries rather than quietly stretching a rule branch. Preserve unresolved feedback and make amended ownership, direct relation payloads, current-base validation and finalizer responsibility explicit. This is the planned checkpoint; do not reopen 100-119.

Acceptance: the six outcomes and every finding are accounted for, graph/manifest/payload validation passes, and Jeremy accepts the amended plan. If full-CI defects arrive after this checkpoint is accepted, follow the existing small-change path or create a new replan plus dependent re-fan-out for broader changes; do not claim they were already reviewed.

## TS-REFAN: apply the accepted amended plan

Owns `docs/symphony-plans/eslint-ts-rules/first-wave-refanout.md` for durable mappings/readbacks. It has the hard prerequisite TS-REPLAN accepted and merged. Use the existing fan-out template and shared DAG payload tools; no new local planning infrastructure. Reuse actual issued IDs; update retained tickets, cancel/replace only as accepted, and create only newly selected nodes. Resolve the repository labels before issue/relation writes, then read back every direct relation in both directions. The exact issue-to-UUID map is generated from actual creates, never guessed from C-nn inventory labels.

Crucially, **update TS-FINAL's blockers and completion checklist before activating any additional implementation ticket**. Every retained/new lane, shared-helper cleanup owner and later CI-defect replan must either reach TS-FINAL through accepted hard paths or be explicitly excluded by human decision. This replaces the initial six-lane completion horizon. Do not let the original finalizer run against a stale graph while more work is active. If no additional lanes are selected, record that disposition and still reconcile the existing graph.

Acceptance: accepted plan revision, issue/branch/PR identities, assignments, labels, states and exact relations have API readback; no duplicates or unmapped targets. Mapping-doc PR is validated and merged. Split criteria: external-system-boundary, workflow-boundary.

## TS-FINAL: reconciliation, log and clean shutdown

Owns `docs/symphony-plans/eslint-ts-rules/final-reconciliation.md` and, after TS-REPLAN/TS-REFAN handoff, `hackathon/1000lines--eslint.md`. Hard prerequisites: each surviving first-wave lane merged to main (or an accepted canceled/replaced disposition), and TS-REFAN completed with its updated finalizer relations. The direct lane edges enforce this merge condition separately from the earlier review checkpoint; mature alone is insufficient. Current main and all task PRs named by the latest accepted plan define the project state.

Use the installed finalization and proof skills. Re-read that latest graph and live project issues/PRs. Record each lane's accepted merged SHA or explicit remaining/canceled disposition and resumption owner. Validate the composed main with the full required CI set and the applicable local suite; distinguish previously observed unrelated failures and unresolved lane defects. Audit project-introduced TODOs/stubs/adapters/flags/disabled paths and any markers introduced by replans; remove them only under accepted ownership or record a human decision promoting them to durable behavior. No such seam is present in this initial plan, and unrelated repository TODOs are excluded.

Reconcile outstanding tickets and drafts: no Active ticket without a PR; no draft PR without a recorded reason and owner. Record all requests for human help, source/CI/review failures and full-suite latency, plus end-of-day completed/remaining work and retrieval links. Human acceptance owns Done; closing/canceling work requires the accepted stop/replan disposition and actual API readback.

The brief specifies automation credential revocation at **16:00 local event time**. Verify event date/timezone and live availability before timing any action; do not infer a revocation from the hosted UTC clock. On abrupt review/push/access loss, preserve prepared work and exact head/operation/failure, stop dependent transitions, and hand off to Jeremy. No false Cadence approval, no alternative credentials, and no orphaned drafts. A clean early stop can be recorded before finalization is possible; all surviving required changes must be accepted into main and full CI must pass before the project is called finalized. If permission loss prevents the required reconciliation, record each exact operator action/readback instead of claiming a clean state.

No deploy, release, upstream submission, or upstream acceptance is commissioned. Delivery is accepted fork/main changes and the log/reconciliation artifacts. The finalizer must not invent deploy evidence. Split criteria: proof-of-work-boundary, temporary-seam cleanup, final acceptance.
