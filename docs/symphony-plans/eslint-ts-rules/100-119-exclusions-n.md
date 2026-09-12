# Exclusion ledger N for 100-119

Selected-base snapshot `3d8a6128e70d2f641697d5ebbfd107f02fa1f671`; 133 entries. See [inventory method and limits](100-119-rule-inventory.md#coverage-and-interpretation).

Each source link points to the existing rule check surface; its same-name test and documentation are the read-only companions. **D:** deprecated rule, deferred to preserve current-rule review capacity; this is a delivery decision, not a claim of TypeScript compatibility. **S:** existing TypeScript tests/handling and no additional gap demonstrated. **N:** no gap demonstrated in the bounded survey; re-evaluate if implementation yields evidence. **T:** named type-information or policy boundary, excluded from this syntax-only wave. Frozen, nondeprecated rules are still eligible for fork bug fixes.

<!-- prettier-ignore -->
| Rule / inspected source | Disposition and exclusion reason |
| --- | --- |
| [new-cap](../../../lib/rules/new-cap.js#L129) | N — `extractNameFromExpression, getCap`; existing check: require constructor names to begin with a capital letter. No TS-specific correction demonstrated. |
| [new-parens](../../../lib/rules/new-parens.js#L76) | D — deprecated metadata; no new delivery lane. |
| [newline-after-var](../../../lib/rules/newline-after-var.js#L97) | D — deprecated metadata; no new delivery lane. |
| [newline-before-return](../../../lib/rules/newline-before-return.js#L218) | D — deprecated metadata; no new delivery lane. |
| [newline-per-chained-call](../../../lib/rules/newline-per-chained-call.js#L112) | D — deprecated metadata; no new delivery lane. |
| [no-alert](../../../lib/rules/no-alert.js#L111) | N — `CallExpression`; existing check: disallow the use of `alert`, `confirm`, and `prompt`. No TS-specific correction demonstrated. |
| [no-array-constructor](../../../lib/rules/no-array-constructor.js#L58) | S — existing TS parser tests; hasCommentsInArrayConstructor, getArgumentsText handling; no additional demonstrated gap. |
| [no-await-in-loop](../../../lib/rules/no-await-in-loop.js#L12) | N — `isBoundary, isLooped`; existing check: disallow `await` inside of loops. No TS-specific correction demonstrated. |
| [no-bitwise](../../../lib/rules/no-bitwise.js#L83) | N — `report, hasBitwiseOperator`; existing check: disallow bitwise operators. No TS-specific correction demonstrated. |
| [no-buffer-constructor](../../../lib/rules/no-buffer-constructor.js#L58) | D — deprecated metadata; no new delivery lane. |
| [no-caller](../../../lib/rules/no-caller.js#L33) | N — `MemberExpression`; existing check: disallow the use of `arguments.caller` or `arguments.callee`. No TS-specific correction demonstrated. |
| [no-case-declarations](../../../lib/rules/no-case-declarations.js#L51) | N — `SwitchCase`; existing check: disallow lexical declarations in case clauses. No TS-specific correction demonstrated. |
| [no-catch-shadow](../../../lib/rules/no-catch-shadow.js#L75) | D — deprecated metadata; no new delivery lane. |
| [no-class-assign](../../../lib/rules/no-class-assign.js#L40) | N — `checkVariable, checkForClass`; existing check: disallow reassigning class members. No TS-specific correction demonstrated. |
| [no-cond-assign](../../../lib/rules/no-cond-assign.js#L75) | N — `isConditionalTestExpression, findConditionalAncestor`; existing check: disallow assignment operators in conditional expressions. No TS-specific correction demonstrated. |
| [no-confusing-arrow](../../../lib/rules/no-confusing-arrow.js#L21) | D — deprecated metadata; no new delivery lane. |
| [no-const-assign](../../../lib/rules/no-const-assign.js#L64) | N — `VariableDeclaration`; existing check: disallow reassigning `const`, `using`, and `await using` variables. No TS-specific correction demonstrated. |
| [no-constructor-return](../../../lib/rules/no-constructor-return.js#L36) | N — `onCodePathStart, onCodePathEnd`; existing check: disallow returning value from constructor. No TS-specific correction demonstrated. |
| [no-continue](../../../lib/rules/no-continue.js#L33) | N — `ContinueStatement`; existing check: disallow `continue` statements. No TS-specific correction demonstrated. |
| [no-control-regex](../../../lib/rules/no-control-regex.js#L122) | N — `Literal`; existing check: disallow control characters in regular expressions. No TS-specific correction demonstrated. |
| [no-debugger](../../../lib/rules/no-debugger.js#L33) | N — `DebuggerStatement`; existing check: disallow the use of `debugger`. No TS-specific correction demonstrated. |
| [no-delete-var](../../../lib/rules/no-delete-var.js#L32) | N — `UnaryExpression`; existing check: disallow deleting variables. No TS-specific correction demonstrated. |
| [no-div-regex](../../../lib/rules/no-div-regex.js#L39) | N — `Literal`; existing check: disallow equal signs explicitly at the beginning of regular expressions. No TS-specific correction demonstrated. |
| [no-dupe-args](../../../lib/rules/no-dupe-args.js#L55) | N — `isParameter, checkParams`; existing check: disallow duplicate arguments in `function` definitions. No TS-specific correction demonstrated. |
| [no-dupe-class-members](../../../lib/rules/no-dupe-class-members.js#L61) | S — existing TS parser tests; TSEmptyBodyFunctionExpression handling; no additional demonstrated gap. |
| [no-dupe-keys](../../../lib/rules/no-dupe-keys.js#L106) | N — `ObjectExpression, ObjectExpression:exit`; existing check: disallow duplicate keys in object literals. No TS-specific correction demonstrated. |
| [no-duplicate-imports](../../../lib/rules/no-duplicate-imports.js#L27) | S — existing TS parser tests; isImportExportSpecifier, getImportExportType handling; no additional demonstrated gap. |
| [no-else-return](../../../lib/rules/no-else-return.js#L78) | N — `isSafeToDeclare, isSafeFromNameCollisions`; existing check: disallow `else` blocks after `return` statements in `if` statements. No TS-specific correction demonstrated. |
| [no-empty-character-class](../../../lib/rules/no-empty-character-class.js#L46) | N — `Literal[regex], onCharacterClassEnter`; existing check: disallow empty character classes in regular expressions. No TS-specific correction demonstrated. |
| [no-empty-function](../../../lib/rules/no-empty-function.js#L45) | S — existing TS parser tests; TSParameterProperty handling; no additional demonstrated gap. |
| [no-empty-pattern](../../../lib/rules/no-empty-pattern.js#L51) | N — `ObjectPattern, ArrayPattern`; existing check: disallow empty destructuring patterns. No TS-specific correction demonstrated. |
| [no-empty-static-block](../../../lib/rules/no-empty-static-block.js#L35) | N — `StaticBlock`; existing check: disallow empty static blocks. No TS-specific correction demonstrated. |
| [no-empty](../../../lib/rules/no-empty.js#L58) | N — `BlockStatement, SwitchStatement`; existing check: disallow empty block statements. No TS-specific correction demonstrated. |
| [no-eq-null](../../../lib/rules/no-eq-null.js#L34) | N — `BinaryExpression`; existing check: disallow `null` comparisons without type-checking operators. No TS-specific correction demonstrated. |
| [no-eval](../../../lib/rules/no-eval.js#L206) | N — `CallExpression:exit, CallExpression:exit`; existing check: disallow the use of `eval()`. No TS-specific correction demonstrated. |
| [no-ex-assign](../../../lib/rules/no-ex-assign.js#L52) | N — `CatchClause`; existing check: disallow reassigning exceptions in `catch` clauses. No TS-specific correction demonstrated. |
| [no-extend-native](../../../lib/rules/no-extend-native.js#L165) | N — `Program:exit`; existing check: disallow extending native types. No TS-specific correction demonstrated. |
| [no-extra-bind](../../../lib/rules/no-extra-bind.js#L58) | N — `isSideEffectFree, report`; existing check: disallow unnecessary calls to `.bind()`. No TS-specific correction demonstrated. |
| [no-extra-label](../../../lib/rules/no-extra-label.js#L47) | N — `enterBreakableStatement, exitBreakableStatement`; existing check: disallow unnecessary labels. No TS-specific correction demonstrated. |
| [no-extra-parens](../../../lib/rules/no-extra-parens.js#L1027) | D — deprecated metadata; no new delivery lane. |
| [no-extra-semi](../../../lib/rules/no-extra-semi.js#L130) | D — deprecated metadata; no new delivery lane. |
| [no-fallthrough](../../../lib/rules/no-fallthrough.js#L158) | N — `onCodePathStart, onCodePathEnd`; existing check: disallow fallthrough of `case` statements. No TS-specific correction demonstrated. |
| [no-floating-decimal](../../../lib/rules/no-floating-decimal.js#L64) | D — deprecated metadata; no new delivery lane. |
| [no-func-assign](../../../lib/rules/no-func-assign.js#L40) | N — `checkReference, checkVariable`; existing check: disallow reassigning `function` declarations. No TS-specific correction demonstrated. |
| [no-global-assign](../../../lib/rules/no-global-assign.js#L94) | N — `Program`; existing check: disallow assignments to native objects or read-only global variables. No TS-specific correction demonstrated. |
| [no-implicit-coercion](../../../lib/rules/no-implicit-coercion.js#L317) | N — `UnaryExpression, BinaryExpression:exit`; existing check: disallow shorthand type conversions. No TS-specific correction demonstrated. |
| [no-inline-comments](../../../lib/rules/no-inline-comments.js#L107) | N — `Program`; existing check: disallow inline comments after code. No TS-specific correction demonstrated. |
| [no-inner-declarations](../../../lib/rules/no-inner-declarations.js#L127) | N — `FunctionDeclaration, VariableDeclaration`; existing check: disallow variable or `function` declarations in nested blocks. No TS-specific correction demonstrated. |
| [no-invalid-this](../../../lib/rules/no-invalid-this.js#L96) | S — existing TS parser tests; onCodePathStart, onCodePathEnd handling; no additional demonstrated gap. |
| [no-irregular-whitespace](../../../lib/rules/no-irregular-whitespace.js#L103) | N — `removeWhitespaceError, removeInvalidNodeErrorsInLiteral`; existing check: disallow irregular whitespace. No TS-specific correction demonstrated. |
| [no-iterator](../../../lib/rules/no-iterator.js#L38) | N — `MemberExpression`; existing check: disallow the use of the `__iterator__` property. No TS-specific correction demonstrated. |
| [no-label-var](../../../lib/rules/no-label-var.js#L61) | N — `LabeledStatement`; existing check: disallow labels that share a name with a variable. No TS-specific correction demonstrated. |
| [no-labels](../../../lib/rules/no-labels.js#L118) | N — `LabeledStatement, LabeledStatement:exit`; existing check: disallow labeled statements. No TS-specific correction demonstrated. |
| [no-lone-blocks](../../../lib/rules/no-lone-blocks.js#L94) | N — `BlockStatement, BlockStatement`; existing check: disallow unnecessary nested blocks. No TS-specific correction demonstrated. |
| [no-lonely-if](../../../lib/rules/no-lonely-if.js#L43) | N — `IfStatement`; existing check: disallow `if` statements as the only statement in `else` blocks. No TS-specific correction demonstrated. |
| [no-loop-func](../../../lib/rules/no-loop-func.js#L25) | S — existing TS parser tests; isIIFE, getContainingLoopNode handling; no additional demonstrated gap. |
| [no-loss-of-precision](../../../lib/rules/no-loss-of-precision.js#L243) | S — existing TS parser tests; Literal handling; no additional demonstrated gap. |
| [no-misleading-character-class](../../../lib/rules/no-misleading-character-class.js#L93) | N — `surrogatePairWithoutUFlag, surrogatePair`; existing check: disallow characters which are made with multiple code points in character class syntax. No TS-specific correction demonstrated. |
| [no-mixed-operators](../../../lib/rules/no-mixed-operators.js#L49) | D — deprecated metadata; no new delivery lane. |
| [no-mixed-requires](../../../lib/rules/no-mixed-requires.js#L252) | D — deprecated metadata; no new delivery lane. |
| [no-mixed-spaces-and-tabs](../../../lib/rules/no-mixed-spaces-and-tabs.js#L74) | D — deprecated metadata; no new delivery lane. |
| [no-multi-assign](../../../lib/rules/no-multi-assign.js) | N — `existing rule visitor`; existing check: disallow use of chained assignment expressions. No TS-specific correction demonstrated. |
| [no-multi-spaces](../../../lib/rules/no-multi-spaces.js#L109) | D — deprecated metadata; no new delivery lane. |
| [no-multi-str](../../../lib/rules/no-multi-str.js#L54) | N — `Literal`; existing check: disallow multiline strings. No TS-specific correction demonstrated. |
| [no-multiple-empty-lines](../../../lib/rules/no-multiple-empty-lines.js#L111) | D — deprecated metadata; no new delivery lane. |
| [no-native-reassign](../../../lib/rules/no-native-reassign.js#L107) | D — deprecated metadata; no new delivery lane. |
| [no-negated-in-lhs](../../../lib/rules/no-negated-in-lhs.js#L48) | D — deprecated metadata; no new delivery lane. |
| [no-nested-ternary](../../../lib/rules/no-nested-ternary.js#L33) | N — `ConditionalExpression`; existing check: disallow nested ternary expressions. No TS-specific correction demonstrated. |
| [no-new-func](../../../lib/rules/no-new-func.js#L46) | N — `Program:exit`; existing check: disallow `new` operators with the `Function` object. No TS-specific correction demonstrated. |
| [no-new-native-nonconstructor](../../../lib/rules/no-new-native-nonconstructor.js#L42) | N — `Program:exit`; existing check: disallow `new` operators with global non-constructor functions. No TS-specific correction demonstrated. |
| [no-new-object](../../../lib/rules/no-new-object.js#L57) | D — deprecated metadata; no new delivery lane. |
| [no-new-require](../../../lib/rules/no-new-require.js#L54) | D — deprecated metadata; no new delivery lane. |
| [no-new-symbol](../../../lib/rules/no-new-symbol.js#L50) | D — deprecated metadata; no new delivery lane. |
| [no-new-wrappers](../../../lib/rules/no-new-wrappers.js#L41) | N — `NewExpression`; existing check: disallow `new` operators with the `String`, `Number`, and `Boolean` objects. No TS-specific correction demonstrated. |
| [no-nonoctal-decimal-escape](../../../lib/rules/no-nonoctal-decimal-escape.js#L86) | N — `Literal`; existing check: disallow `\8` and `\9` escape sequences in string literals. No TS-specific correction demonstrated. |
| [no-obj-calls](../../../lib/rules/no-obj-calls.js#L76) | N — `Program`; existing check: disallow calling global object properties as functions. No TS-specific correction demonstrated. |
| [no-object-constructor](../../../lib/rules/no-object-constructor.js#L55) | T — Generic-call fix/type-inference concerns need further evidence; not a proven syntax-only lane. |
| [no-octal-escape](../../../lib/rules/no-octal-escape.js#L33) | N — `Literal`; existing check: disallow octal escape sequences in string literals. No TS-specific correction demonstrated. |
| [no-octal](../../../lib/rules/no-octal.js#L32) | N — `Literal`; existing check: disallow octal literals. No TS-specific correction demonstrated. |
| [no-param-reassign](../../../lib/rules/no-param-reassign.js#L89) | N — `isModifyingProp, isIgnoredPropertyAssignment`; existing check: disallow reassigning function parameters. No TS-specific correction demonstrated. |
| [no-path-concat](../../../lib/rules/no-path-concat.js#L61) | D — deprecated metadata; no new delivery lane. |
| [no-plusplus](../../../lib/rules/no-plusplus.js#L87) | N — `UpdateExpression`; existing check: disallow the unary operators `++` and `--`. No TS-specific correction demonstrated. |
| [no-process-env](../../../lib/rules/no-process-env.js#L53) | D — deprecated metadata; no new delivery lane. |
| [no-process-exit](../../../lib/rules/no-process-exit.js#L57) | D — deprecated metadata; no new delivery lane. |
| [no-proto](../../../lib/rules/no-proto.js#L38) | N — `MemberExpression`; existing check: disallow the use of the `__proto__` property. No TS-specific correction demonstrated. |
| [no-prototype-builtins](../../../lib/rules/no-prototype-builtins.js#L27) | N — `isAfterOptional, disallowBuiltIns`; existing check: disallow calling some `Object.prototype` methods directly on objects. No TS-specific correction demonstrated. |
| [no-regex-spaces](../../../lib/rules/no-regex-spaces.js#L99) | N — `onCharacterClassEnter`; existing check: disallow multiple spaces in regular expressions. No TS-specific correction demonstrated. |
| [no-restricted-globals](../../../lib/rules/no-restricted-globals.js#L186) | S — existing TS parser tests; TSClassImplements, TSInterfaceHeritage, TSQualifiedName, TSTypeQuery handling; no additional demonstrated gap. |
| [no-restricted-imports](../../../lib/rules/no-restricted-imports.js#L859) | S — existing TS parser tests; TSExternalModuleReference, TSImportEqualsDeclaration handling; no additional demonstrated gap. |
| [no-restricted-modules](../../../lib/rules/no-restricted-modules.js#L220) | D — deprecated metadata; no new delivery lane. |
| [no-restricted-syntax](../../../lib/rules/no-restricted-syntax.js#L66) | N — `selector`; existing check: disallow specified syntax. No TS-specific correction demonstrated. |
| [no-return-assign](../../../lib/rules/no-return-assign.js#L54) | N — `AssignmentExpression`; existing check: disallow assignment operators in `return` statements. No TS-specific correction demonstrated. |
| [no-return-await](../../../lib/rules/no-return-await.js#L155) | D — deprecated metadata; no new delivery lane. |
| [no-script-url](../../../lib/rules/no-script-url.js#L51) | N — `Literal, TemplateLiteral`; existing check: disallow `javascript:` URLs. No TS-specific correction demonstrated. |
| [no-sequences](../../../lib/rules/no-sequences.js#L123) | N — `SequenceExpression`; existing check: disallow comma operators. No TS-specific correction demonstrated. |
| [no-setter-return](../../../lib/rules/no-setter-return.js#L115) | N — `ArrowFunctionExpression, ReturnStatement`; existing check: disallow returning values from setters. No TS-specific correction demonstrated. |
| [no-shadow-restricted-names](../../../lib/rules/no-shadow-restricted-names.js#L85) | N — `VariableDeclaration, :function, CatchClause, ImportDeclaration, ClassDeclaration, ClassExpression`; existing check: disallow identifiers from shadowing restricted names. No TS-specific correction demonstrated. |
| [no-shadow](../../../lib/rules/no-shadow.js#L675) | S — existing TS parser tests; TSCallSignatureDeclaration, TSConstructSignatureDeclaration, TSConstructorType, TSDeclareFunction handling; no additional demonstrated gap. |
| [no-spaced-func](../../../lib/rules/no-spaced-func.js#L65) | D — deprecated metadata; no new delivery lane. |
| [no-sparse-arrays](../../../lib/rules/no-sparse-arrays.js#L37) | N — `ArrayExpression`; existing check: disallow sparse arrays. No TS-specific correction demonstrated. |
| [no-sync](../../../lib/rules/no-sync.js#L70) | D — deprecated metadata; no new delivery lane. |
| [no-tabs](../../../lib/rules/no-tabs.js#L77) | D — deprecated metadata; no new delivery lane. |
| [no-template-curly-in-string](../../../lib/rules/no-template-curly-in-string.js#L35) | T — Literal type strings need a reviewed rule-policy distinction; a pattern match alone is not an established defect. |
| [no-ternary](../../../lib/rules/no-ternary.js#L33) | N — `ConditionalExpression`; existing check: disallow ternary operators. No TS-specific correction demonstrated. |
| [no-this-before-super](../../../lib/rules/no-this-before-super.js#L174) | N — `onCodePathStart, onCodePathEnd`; existing check: disallow `this`/`super` before calling `super()` in constructors. No TS-specific correction demonstrated. |
| [no-trailing-spaces](../../../lib/rules/no-trailing-spaces.js#L101) | D — deprecated metadata; no new delivery lane. |
| [no-unassigned-vars](../../../lib/rules/no-unassigned-vars.js#L36) | S — existing TS parser tests; TSModuleDeclaration handling; no additional demonstrated gap. |
| [no-undef-init](../../../lib/rules/no-undef-init.js#L49) | N — `VariableDeclarator`; existing check: disallow initializing variables to `undefined`. No TS-specific correction demonstrated. |
| [no-undef](../../../lib/rules/no-undef.js#L65) | T — Compiler/global type-library knowledge is outside this syntax-only project; parser references alone do not authorize that change. |
| [no-undefined](../../../lib/rules/no-undefined.js#L77) | N — `Program:exit`; existing check: disallow the use of `undefined` as an identifier. No TS-specific correction demonstrated. |
| [no-unexpected-multiline](../../../lib/rules/no-unexpected-multiline.js#L75) | N — `MemberExpression, TaggedTemplateExpression`; existing check: disallow confusing multiline expressions. No TS-specific correction demonstrated. |
| [no-unmodified-loop-condition](../../../lib/rules/no-unmodified-loop-condition.js#L102) | N — `ForStatement, enter`; existing check: disallow unmodified loop conditions. No TS-specific correction demonstrated. |
| [no-unreachable-loop](../../../lib/rules/no-unreachable-loop.js#L114) | N — `onCodePathStart, onCodePathEnd`; existing check: disallow loops with a body that allows only one iteration. No TS-specific correction demonstrated. |
| [no-unreachable](../../../lib/rules/no-unreachable.js#L188) | N — `onCodePathStart, onCodePathEnd`; existing check: disallow unreachable code after `return`, `throw`, `continue`, and `break` statements. No TS-specific correction demonstrated. |
| [no-unsafe-finally](../../../lib/rules/no-unsafe-finally.js#L46) | N — `isFinallyBlock, isInFinallyBlock`; existing check: disallow control flow statements in `finally` blocks. No TS-specific correction demonstrated. |
| [no-unused-labels](../../../lib/rules/no-unused-labels.js#L47) | N — `enterLabeledScope, isFixable`; existing check: disallow unused labels. No TS-specific correction demonstrated. |
| [no-unused-private-class-members](../../../lib/rules/no-unused-private-class-members.js#L240) | N — `ClassBody, PrivateIdentifier`; existing check: disallow unused private class members. No TS-specific correction demonstrated. |
| [no-use-before-define](../../../lib/rules/no-use-before-define.js#L447) | S — existing TS parser tests; TSEnumName, TSQualifiedName, TSTypeQuery, TSTypeReference handling; no additional demonstrated gap. |
| [no-useless-assignment](../../../lib/rules/no-useless-assignment.js#L505) | N — `onCodePathStart, onCodePathEnd`; existing check: disallow variable assignments when the value is not used. No TS-specific correction demonstrated. |
| [no-useless-backreference](../../../lib/rules/no-useless-backreference.js#L119) | N — `onBackreferenceEnter, Literal[regex]`; existing check: disallow useless backreferences in regular expressions. No TS-specific correction demonstrated. |
| [no-useless-call](../../../lib/rules/no-useless-call.js#L74) | N — `CallExpression`; existing check: disallow unnecessary calls to `.call()` and `.apply()`. No TS-specific correction demonstrated. |
| [no-useless-catch](../../../lib/rules/no-useless-catch.js#L33) | N — `CatchClause`; existing check: disallow unnecessary `catch` clauses. No TS-specific correction demonstrated. |
| [no-useless-computed-key](../../../lib/rules/no-useless-computed-key.js#L42) | N — `hasUselessComputedKey, check`; existing check: disallow unnecessary computed property keys in objects and classes. No TS-specific correction demonstrated. |
| [no-useless-constructor](../../../lib/rules/no-useless-constructor.js#L18) | S — existing TS parser tests; TSParameterProperty handling; no additional demonstrated gap. |
| [no-useless-escape](../../../lib/rules/no-useless-escape.js#L231) | N — `onCharacterEnter`; existing check: disallow unnecessary escape characters. No TS-specific correction demonstrated. |
| [no-useless-rename](../../../lib/rules/no-useless-rename.js#L73) | N — `reportError, checkDestructured`; existing check: disallow renaming import, export, and destructured assignments to the same name. No TS-specific correction demonstrated. |
| [no-useless-return](../../../lib/rules/no-useless-return.js#L254) | N — `onCodePathStart, onCodePathEnd`; existing check: disallow redundant return statements. No TS-specific correction demonstrated. |
| [no-var](../../../lib/rules/no-var.js#L471) | S — existing TS parser tests; TSModuleBlock, TSModuleDeclaration handling; no additional demonstrated gap. |
| [no-void](../../../lib/rules/no-void.js#L54) | N — `UnaryExpression[operator="void"]`; existing check: disallow `void` operators. No TS-specific correction demonstrated. |
| [no-warning-comments](../../../lib/rules/no-warning-comments.js#L200) | N — `Program`; existing check: disallow specified warning terms in comments. No TS-specific correction demonstrated. |
| [no-whitespace-before-property](../../../lib/rules/no-whitespace-before-property.js#L122) | D — deprecated metadata; no new delivery lane. |
| [no-with](../../../lib/rules/no-with.js#L34) | N — `WithStatement`; existing check: disallow `with` statements. No TS-specific correction demonstrated. |
| [nonblock-statement-body-position](../../../lib/rules/nonblock-statement-body-position.js#L149) | D — deprecated metadata; no new delivery lane. |
