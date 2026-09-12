# Exclusion ledger A-M for 100-119

Selected-base snapshot `3d8a6128e70d2f641697d5ebbfd107f02fa1f671`; 71 entries. See [inventory method and limits](100-119-rule-inventory.md#coverage-and-interpretation).

Each source link points to the existing rule check surface; its same-name test and documentation are the read-only companions. **D:** deprecated rule, deferred to preserve current-rule review capacity; this is a delivery decision, not a claim of TypeScript compatibility. **S:** existing TypeScript tests/handling and no additional gap demonstrated. **N:** no gap demonstrated in the bounded survey; re-evaluate if implementation yields evidence. **T:** named type-information or policy boundary, excluded from this syntax-only wave. Frozen, nondeprecated rules are still eligible for fork bug fixes.

<!-- prettier-ignore -->
| Rule / inspected source | Disposition and exclusion reason |
| --- | --- |
| [accessor-pairs](../../../lib/rules/accessor-pairs.js#L42) | S — existing TS parser tests; TSInterfaceBody, TSMethodSignature, TSTypeLiteral handling; no additional demonstrated gap. |
| [array-bracket-newline](../../../lib/rules/array-bracket-newline.js#L95) | D — deprecated metadata; no new delivery lane. |
| [array-bracket-spacing](../../../lib/rules/array-bracket-spacing.js#L89) | D — deprecated metadata; no new delivery lane. |
| [array-element-newline](../../../lib/rules/array-element-newline.js#L115) | D — deprecated metadata; no new delivery lane. |
| [arrow-body-style](../../../lib/rules/arrow-body-style.js#L398) | N — `BinaryExpression[operator='in'], ArrowFunctionExpression`; existing check: require braces around arrow function bodies. No TS-specific correction demonstrated. |
| [arrow-parens](../../../lib/rules/arrow-parens.js#L169) | D — deprecated metadata; no new delivery lane. |
| [arrow-spacing](../../../lib/rules/arrow-spacing.js#L93) | D — deprecated metadata; no new delivery lane. |
| [block-scoped-var](../../../lib/rules/block-scoped-var.js#L120) | N — `Program`; existing check: enforce the use of variables within the scope they are defined. No TS-specific correction demonstrated. |
| [block-spacing](../../../lib/rules/block-spacing.js#L68) | D — deprecated metadata; no new delivery lane. |
| [brace-style](../../../lib/rules/brace-style.js#L226) | D — deprecated metadata; no new delivery lane. |
| [callback-return](../../../lib/rules/callback-return.js#L149) | D — deprecated metadata; no new delivery lane. |
| [camelcase](../../../lib/rules/camelcase.js#L267) | T — Extending variable-name policy to type-only names needs explicit semantics; no proven gap commissioned. |
| [capitalized-comments](../../../lib/rules/capitalized-comments.js#L318) | N — `Program`; existing check: enforce or disallow capitalization of the first letter of a comment. No TS-specific correction demonstrated. |
| [class-methods-use-this](../../../lib/rules/class-methods-use-this.js#L81) | S — existing TS parser tests; pushContext, popContext handling; no additional demonstrated gap. |
| [comma-dangle](../../../lib/rules/comma-dangle.js#L403) | D — deprecated metadata; no new delivery lane. |
| [comma-spacing](../../../lib/rules/comma-spacing.js#L155) | D — deprecated metadata; no new delivery lane. |
| [comma-style](../../../lib/rules/comma-style.js#L111) | D — deprecated metadata; no new delivery lane. |
| [complexity](../../../lib/rules/complexity.js#L114) | N — `onCodePathStart, AssignmentExpression`; existing check: enforce a maximum cyclomatic complexity allowed in a program. No TS-specific correction demonstrated. |
| [computed-property-spacing](../../../lib/rules/computed-property-spacing.js#L93) | D — deprecated metadata; no new delivery lane. |
| [consistent-return](../../../lib/rules/consistent-return.js#L133) | T — Promise/void/never return-type inference is excluded; existing code-path behavior remains. |
| [consistent-this](../../../lib/rules/consistent-this.js#L162) | N — `VariableDeclarator, AssignmentExpression`; existing check: enforce consistent naming when capturing the current execution context. No TS-specific correction demonstrated. |
| [constructor-super](../../../lib/rules/constructor-super.js#L210) | N — `onCodePathStart, onCodePathEnd`; existing check: require `super()` calls in constructors. No TS-specific correction demonstrated. |
| [curly](../../../lib/rules/curly.js#L231) | N — `check, IfStatement`; existing check: enforce consistent brace style for all control statements. No TS-specific correction demonstrated. |
| [default-case-last](../../../lib/rules/default-case-last.js#L33) | N — `SwitchStatement`; existing check: enforce `default` clauses in `switch` statements to be last. No TS-specific correction demonstrated. |
| [default-case](../../../lib/rules/default-case.js#L69) | N — `SwitchStatement`; existing check: require `default` cases in `switch` statements. No TS-specific correction demonstrated. |
| [default-param-last](../../../lib/rules/default-param-last.js#L13) | S — existing TS parser tests; TSParameterProperty handling; no additional demonstrated gap. |
| [dot-location](../../../lib/rules/dot-location.js#L76) | D — deprecated metadata; no new delivery lane. |
| [dot-notation](../../../lib/rules/dot-notation.js#L148) | T — Access-control/index-signature exceptions need resolved member types; do not add type-aware policy. |
| [eol-last](../../../lib/rules/eol-last.js) | D — deprecated metadata; no new delivery lane. |
| [eqeqeq](../../../lib/rules/eqeqeq.js#L201) | N — `BinaryExpression`; existing check: require the use of `===` and `!==`. No TS-specific correction demonstrated. |
| [for-direction](../../../lib/rules/for-direction.js#L166) | N — `ForStatement`; existing check: enforce `for` loop update clause moving the counter in the right direction. No TS-specific correction demonstrated. |
| [func-call-spacing](../../../lib/rules/func-call-spacing.js#L250) | D — deprecated metadata; no new delivery lane. |
| [func-name-matching](../../../lib/rules/func-name-matching.js#L209) | N — `VariableDeclarator, AssignmentExpression`; existing check: require function names to match the name of the variable or property to which they are assigned. No TS-specific correction demonstrated. |
| [func-names](../../../lib/rules/func-names.js#L29) | N — `isFunctionName, getConfigForNode`; existing check: require or disallow named `function` expressions. No TS-specific correction demonstrated. |
| [func-style](../../../lib/rules/func-style.js#L112) | S — existing TS parser tests; TSDeclareFunction handling; no additional demonstrated gap. |
| [function-call-argument-newline](../../../lib/rules/function-call-argument-newline.js#L94) | D — deprecated metadata; no new delivery lane. |
| [function-paren-newline](../../../lib/rules/function-paren-newline.js#L116) | D — deprecated metadata; no new delivery lane. |
| [generator-star-spacing](../../../lib/rules/generator-star-spacing.js#L107) | D — deprecated metadata; no new delivery lane. |
| [getter-return](../../../lib/rules/getter-return.js#L131) | N — `onCodePathStart, onCodePathEnd`; existing check: enforce `return` statements in getters. No TS-specific correction demonstrated. |
| [global-require](../../../lib/rules/global-require.js#L99) | D — deprecated metadata; no new delivery lane. |
| [grouped-accessor-pairs](../../../lib/rules/grouped-accessor-pairs.js#L243) | S — existing TS parser tests; TSInterfaceBody, TSMethodSignature, TSTypeLiteral handling; no additional demonstrated gap. |
| [guard-for-in](../../../lib/rules/guard-for-in.js#L31) | N — `ForInStatement`; existing check: require `for-in` loops to include an `if` statement. No TS-specific correction demonstrated. |
| [handle-callback-err](../../../lib/rules/handle-callback-err.js#L64) | D — deprecated metadata; no new delivery lane. |
| [id-blacklist](../../../lib/rules/id-blacklist.js#L230) | D — deprecated metadata; no new delivery lane. |
| [id-denylist](../../../lib/rules/id-denylist.js#L216) | N — `Program`; existing check: disallow specified identifiers. No TS-specific correction demonstrated. |
| [id-length](../../../lib/rules/id-length.js#L122) | T — Type-only naming extension needs policy evidence; no proven gap commissioned. |
| [id-match](../../../lib/rules/id-match.js#L207) | N — `Program, Identifier`; existing check: require identifiers to match a specified regular expression. No TS-specific correction demonstrated. |
| [implicit-arrow-linebreak](../../../lib/rules/implicit-arrow-linebreak.js#L67) | D — deprecated metadata; no new delivery lane. |
| [indent-legacy](../../../lib/rules/indent-legacy.js#L1176) | D — deprecated metadata; no new delivery lane. |
| [indent](../../../lib/rules/indent.js#L1215) | D — deprecated metadata; no new delivery lane. |
| [init-declarations](../../../lib/rules/init-declarations.js#L119) | S — existing TS parser tests; TSModuleDeclaration handling; no additional demonstrated gap. |
| [jsx-quotes](../../../lib/rules/jsx-quotes.js#L23) | D — deprecated metadata; no new delivery lane. |
| [key-spacing](../../../lib/rules/key-spacing.js#L795) | D — deprecated metadata; no new delivery lane. |
| [keyword-spacing](../../../lib/rules/keyword-spacing.js#L691) | D — deprecated metadata; no new delivery lane. |
| [line-comment-position](../../../lib/rules/line-comment-position.js#L110) | D — deprecated metadata; no new delivery lane. |
| [linebreak-style](../../../lib/rules/linebreak-style.js#L86) | D — deprecated metadata; no new delivery lane. |
| [lines-around-comment](../../../lib/rules/lines-around-comment.js#L547) | D — deprecated metadata; no new delivery lane. |
| [lines-around-directive](../../../lib/rules/lines-around-directive.js#L94) | D — deprecated metadata; no new delivery lane. |
| [lines-between-class-members](../../../lib/rules/lines-between-class-members.js#L281) | D — deprecated metadata; no new delivery lane. |
| [logical-assignment-operators](../../../lib/rules/logical-assignment-operators.js#L363) | N — `AssignmentExpression, AssignmentExpression[operator='='][right.type='LogicalExpression']`; existing check: require or disallow logical assignment operator shorthand. No TS-specific correction demonstrated. |
| [max-classes-per-file](../../../lib/rules/max-classes-per-file.js#L67) | N — `Program, Program:exit`; existing check: enforce a maximum number of classes per file. No TS-specific correction demonstrated. |
| [max-depth](../../../lib/rules/max-depth.js#L146) | N — `IfStatement, IfStatement:exit`; existing check: enforce a maximum depth that blocks can be nested. No TS-specific correction demonstrated. |
| [max-len](../../../lib/rules/max-len.js#L132) | D — deprecated metadata; no new delivery lane. |
| [max-lines-per-function](../../../lib/rules/max-lines-per-function.js#L53) | N — `getCommentLineNumbers, isFullLineComment`; existing check: enforce a maximum number of lines of code in a function. No TS-specific correction demonstrated. |
| [max-lines](../../../lib/rules/max-lines.js#L140) | N — `Program:exit`; existing check: enforce a maximum number of lines per file. No TS-specific correction demonstrated. |
| [max-nested-callbacks](../../../lib/rules/max-nested-callbacks.js#L94) | N — `checkFunction, popStack`; existing check: enforce a maximum depth that callbacks can be nested. No TS-specific correction demonstrated. |
| [max-params](../../../lib/rules/max-params.js#L105) | S — existing TS parser tests; TSDeclareFunction, TSFunctionType, TSVoidKeyword handling; no additional demonstrated gap. |
| [max-statements-per-line](../../../lib/rules/max-statements-per-line.js#L90) | D — deprecated metadata; no new delivery lane. |
| [max-statements](../../../lib/rules/max-statements.js#L178) | N — `Program:exit`; existing check: enforce a maximum number of statements allowed in function blocks. No TS-specific correction demonstrated. |
| [multiline-comment-style](../../../lib/rules/multiline-comment-style.js#L318) | D — deprecated metadata; no new delivery lane. |
| [multiline-ternary](../../../lib/rules/multiline-ternary.js#L79) | D — deprecated metadata; no new delivery lane. |
