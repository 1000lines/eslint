# Reserved candidates C-16–C-31 for 100-119

Part of the [rule inventory](100-119-rule-inventory.md); same selected-base snapshot, reproduction method, exact-file policy and deferred commissioning apply.

## Candidates

### C-16: no-console

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** isMemberAccessExceptAllowed.

Observed TypeScript: `(console as any).log("x");`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unexpected missing.

**Expected:** Follow wrapper parents from the global console reference; preserve shadowed bindings and allowed methods.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-console.js](../../../lib/rules/no-console.js)
- [tests/lib/rules/no-console.js](../../../tests/lib/rules/no-console.js)
- [docs/src/rules/no-console.md](../../src/rules/no-console.md)

### C-17: no-promise-executor-return

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** executor parent checks.

Observed TypeScript: `new Promise((function(resolve){ return 1; })!);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. returnsValue missing.

**Expected:** Recognize wrapped executor functions and preserve code-path and allowVoid behavior.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-promise-executor-return.js](../../../lib/rules/no-promise-executor-return.js)
- [tests/lib/rules/no-promise-executor-return.js](../../../tests/lib/rules/no-promise-executor-return.js)
- [docs/src/rules/no-promise-executor-return.md](../../src/rules/no-promise-executor-return.md)

### C-18: no-underscore-dangle

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** checkForDanglingUnderscoreInFunctionParameters.

Observed TypeScript: `class C {constructor(public _value: number){}}`

Settings: options `[{"allowFunctionParams":false}]`.

Baseline: **no diagnostics**. unexpectedUnderscore missing with allowFunctionParams=false.

**Expected:** Apply existing parameter-name restrictions to TS parameter properties, retaining class-field options and allowed names.

**Syntax-only basis:** Declaration node kinds, flags, parent statement lists and parser-supplied references expose the distinction; no resolved types are required.

Exact files:

- [lib/rules/no-underscore-dangle.js](../../../lib/rules/no-underscore-dangle.js)
- [tests/lib/rules/no-underscore-dangle.js](../../../tests/lib/rules/no-underscore-dangle.js)
- [docs/src/rules/no-underscore-dangle.md](../../src/rules/no-underscore-dangle.md)

### C-19: no-implicit-globals

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** Program scope definitions.

Observed TypeScript: `declare var value: number;`

Settings: sourceType `script`.

Baseline: `globalNonLexicalBinding` at 1:13. global variable report on erased declaration (sourceType=script).

**Expected:** Exclude ambient declarations with no runtime global creation; retain reports on ordinary script globals.

**Syntax-only basis:** Declaration node kinds, flags, parent statement lists and parser-supplied references expose the distinction; no resolved types are required.

Exact files:

- [lib/rules/no-implicit-globals.js](../../../lib/rules/no-implicit-globals.js)
- [tests/lib/rules/no-implicit-globals.js](../../../tests/lib/rules/no-implicit-globals.js)
- [docs/src/rules/no-implicit-globals.md](../../src/rules/no-implicit-globals.md)

### C-20: no-negated-condition

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** isNegatedUnaryExpression.

Observed TypeScript: `if ((!foo) as boolean) first(); else second();`

Settings: default rule options; module source.

Baseline: **no diagnostics**. negatedCondition missing.

**Expected:** Inspect syntactic negation beneath wrappers using existing if/else and ternary policy.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-negated-condition.js](../../../lib/rules/no-negated-condition.js)
- [tests/lib/rules/no-negated-condition.js](../../../tests/lib/rules/no-negated-condition.js)
- [docs/src/rules/no-negated-condition.md](../../src/rules/no-negated-condition.md)

### C-21: no-compare-neg-zero

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** isNegZero.

Observed TypeScript: `value === (-0 as number);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unexpected missing.

**Expected:** Detect wrapped negative zero and retain suggestion semantics and parentheses.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-compare-neg-zero.js](../../../lib/rules/no-compare-neg-zero.js)
- [tests/lib/rules/no-compare-neg-zero.js](../../../tests/lib/rules/no-compare-neg-zero.js)
- [docs/src/rules/no-compare-neg-zero.md](../../src/rules/no-compare-neg-zero.md)

### C-22: no-unneeded-ternary

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** isBooleanLiteral.

Observed TypeScript: `const x = foo ? (true as boolean) : false;`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unnecessaryConditionalExpression missing.

**Expected:** Recognize wrapped literal arms while preserving value semantics and safe fix text.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-unneeded-ternary.js](../../../lib/rules/no-unneeded-ternary.js)
- [tests/lib/rules/no-unneeded-ternary.js](../../../tests/lib/rules/no-unneeded-ternary.js)
- [docs/src/rules/no-unneeded-ternary.md](../../src/rules/no-unneeded-ternary.md)

### C-23: preserve-caught-error

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** isThrowingNewError.

Observed TypeScript: `try { f(); } catch (e) { throw (new Error("message") as Error); }`

Settings: default rule options; module source.

Baseline: **no diagnostics**. missing-cause diagnostic missing.

**Expected:** Follow wrapped new-error expressions without treating assertions as evidence of error type; retain shadowing and cause handling.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/preserve-caught-error.js](../../../lib/rules/preserve-caught-error.js)
- [tests/lib/rules/preserve-caught-error.js](../../../tests/lib/rules/preserve-caught-error.js)
- [docs/src/rules/preserve-caught-error.md](../../src/rules/preserve-caught-error.md)

### C-24: no-restricted-properties

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** MemberExpression object.type check.

Observed TypeScript: `(obj as any).forbidden;`

Settings: options `[{"object":"obj","property":"forbidden"}]`.

Baseline: **no diagnostics**. restricted property diagnostic missing with object=obj/property=forbidden.

**Expected:** Apply configured object/property checks through wrappers without changing restriction options.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-restricted-properties.js](../../../lib/rules/no-restricted-properties.js)
- [tests/lib/rules/no-restricted-properties.js](../../../tests/lib/rules/no-restricted-properties.js)
- [docs/src/rules/no-restricted-properties.md](../../src/rules/no-restricted-properties.md)

### C-25: prefer-destructuring

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** performCheck; checkVariableDeclarator.

Observed TypeScript: `const foo = (object.foo as number);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. preferDestructuring missing.

**Expected:** Recognize wrapped member initialization; preserve annotations/assertions in any offered fix, or suppress unsafe fixes.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/prefer-destructuring.js](../../../lib/rules/prefer-destructuring.js)
- [tests/lib/rules/prefer-destructuring.js](../../../tests/lib/rules/prefer-destructuring.js)
- [docs/src/rules/prefer-destructuring.md](../../src/rules/prefer-destructuring.md)

### C-26: no-useless-concat

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** getLeft; getRight; isConcatenation.

Observed TypeScript: `const x = ("a" as string) + "b";`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unexpectedConcat missing.

**Expected:** Find literal-only runtime concatenation through wrappers; keep genuinely dynamic operands valid.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-useless-concat.js](../../../lib/rules/no-useless-concat.js)
- [tests/lib/rules/no-useless-concat.js](../../../tests/lib/rules/no-useless-concat.js)
- [docs/src/rules/no-useless-concat.md](../../src/rules/no-useless-concat.md)

### C-27: no-magic-numbers

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** radix parent/context checks.

Observed TypeScript: `parseInt("123", 10 as number);`

Settings: default rule options; module source.

Baseline: `noMagic` at 1:17. noMagic false positive.

**Expected:** Preserve existing contextual numeric exemptions through erased wrappers, including radix, and keep existing TS options unchanged.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-magic-numbers.js](../../../lib/rules/no-magic-numbers.js)
- [tests/lib/rules/no-magic-numbers.js](../../../tests/lib/rules/no-magic-numbers.js)
- [docs/src/rules/no-magic-numbers.md](../../src/rules/no-magic-numbers.md)

### C-28: no-invalid-regexp

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** constructor static argument inspection.

Observed TypeScript: `RegExp("[" as string);`

Settings: default rule options; module source.

Baseline: **no diagnostics**. invalid-regexp diagnostic missing.

**Expected:** Validate syntactically known regex strings beneath wrappers with existing ecmaVersion/flag options.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-invalid-regexp.js](../../../lib/rules/no-invalid-regexp.js)
- [tests/lib/rules/no-invalid-regexp.js](../../../tests/lib/rules/no-invalid-regexp.js)
- [docs/src/rules/no-invalid-regexp.md](../../src/rules/no-invalid-regexp.md)

### C-29: no-implied-eval

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** CallExpression callee matching.

Observed TypeScript: `(setTimeout as any)("foo()", 1);`

Settings: globals `{"setTimeout":"readonly"}`.

Baseline: **no diagnostics**. impliedEval missing with setTimeout configured as a readonly global.

**Expected:** Recognize wrapped timer callees while retaining the existing static-string evaluator and shadowed-timer exceptions.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-implied-eval.js](../../../lib/rules/no-implied-eval.js)
- [tests/lib/rules/no-implied-eval.js](../../../tests/lib/rules/no-implied-eval.js)
- [docs/src/rules/no-implied-eval.md](../../src/rules/no-implied-eval.md)

### C-30: no-dupe-else-if

**Disposition:** reserved for replan; difficulty `hard`. **Source mechanism:** equal; splitByLogicalOperator.

Observed TypeScript: `if (foo) {} else if (foo as boolean) {}`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unexpected missing.

**Expected:** Compare equivalent erased conditions using current subset logic, without type-based equivalence.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-dupe-else-if.js](../../../lib/rules/no-dupe-else-if.js)
- [tests/lib/rules/no-dupe-else-if.js](../../../tests/lib/rules/no-dupe-else-if.js)
- [docs/src/rules/no-dupe-else-if.md](../../src/rules/no-dupe-else-if.md)

### C-31: no-duplicate-case

**Disposition:** reserved for replan; difficulty `easy`. **Source mechanism:** equal; SwitchStatement.

Observed TypeScript: `switch (x) { case 1: break; case (1 as number): break; }`

Settings: default rule options; module source.

Baseline: **no diagnostics**. unexpected missing.

**Expected:** Compare wrapped case tests while retaining existing literal/expression comparison policy.

**Syntax-only basis:** The erased wrapper retains its value expression; inspect that expression and existing syntactic predicates, never the asserted type.

Exact files:

- [lib/rules/no-duplicate-case.js](../../../lib/rules/no-duplicate-case.js)
- [tests/lib/rules/no-duplicate-case.js](../../../tests/lib/rules/no-duplicate-case.js)
- [docs/src/rules/no-duplicate-case.md](../../src/rules/no-duplicate-case.md)

## Known shared-work questions for the checkpoint

C-01/C-02 already meet at `lib/rules/utils/ast-utils.js::couldBeError`; C-04 uses `isConstant`, and other wrapper cases mix source ranges, parent traversal, static evaluation and token comparisons. Do not create a universal unwrapping helper merely because these cases have similar names. If two selected lanes require the same helper change, the replan must assign that helper and its tests to one prerequisite node, then add only its real consumer edges. Do not copy a recursive shared implementation into both rules to preserve a shallow graph.

C-18 requires the existing `allowFunctionParams: false` option: its default intentionally permits parameter underscores. C-29 requires a configured readonly `setTimeout` global and a wrapped callee; the existing static evaluator already handles a wrapped literal string argument. These were corrected during probing before inclusion.

`no-object-constructor` generic-call suggestions, type-only naming conventions and literal-string types need a defensible rule-policy or type-safety requirement before commissioning. They are not counted as confirmed candidates merely because a compiler or parser accepts a snippet. Type-aware alternatives to `dot-notation`, `consistent-return`, `require-await`, or Promise/error rules are excluded; their existing syntax-only behavior may still have a separately demonstrated gap.
