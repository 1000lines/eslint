# Rule inventory for 100-119

Snapshot: `1000lines/eslint:main@3d8a6128e70d2f641697d5ebbfd107f02fa1f671`. Part of the [fan-out plan](../fan-out-plan-100-119-eslint-ts-rules.md).

## Coverage and interpretation

The registry and rule-file survey agree on **292 rules**. The initial disposition is **37 candidates**, **93 deprecated rules deferred from delivery**, **21 other rules with existing TypeScript parser tests**, and **141 other rules with no demonstrated gap in this survey**. Every rule appears exactly once here or in the exclusion ledgers: [A–M](100-119-exclusions-a-m.md), [N](100-119-exclusions-n.md), [O–Z](100-119-exclusions-o-z.md).

Inspected the registry, rule metadata, visitor/function structure and TypeScript-specific handling across `lib/rules/`, then corresponding tests/docs and relevant control flow for candidates. Ran a 45-snippet diagnostic survey against all 199 nondeprecated rules, focused follow-ups, and the 37 observations below with the existing TypeScript parser. For the 31 reserved candidates, compared reports with TypeScript-transpiled JavaScript; all showed a diagnostic difference. Transpilation is a syntax probe, not type checking or proof that every diagnostic should match. Structural declarations in the first six require the stated language-specific expectations.

Probe environment: Node `20.20.0`, npm `11.13.0`, `@typescript-eslint/parser` `8.70.0`, TypeScript `6.0.3`. The fork intentionally has no package lock, so record resolved versions again when reproducing.

The survey is bounded: it does not certify complete TypeScript support for any excluded rule. Absence of TypeScript tests alone is not an inclusion reason. A candidate is a concrete gap to review, not a claim that all of its fixes are already designed. Implementation must add valid/invalid RuleTester cases, retain JS behavior, and replan if the boundary or syntax-only premise fails. No TypeScript Program or checker was supplied to the linter.

## First wave and reserved inventory

Only **TSR-01–TSR-06** are nodes commissioned by this initial DAG. **C-01–C-31 are inventory reservations, not task IDs, tickets, branches, or blocker endpoints. Do not create them during 100-120.** The required replan selects further work against review capacity and proposes any shared prerequisite before its dependent re-fan-out. All six first-wave rules have separate rule/test/doc files and need no new shared helper.

For every entry, the source/test/doc links below are also the exact prospective `owned_files`; no shared type, generated index, utility, configuration, or log file is included. For reserved entries this is a proposed boundary, not edit authority. `source_files` is the same trio; `lib/rules/index.js`, shared utilities and the accepted design are read-only context. First-wave implementation has `integration_pattern: none`.

## Reproduce an observation

Run from the repository root after `npm install --no-package-lock`. Substitute a row’s rule, TypeScript snippet and explicitly listed options/globals. Filename selection is necessary; `.ts` files otherwise may be ignored by flat config. This command observes the unchanged rule; it is not an implementation test harness.

```js
const { Linter } = require("./lib/linter");
const parser = require("@typescript-eslint/parser");
const ruleName = "no-unused-expressions";
const messages = new Linter().verify(
	"value satisfies unknown;",
	[
		{
			files: ["**/*.ts"],
			languageOptions: { parser, sourceType: "module" },
			rules: { [ruleName]: "error" },
		},
	],
	{ filename: "probe.ts" },
);
console.log(messages); // Baseline: []; expected after TSR-01: unusedExpression.
```

## Candidates

### TSR-01: no-unused-expressions

**Disposition:** first wave; difficulty `easy`. **Source mechanism:** Checker; TSSatisfiesExpression missing.

Observed TypeScript: `value satisfies unknown;`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unusedExpression missing.

**Expected:** Report effect-free satisfies expressions; preserve permitted calls and existing short-circuit options.

**Syntax-only basis:** Declaration node kinds, flags, parent statement lists and parser-supplied references expose the distinction; no resolved types are required.

Exact files:

- [lib/rules/no-unused-expressions.js](../../../lib/rules/no-unused-expressions.js)
- [tests/lib/rules/no-unused-expressions.js](../../../tests/lib/rules/no-unused-expressions.js)
- [docs/src/rules/no-unused-expressions.md](../../src/rules/no-unused-expressions.md)

### TSR-02: no-redeclare

**Disposition:** first wave; difficulty `hard`. **Source mechanism:** iterateDeclarations; variable.identifiers.

Observed TypeScript: `interface A {x:number} interface A {y:number}`

Settings: default rule options; module source.

Baseline: `redeclared` at 1:34. redeclared false positive.

**Expected:** Allow legal interface, overload and type/value declaration combinations; continue reporting illegal duplicate runtime declarations and var redeclarations.

**Syntax-only basis:** Declaration node kinds, flags, parent statement lists and parser-supplied references expose the distinction; no resolved types are required.

Exact files:

- [lib/rules/no-redeclare.js](../../../lib/rules/no-redeclare.js)
- [tests/lib/rules/no-redeclare.js](../../../tests/lib/rules/no-redeclare.js)
- [docs/src/rules/no-redeclare.md](../../src/rules/no-redeclare.md)

### TSR-03: no-unused-vars

**Disposition:** first wave; difficulty `hard`. **Source mechanism:** collectUnusedVariables; isExported; parameter fixes.

Observed TypeScript: `export type F = (parameter: number) => void;`

Settings: default rule options; module source.

Baseline: `unusedVar` at 1:18. unusedVar false positive on parameter, with removal suggestion.

**Expected:** Distinguish signature-only parameters, overloads, ambient/export declarations, type references and runtime uses using syntactic scope metadata; preserve JS reporting and safe suggestions.

**Syntax-only basis:** Declaration node kinds, flags, parent statement lists and parser-supplied references expose the distinction; no resolved types are required.

Exact files:

- [lib/rules/no-unused-vars.js](../../../lib/rules/no-unused-vars.js)
- [tests/lib/rules/no-unused-vars.js](../../../tests/lib/rules/no-unused-vars.js)
- [docs/src/rules/no-unused-vars.md](../../src/rules/no-unused-vars.md)

### TSR-04: no-import-assign

**Disposition:** first wave; difficulty `hard`. **Source mechanism:** ImportDeclaration visitor only.

Observed TypeScript: `import fs = require("fs"); fs = other;`

Settings: default rule options; module source.

Baseline: **no diagnostics**. readonly missing.

**Expected:** Check direct writes to import-equals bindings, with valid read cases; distinguish external require aliases from ES namespace imports before applying member-write checks.

**Syntax-only basis:** Declaration node kinds, flags, parent statement lists and parser-supplied references expose the distinction; no resolved types are required.

Exact files:

- [lib/rules/no-import-assign.js](../../../lib/rules/no-import-assign.js)
- [tests/lib/rules/no-import-assign.js](../../../tests/lib/rules/no-import-assign.js)
- [docs/src/rules/no-import-assign.md](../../src/rules/no-import-assign.md)

### TSR-05: no-restricted-exports

**Disposition:** first wave; difficulty `easy`. **Source mechanism:** ExportNamedDeclaration declaration whitelist.

Observed TypeScript: `export interface forbidden {}`

Settings: options `[{"restrictedNamedExports":["forbidden"]}]`.

Baseline: **no diagnostics**. restrictedNamed missing with restrictedNamedExports=[forbidden].

**Expected:** Apply existing named-export restrictions to TS interfaces, aliases, enums, namespaces and declared functions; preserve default/export-type/re-export option behavior.

**Syntax-only basis:** Declaration node kinds, flags, parent statement lists and parser-supplied references expose the distinction; no resolved types are required.

Exact files:

- [lib/rules/no-restricted-exports.js](../../../lib/rules/no-restricted-exports.js)
- [tests/lib/rules/no-restricted-exports.js](../../../tests/lib/rules/no-restricted-exports.js)
- [docs/src/rules/no-restricted-exports.md](../../src/rules/no-restricted-exports.md)

### TSR-06: vars-on-top

**Disposition:** first wave; difficulty `easy`. **Source mechanism:** blockScopeVarCheck excludes TSModuleBlock.

Observed TypeScript: `namespace N { var a; use(a); }`

Settings: default rule options; module source.

Baseline: `top` at 1:15. top false positive.

**Expected:** Recognize TS namespace/module statement lists as their own var scope; still report declarations following executable statements and improper nested-block declarations.

**Syntax-only basis:** Declaration node kinds, flags, parent statement lists and parser-supplied references expose the distinction; no resolved types are required.

Exact files:

- [lib/rules/vars-on-top.js](../../../lib/rules/vars-on-top.js)
- [tests/lib/rules/vars-on-top.js](../../../tests/lib/rules/vars-on-top.js)
- [docs/src/rules/vars-on-top.md](../../src/rules/vars-on-top.md)

### C-01: no-throw-literal

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** astUtils.couldBeError.

Observed TypeScript: `throw (new Error() as Error);`

Settings: default rule options; module source.

Baseline: `object` at 1:1. object false positive.

**Expected:** Retain the existing syntax-only couldBeError behavior through erased wrappers; do not infer thrown value types.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-throw-literal.js](../../../lib/rules/no-throw-literal.js)
- [tests/lib/rules/no-throw-literal.js](../../../tests/lib/rules/no-throw-literal.js)
- [docs/src/rules/no-throw-literal.md](../../src/rules/no-throw-literal.md)

### C-02: prefer-promise-reject-errors

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** checkRejectCall; astUtils.couldBeError.

Observed TypeScript: `Promise.reject(new Error() as Error);`

Settings: default rule options; module source.

Baseline: `rejectAnError` at 1:1. rejectAnError false positive.

**Expected:** Apply existing syntactic error-expression checks through wrappers to Promise.reject and executor reject calls.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/prefer-promise-reject-errors.js](../../../lib/rules/prefer-promise-reject-errors.js)
- [tests/lib/rules/prefer-promise-reject-errors.js](../../../tests/lib/rules/prefer-promise-reject-errors.js)
- [docs/src/rules/prefer-promise-reject-errors.md](../../src/rules/prefer-promise-reject-errors.md)

### C-03: no-unsafe-optional-chaining

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** checkUndefinedShortCircuit.

Observed TypeScript: `(obj?.foo as any)();`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unsafeOptionalChain missing.

**Expected:** Trace optional short-circuiting through erased wrappers, including nested logical/conditional paths and current arithmetic option.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-unsafe-optional-chaining.js](../../../lib/rules/no-unsafe-optional-chaining.js)
- [tests/lib/rules/no-unsafe-optional-chaining.js](../../../tests/lib/rules/no-unsafe-optional-chaining.js)
- [docs/src/rules/no-unsafe-optional-chaining.md](../../src/rules/no-unsafe-optional-chaining.md)

### C-04: no-constant-condition

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** reportIfConstant; astUtils.isConstant.

Observed TypeScript: `if (true as boolean) run();`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unexpected missing.

**Expected:** Evaluate literal syntactic conditions through wrappers without deriving variable types.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-constant-condition.js](../../../lib/rules/no-constant-condition.js)
- [tests/lib/rules/no-constant-condition.js](../../../tests/lib/rules/no-constant-condition.js)
- [docs/src/rules/no-constant-condition.md](../../src/rules/no-constant-condition.md)

### C-05: no-constant-binary-expression

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** hasConstantNullishness; static boolean helpers.

Observed TypeScript: `(false as boolean) && x;`

Settings: default rule options; module source.

Baseline: **no diagnostics**. constantShortCircuit missing.

**Expected:** Preserve existing constant/nullish/boolean classifications after transparent syntactic wrappers.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-constant-binary-expression.js](../../../lib/rules/no-constant-binary-expression.js)
- [tests/lib/rules/no-constant-binary-expression.js](../../../tests/lib/rules/no-constant-binary-expression.js)
- [docs/src/rules/no-constant-binary-expression.md](../../src/rules/no-constant-binary-expression.md)

### C-06: no-unsafe-negation

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** isNegation; BinaryExpression.

Observed TypeScript: `(!foo as any) in bar;`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unexpected missing.

**Expected:** Find negation beneath wrappers and keep fixes parenthesized and type syntax intact.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-unsafe-negation.js](../../../lib/rules/no-unsafe-negation.js)
- [tests/lib/rules/no-unsafe-negation.js](../../../tests/lib/rules/no-unsafe-negation.js)
- [docs/src/rules/no-unsafe-negation.md](../../src/rules/no-unsafe-negation.md)

### C-07: no-self-assign

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** AssignmentExpression; destructuring/member comparisons.

Observed TypeScript: `foo = (foo as any);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. selfAssignment missing.

**Expected:** Compare wrapped runtime operands while preserving destructuring, member and side-effect exclusions.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-self-assign.js](../../../lib/rules/no-self-assign.js)
- [tests/lib/rules/no-self-assign.js](../../../tests/lib/rules/no-self-assign.js)
- [docs/src/rules/no-self-assign.md](../../src/rules/no-self-assign.md)

### C-08: no-self-compare

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** BinaryExpression; token equality.

Observed TypeScript: `(foo as any) === foo;`

Settings: default rule options; module source.

Baseline: **no diagnostics**. comparingToSelf missing.

**Expected:** Compare erased operands under the existing same-reference restrictions.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-self-compare.js](../../../lib/rules/no-self-compare.js)
- [tests/lib/rules/no-self-compare.js](../../../tests/lib/rules/no-self-compare.js)
- [docs/src/rules/no-self-compare.md](../../src/rules/no-self-compare.md)

### C-09: array-callback-return

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** getArrayMethodName.

Observed TypeScript: `[1].map((function(x){x;}) as any);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. expectedInside missing.

**Expected:** Recognize wrapped callbacks and preserve code-path analysis and method-specific return requirements.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/array-callback-return.js](../../../lib/rules/array-callback-return.js)
- [tests/lib/rules/array-callback-return.js](../../../tests/lib/rules/array-callback-return.js)
- [docs/src/rules/array-callback-return.md](../../src/rules/array-callback-return.md)

### C-10: prefer-arrow-callback

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** callback parent traversal.

Observed TypeScript: `array.map((function(x){return x;}) as any);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. preferArrowCallback missing.

**Expected:** Recognize wrapped callbacks while retaining explicit this parameters and this/arguments/generator exceptions.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/prefer-arrow-callback.js](../../../lib/rules/prefer-arrow-callback.js)
- [tests/lib/rules/prefer-arrow-callback.js](../../../tests/lib/rules/prefer-arrow-callback.js)
- [docs/src/rules/prefer-arrow-callback.md](../../src/rules/prefer-arrow-callback.md)

### C-11: no-async-promise-executor

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** direct arguments.0.async selector.

Observed TypeScript: `new Promise((async function(resolve){}) as any);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. async missing.

**Expected:** Inspect wrapped executor functions; preserve the current Promise identification policy.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-async-promise-executor.js](../../../lib/rules/no-async-promise-executor.js)
- [tests/lib/rules/no-async-promise-executor.js](../../../tests/lib/rules/no-async-promise-executor.js)
- [docs/src/rules/no-async-promise-executor.md](../../src/rules/no-async-promise-executor.md)

### C-12: no-extra-boolean-cast

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** isInBooleanContext; isInFlaggedContext.

Observed TypeScript: `if ((!!value) as boolean) run();`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unexpectedNegation missing.

**Expected:** Recognize boolean context through wrappers without widening existing logical-context options or unsafe fixes.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-extra-boolean-cast.js](../../../lib/rules/no-extra-boolean-cast.js)
- [tests/lib/rules/no-extra-boolean-cast.js](../../../tests/lib/rules/no-extra-boolean-cast.js)
- [docs/src/rules/no-extra-boolean-cast.md](../../src/rules/no-extra-boolean-cast.md)

### C-13: prefer-regex-literals

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** isStringLiteral; isStaticString.

Observed TypeScript: `RegExp("foo" as string);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unexpectedRegExp missing.

**Expected:** Find syntactically static strings through wrappers; preserve flags, escapes and safe-fix checks.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/prefer-regex-literals.js](../../../lib/rules/prefer-regex-literals.js)
- [tests/lib/rules/prefer-regex-literals.js](../../../tests/lib/rules/prefer-regex-literals.js)
- [docs/src/rules/prefer-regex-literals.md](../../src/rules/prefer-regex-literals.md)

### C-14: prefer-numeric-literals

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** CallExpression argument checks.

Observed TypeScript: `parseInt("111" as string, 2);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. useLiteral missing.

**Expected:** Recognize literal input/radix through wrappers and retain safe numeric replacement constraints.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/prefer-numeric-literals.js](../../../lib/rules/prefer-numeric-literals.js)
- [tests/lib/rules/prefer-numeric-literals.js](../../../tests/lib/rules/prefer-numeric-literals.js)
- [docs/src/rules/prefer-numeric-literals.md](../../src/rules/prefer-numeric-literals.md)

### C-15: no-new

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** ExpressionStatement > NewExpression.

Observed TypeScript: `new Foo() as Foo;`

Settings: default rule options; module source.

Baseline: **no diagnostics**. noNewStatement missing.

**Expected:** Recognize a discarded new expression under wrappers; keep assigned/returned instances valid.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-new.js](../../../lib/rules/no-new.js)
- [tests/lib/rules/no-new.js](../../../tests/lib/rules/no-new.js)
- [docs/src/rules/no-new.md](../../src/rules/no-new.md)

Reserved candidates continue in [C-16–C-31 and shared-work findings](100-119-reserved-candidates.md).
