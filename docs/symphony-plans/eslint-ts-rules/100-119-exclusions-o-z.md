# Exclusion ledger O-Z for 100-119

Selected-base snapshot `3d8a6128e70d2f641697d5ebbfd107f02fa1f671`; 51 entries. See [inventory method and limits](100-119-rule-inventory.md#coverage-and-interpretation).

Each source link points to the existing rule check surface; its same-name test and documentation are the read-only companions. **D:** deprecated rule, deferred to preserve current-rule review capacity; this is a delivery decision, not a claim of TypeScript compatibility. **S:** existing TypeScript tests/handling and no additional gap demonstrated. **N:** no gap demonstrated in the bounded survey; re-evaluate if implementation yields evidence. **T:** named type-information or policy boundary, excluded from this syntax-only wave. Frozen, nondeprecated rules are still eligible for fork bug fixes.

<!-- prettier-ignore -->
| Rule / inspected source | Disposition and exclusion reason |
| --- | --- |
| [object-curly-newline](../../../lib/rules/object-curly-newline.js#L50) | D — deprecated metadata; no new delivery lane. |
| [object-curly-spacing](../../../lib/rules/object-curly-spacing.js#L86) | D — deprecated metadata; no new delivery lane. |
| [object-property-newline](../../../lib/rules/object-property-newline.js#L85) | D — deprecated metadata; no new delivery lane. |
| [object-shorthand](../../../lib/rules/object-shorthand.js#L476) | N — `ArrowFunctionExpression, ArrowFunctionExpression:exit`; existing check: require or disallow method and property shorthand syntax for object literals. No TS-specific correction demonstrated. |
| [one-var-declaration-per-line](../../../lib/rules/one-var-declaration-per-line.js#L72) | D — deprecated metadata; no new delivery lane. |
| [one-var](../../../lib/rules/one-var.js#L23) | N — `isInStatementList, startBlock`; existing check: enforce variables to be declared either together or separately in functions. No TS-specific correction demonstrated. |
| [operator-assignment](../../../lib/rules/operator-assignment.js#L24) | N — `isCommutativeOperatorWithShorthand, isNonCommutativeOperatorWithShorthand`; existing check: require or disallow assignment operator shorthand where possible. No TS-specific correction demonstrated. |
| [operator-linebreak](../../../lib/rules/operator-linebreak.js#L299) | D — deprecated metadata; no new delivery lane. |
| [padded-blocks](../../../lib/rules/padded-blocks.js#L129) | D — deprecated metadata; no new delivery lane. |
| [padding-line-between-statements](../../../lib/rules/padding-line-between-statements.js#L278) | D — deprecated metadata; no new delivery lane. |
| [prefer-const](../../../lib/rules/prefer-const.js#L541) | N — `Program:exit, VariableDeclaration`; existing check: require `const` declarations for variables that are never reassigned after declared. No TS-specific correction demonstrated. |
| [prefer-exponentiation-operator](../../../lib/rules/prefer-exponentiation-operator.js#L257) | N — `Program`; existing check: disallow the use of `Math.pow` in favor of the `**` operator. No TS-specific correction demonstrated. |
| [prefer-named-capture-group](../../../lib/rules/prefer-named-capture-group.js#L140) | N — `onCapturingGroupEnter, Literal`; existing check: enforce using named capture group in regular expression. No TS-specific correction demonstrated. |
| [prefer-object-has-own](../../../lib/rules/prefer-object-has-own.js#L77) | N — `CallExpression`; existing check: disallow use of `Object.prototype.hasOwnProperty.call()` and prefer use of `Object.hasOwn()`. No TS-specific correction demonstrated. |
| [prefer-object-spread](../../../lib/rules/prefer-object-spread.js#L293) | N — `Program`; existing check: disallow using `Object.assign` with an object literal as the first argument and prefer the use of object spread instead. No TS-specific correction demonstrated. |
| [prefer-reflect](../../../lib/rules/prefer-reflect.js#L109) | D — deprecated metadata; no new delivery lane. |
| [prefer-rest-params](../../../lib/rules/prefer-rest-params.js#L25) | N — `getVariableOfArguments, isNotNormalMemberAccess`; existing check: require rest parameters instead of `arguments`. No TS-specific correction demonstrated. |
| [prefer-spread](../../../lib/rules/prefer-spread.js#L70) | N — `CallExpression`; existing check: require spread operators instead of `.apply()`. No TS-specific correction demonstrated. |
| [prefer-template](../../../lib/rules/prefer-template.js#L345) | N — `Program`; existing check: require template literals instead of string concatenation. No TS-specific correction demonstrated. |
| [quote-props](../../../lib/rules/quote-props.js#L376) | D — deprecated metadata; no new delivery lane. |
| [quotes](../../../lib/rules/quotes.js#L328) | D — deprecated metadata; no new delivery lane. |
| [radix](../../../lib/rules/radix.js#L162) | N — `Program:exit`; existing check: enforce the use of the radix argument when using `parseInt()`. No TS-specific correction demonstrated. |
| [require-atomic-updates](../../../lib/rules/require-atomic-updates.js#L227) | N — `onCodePathStart, onCodePathEnd`; existing check: disallow assignments that can lead to race conditions due to usage of `await` or `yield`. No TS-specific correction demonstrated. |
| [require-await](../../../lib/rules/require-await.js#L159) | T — Inferring whether returned values are thenable requires types; preserve the syntactic await policy. |
| [require-unicode-regexp](../../../lib/rules/require-unicode-regexp.js#L87) | N — `Literal[regex], Program`; existing check: enforce the use of `u` or `v` flag on regular expressions. No TS-specific correction demonstrated. |
| [require-yield](../../../lib/rules/require-yield.js#L79) | N — `YieldExpression`; existing check: require generator functions to contain `yield`. No TS-specific correction demonstrated. |
| [rest-spread-spacing](../../../lib/rules/rest-spread-spacing.js#L74) | D — deprecated metadata; no new delivery lane. |
| [semi-spacing](../../../lib/rules/semi-spacing.js#L279) | D — deprecated metadata; no new delivery lane. |
| [semi-style](../../../lib/rules/semi-style.js#L183) | D — deprecated metadata; no new delivery lane. |
| [semi](../../../lib/rules/semi.js#L459) | D — deprecated metadata; no new delivery lane. |
| [sort-imports](../../../lib/rules/sort-imports.js#L147) | N — `ImportDeclaration`; existing check: enforce sorted `import` declarations within modules. No TS-specific correction demonstrated. |
| [sort-keys](../../../lib/rules/sort-keys.js#L48) | N — `asc, ascI`; existing check: require object keys to be sorted. No TS-specific correction demonstrated. |
| [sort-vars](../../../lib/rules/sort-vars.js#L56) | N — `VariableDeclaration`; existing check: require variables within the same declaration block to be sorted. No TS-specific correction demonstrated. |
| [space-before-blocks](../../../lib/rules/space-before-blocks.js#L24) | D — deprecated metadata; no new delivery lane. |
| [space-before-function-paren](../../../lib/rules/space-before-function-paren.js#L98) | D — deprecated metadata; no new delivery lane. |
| [space-in-parens](../../../lib/rules/space-in-parens.js#L95) | D — deprecated metadata; no new delivery lane. |
| [space-infix-ops](../../../lib/rules/space-infix-ops.js#L223) | D — deprecated metadata; no new delivery lane. |
| [space-unary-ops](../../../lib/rules/space-unary-ops.js#L105) | D — deprecated metadata; no new delivery lane. |
| [spaced-comment](../../../lib/rules/spaced-comment.js#L438) | D — deprecated metadata; no new delivery lane. |
| [strict](../../../lib/rules/strict.js#L273) | N — `Program, ClassBody`; existing check: require or disallow strict mode directives. No TS-specific correction demonstrated. |
| [switch-colon-spacing](../../../lib/rules/switch-colon-spacing.js#L125) | D — deprecated metadata; no new delivery lane. |
| [symbol-description](../../../lib/rules/symbol-description.js#L54) | N — `Program:exit`; existing check: require symbol descriptions. No TS-specific correction demonstrated. |
| [template-curly-spacing](../../../lib/rules/template-curly-spacing.js#L160) | D — deprecated metadata; no new delivery lane. |
| [template-tag-spacing](../../../lib/rules/template-tag-spacing.js#L66) | D — deprecated metadata; no new delivery lane. |
| [unicode-bom](../../../lib/rules/unicode-bom.js) | N — `existing rule visitor`; existing check: require or disallow Unicode byte order mark (BOM). No TS-specific correction demonstrated. |
| [use-isnan](../../../lib/rules/use-isnan.js#L24) | N — `isNaNIdentifier, getBinaryExpressionFixer`; existing check: require calls to `isNaN()` when checking for `NaN`. No TS-specific correction demonstrated. |
| [valid-typeof](../../../lib/rules/valid-typeof.js#L104) | N — `Program, UnaryExpression`; existing check: enforce comparing `typeof` expressions against valid strings. No TS-specific correction demonstrated. |
| [wrap-iife](../../../lib/rules/wrap-iife.js#L152) | D — deprecated metadata; no new delivery lane. |
| [wrap-regex](../../../lib/rules/wrap-regex.js#L58) | D — deprecated metadata; no new delivery lane. |
| [yield-star-spacing](../../../lib/rules/yield-star-spacing.js#L97) | D — deprecated metadata; no new delivery lane. |
| [yoda](../../../lib/rules/yoda.js#L332) | N — `BinaryExpression`; existing check: require or disallow "Yoda" conditions. No TS-specific correction demonstrated. |
