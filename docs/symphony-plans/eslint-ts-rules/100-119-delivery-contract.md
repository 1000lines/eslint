# Delivery contract for the 100-119 DAG

This is executable ticket scope for the [initial plan](../fan-out-plan-100-119-eslint-ts-rules.md), at `1000lines/eslint:main@3d8a6128e70d2f641697d5ebbfd107f02fa1f671`. Read it with the [candidate inventory](100-119-rule-inventory.md) and [reserved continuation](100-119-reserved-candidates.md). The original requirements/design remains read-only.

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

For planning/configuration/log tickets, use Prettier/markdownlint on owned Markdown, the shared DAG parser for graph changes, the config validation helper for `.symphony.cfg.json`, and the selected-base configured `node Makefile.js mocha`. Configuration and docs changes also need current-head CI.

For every proof record target SHA, command/environment, criterion, durable artifact or run link, actual result, limitation, next owner. CI needs workflow, event/ref, emitting App, run/attempt and child results; missing, skipped, stale, canceled or pending checks never pass. Until narrowing lands, the empty config is unconfigured, and this plan proposes evaluating the existing application CI rather than treating an empty set as green. Jeremy's [administrator comment](https://github.com/1000lines/eslint/pull/2#issuecomment-5648910128) confirms no fork required-check configuration; it does not waive mandatory CI.

Normal handoff requires all applicable current-head checks plus a fresh `1000lines-cadence[bot]` review, reviewed SHA/verdict and matching Cadence workpad, closed mandatory feedback, a clean branch and PR ready from draft. Inspect submitted reviews, top-level comments, inline comments/threads and Linear comments before handoff. Apply `mature` to the blocker only at that point. Remove it for request-changes, rejected/stale evidence or a severe regression, not ordinary edits alone. A new head or review-relevant activity requires fresh acceptance evidence. Cadence is advisory to human acceptance and is not a required application CI check. Human merge/acceptance owns Done. At the three-pass review-loop cap, summarize the remaining decision for the lead rather than inventing approval.

Pending/missing CI: Unhappy with `wake:15m`; failed CI/conflict: Active; checks passed but review/input outstanding: Inactive. The server owns CI waiting. Metadata-only fan-out writes use API readbacks, but a published mapping document still requires its own CI. Read current state/head before transitions; preserve concurrent and terminal changes.

## CI ownership: TS-CI-N and TS-CI-W

Both nodes own **only `.symphony.cfg.json`**. Their overlap is serial: TS-CI-N merges before the six lanes, then TS-CI-W changes the same field after those lanes merge. Preserve all other config and every workflow, especially `.github/workflows/ci.yml`. `source_files`: `.symphony.cfg.json`; source notes: `.github/workflows/ci.yml`, selected-base actual jobs/checks, configuration reference. Split criteria: workflow-boundary, validation-surface.

TS-CI-N installs precisely these entries under `ci.requiredChecks`, after refreshing their identities on a real fork run:

```json
[
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
```

The ordinary Ubuntu 24 job is distinct from the transform-types leg. Baseline [CI run 34719070868](https://github.com/1000lines/eslint/actions/runs/34719070868), attempt 1 at `deb40ba5e663767b2df5000b1260d10acfae57d8`, emitted the following 18 successful children. This is observed identity evidence, not validation of future commits. Producer is `github-actions`, App `15368`; the parent workflow is `.github/workflows/ci.yml`, including its existing reusable package-manager call.

TS-CI-W restores **all 18 application child checks**, with those workflow/App fields, refreshing names if the upstream workflow has changed:

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

“Restore” means restore full-matrix gating as required by the brief, not restore the snapshot's empty array. Refresh branch rules too; configured selection cannot waive new human-imposed branch requirements. Narrowing leaves the full workflow running and visible. Validate configuration with the installed repository helper, then prove selected checks on the configuration PR's actual head. Widening needs the full intended set passing on its head even though main still contains the narrowed config during its PR. Record merge SHA/readback before finalization. If the workflow introduces renamed/additional children, amend the concrete set with provenance; never silently drop failures or bind a similarly named check from another producer.

TS-CI-W requires the six surviving first-wave changes merged to main, not merely mature. If a lane is canceled, TS-REPLAN must amend the accepted wave/missing-result disposition before widening proceeds. A clean early stop before those merges is permitted but is not project finalization. Attribute full-matrix failures to already merged lanes or unrelated baseline/infrastructure; feed defects into TS-REPLAN or a later two-ticket replan if the checkpoint already closed. Do not silently undo the approved narrowing decision or alter CI workflow files.

## First-wave node acceptance

Each node owns exactly its inventory trio, uses the common validation/review contract, depends on TS-CI-N **merged to main**, and has no dependency on another rule. Split criteria: locality, validation-surface, independently reviewable rule behavior.

<!-- prettier-ignore -->
| Node | Additional acceptance focus |
| --- | --- |
| TSR-01 | Effect-free `satisfies` is reported; wrapped side effects remain allowed; nested wrappers and existing short-circuit/ternary settings retain meaning. |
| TSR-02 | Valid declaration-merging matrix (interface/interface, value/type, permitted namespace/class/function combinations, overload signatures) does not report; invalid duplicates still report in each relevant TS scope. No new ignore-merging option. |
| TSR-03 | Signature/overload parameters no longer report or receive destructive suggestions; cover ambient declarations, exported types, namespace/enum/type-parameter definitions, value-vs-type references and retained JS option behavior. Specify each syntactic exemption; do not mark every TS scope used. Disable only demonstrably unsafe existing suggestions for unsupported syntax. |
| TSR-04 | Import-equals reads are valid; assignment/update/destructuring writes report at the existing locations. Do not assume a `require` alias has the ES namespace object's readonly-member semantics. |
| TSR-05 | Restricted named TS exports report with existing exact-name/pattern options; allowed names and existing default/type/re-export behavior remain correct. |
| TSR-06 | Leading namespace/module vars are valid, trailing/nested-block vars still report; nested namespaces, exported vars, declarations without runtime statements and JS/static-block cases are covered. |

## TS-LOG: initialize the activity log

Owns `hackathon/1000lines--eslint.md`. No hard prerequisite; can run beside TS-CI-N. Use the [event README](https://github.com/1000lines/symphony-client-template/blob/main/hackathon/README.md) and [log template](https://github.com/1000lines/symphony-client-template/blob/main/hackathon/repo-log-template.md), read at planning time. Record participant, source/working repositories, fork setup, Linear/plan links and intended outcome; then timestamped activity, decisions, blockers/help and end-of-day result. Record the source-file access interruption, supplied attachment, empty required-check discovery, setup/test latency and any new intervention with actual links. Never copy credentials.

Acceptance: the real file follows that layout and includes observed events; its PR passes applicable validation/review. Once merged, hand ownership to TS-REPLAN; rule agents continue logging events in their own workpads. This node is real documentation work, not an agent that stays running to watch the project. Split criteria: proof-of-work-boundary, shared-file ownership.

## TS-REPLAN: first-wave review checkpoint

Owns `docs/symphony-plans/eslint-ts-rules/first-wave-replan.md`, its `.mmd`, and (after TS-LOG merges) `hackathon/1000lines--eslint.md`. Read all six actual PRs/workpads, this plan/inventory, current main and CI outcomes. Trigger when all six lanes have current-head normal review readiness (`mature`) or an explicitly recorded terminal disposition requiring amendment. It does not wait for every merge. The six lane edges are hard review-evidence prerequisites; TS-LOG's edge requires its merge for file ownership.

Collect cancellations requiring type information, multi-rule boundary failures, shared helper needs, missing inventory, narrowed-check misses, full-matrix signals, runner/flake defects, review latency and every human intervention. Record all findings in the activity log even if topology is unchanged. Known reserved helper candidates are input, not permission to modify `ast-utils.js` here.

Use the installed `symphony-replan` skill and existing client planning template. Produce an amended graph and exactly one manifest for that new plan, retaining useful work and identifying replacements/cancellations. Choose additional lanes only from reviewed evidence and available capacity; zero additional lanes is valid. If two selected lanes need a helper, give it one exact owner plus tests and make genuine consumers depend on it. Cancel/replace invalid boundaries rather than quietly stretching a rule branch. Preserve unresolved feedback and make amended ownership, direct relation payloads, current-base validation and finalizer responsibility explicit. This is the planned checkpoint; do not reopen 100-119.

Acceptance: the six outcomes and every finding are accounted for, graph/manifest/payload validation passes, and Jeremy accepts the amended plan. If widening defects arrive after this checkpoint is accepted, follow the existing small-change path or create a new replan plus dependent re-fan-out for broader changes; do not claim they were already reviewed.

## TS-REFAN: apply the accepted amended plan

Owns `docs/symphony-plans/eslint-ts-rules/first-wave-refanout.md` for durable mappings/readbacks. It has the hard prerequisite TS-REPLAN accepted and merged. Use the existing fan-out template and shared DAG payload tools; no new local planning infrastructure. Reuse actual issued IDs; update retained tickets, cancel/replace only as accepted, and create only newly selected nodes. Resolve the repository labels before issue/relation writes, then read back every direct relation in both directions. The exact issue-to-UUID map is generated from actual creates, never guessed from C-nn inventory labels.

Crucially, **update TS-FINAL's blockers and completion checklist before activating any additional implementation ticket**. Every retained/new lane, shared-helper cleanup owner and later widening-defect replan must either reach TS-FINAL through accepted hard paths or be explicitly excluded by human decision. This replaces the initial six-lane completion horizon. Do not let the original finalizer run against a stale graph while more work is active. If no additional lanes are selected, record that disposition and still reconcile the existing graph.

Acceptance: accepted plan revision, issue/branch/PR identities, assignments, labels, states and exact relations have API readback; no duplicates or unmapped targets. Mapping-doc PR is validated and merged. Split criteria: external-system-boundary, workflow-boundary.

## TS-FINAL: reconciliation, log and clean shutdown

Owns `docs/symphony-plans/eslint-ts-rules/final-reconciliation.md` and, after TS-REPLAN/TS-REFAN handoff, `hackathon/1000lines--eslint.md`. Hard prerequisites: TS-CI-W merged with full-set evidence, and TS-REFAN completed with its updated finalizer relations. Current main and all task PRs named by the latest accepted plan define the project state.

Use the installed finalization and proof skills. Re-read that latest graph and live project issues/PRs. Record each lane's accepted merged SHA or explicit remaining/canceled disposition and resumption owner. Validate the composed main with the full required CI set and the applicable local suite; distinguish previously observed unrelated failures and unresolved lane defects. Audit project-introduced TODOs/stubs/adapters/flags/disabled paths and any markers introduced by replans; remove them only under accepted ownership or record a human decision promoting them to durable behavior. No such seam is present in this initial plan, and unrelated repository TODOs are excluded.

Reconcile outstanding tickets and drafts: no Active ticket without a PR; no draft PR without a recorded reason and owner. Record all requests for human help, source/CI/review failures and full-suite latency, plus end-of-day completed/remaining work and retrieval links. Human acceptance owns Done; closing/canceling work requires the accepted stop/replan disposition and actual API readback.

The brief specifies automation credential revocation at **16:00 local event time**. Verify event date/timezone and live availability before timing any action; do not infer a revocation from the hosted UTC clock. On abrupt review/push/access loss, preserve prepared work and exact head/operation/failure, stop dependent transitions, and hand off to Jeremy. No false Cadence approval, no alternative credentials, and no orphaned drafts. A clean early stop can be recorded before finalization is possible; full CI widening still must land before the project is called finalized. If permission loss prevents the required reconciliation, record each exact operator action/readback instead of claiming a clean state.

No deploy, release, upstream submission, or upstream acceptance is commissioned. Delivery is accepted fork/main changes and the log/reconciliation artifacts. The finalizer must not invent deploy evidence. Split criteria: proof-of-work-boundary, temporary-seam cleanup, final acceptance.
