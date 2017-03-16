# Idearium JavaScript Style Guide

This is a guide for writing consistent and aesthetically pleasing JavaScript code. It is inspired by what is popular within the community, and flavoured with some personal opinions.

It is licensed under the [CC BY-SA 3.0][cc] license. You are encouraged to fork this repository and make adjustments according to your preferences.

[cc]: http://creativecommons.org/licenses/by-sa/3.0/

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## Table of Contents

- [Possible Errors](#possible-errors)
- [Best Practices](#best-practices)
- [Strict Mode](#strict-mode)
- [Variables](#variables)
- [Node.js and CommonJS](#nodejs-and-commonjs)
- [Stylistic Issues](#stylistic-issues)
- [ECMAScript 6](#ecmascript-6)

## Possible Errors

These rules relate to possible syntax or logic errors in JavaScript code:

- ### Disallow comparing against -0 ([no-compare-neg-zero](http://eslint.org/docs/rules/no-compare-neg-zero))

  > Why? Comparing against -0 will not work as expected.

  ```javascript
  // Good.
  if (x === 0) {
      // ...
  }

  // Bad.
  if (x === -0) {
      // ...
  }
  ```

- ### Disallow calling some Object.prototype methods directly on objects ([no-prototype-builtins](http://eslint.org/docs/rules/no-prototype-builtins))

  > Why? It can lead to errors when it is assumed that objects will have properties from `Object.prototype`.

  ```javascript
  // Good.
  const has = Object.prototype.hasOwnProperty;
  has.call(foo, 'bar');

  // Bad.
  foo.hasOwnProperty('bar');
  ```

- ### Disallow template literal placeholder syntax in regular strings ([no-template-curly-in-string](http://eslint.org/docs/rules/no-template-curly-in-string))

  > Why? Because it's an error!

  ```javascript
  // Good.
  `Hello ${name}!`;

  // Bad.
  'Hello ${name}!';
  ```

- ### Disallow negating the left operand of relational operators ([no-unsafe-negation](http://eslint.org/docs/rules/no-unsafe-negation))

  > Why? Nobody wants to memorise operator precedence.

  ```javascript
  // Good.
  if (!(key in object)) {
    // ...
  }

  // Bad.
  if (!key in object) {
    // ...
  }
  ```

- ### Enforce valid JSDoc comments ([valid-jsdoc](http://eslint.org/docs/rules/valid-jsdoc))

  > Why? For complete code documentation.

  ```javascript
  // Good.
  /**
   * Add two numbers.
   * @param   {Number} num1 The first number.
   * @param   {Number} num2 The second number.
   * @returns {Number}      The sum of the two numbers.
   */
  function add(num1, num2) {
      return num1 + num2;
  }

  // Bad.
  /**
   * Add two numbers.
   * @returns {Number} The sum of the two numbers.
   */
  function add(num1, num2) {
      return num1 + num2;
  }
  ```

## Best Practices

These rules relate to better ways of doing things to help you avoid problems:

- ### Enforce getter and setter pairs in objects ([accessor-pairs](http://eslint.org/docs/rules/accessor-pairs))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce return statements in callbacks of array methods ([array-callback-return](http://eslint.org/docs/rules/array-callback-return))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce the use of variables within the scope they are defined ([block-scoped-var](http://eslint.org/docs/rules/block-scoped-var))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce that class methods utilize this ([class-methods-use-this](http://eslint.org/docs/rules/class-methods-use-this))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce a maximum cyclomatic complexity allowed in a program ([complexity](http://eslint.org/docs/rules/complexity))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require return statements to either always or never specify values ([consistent-return](http://eslint.org/docs/rules/consistent-return))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent brace style for all control statements ([curly](http://eslint.org/docs/rules/curly))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require default cases in switch statements ([default-case](http://eslint.org/docs/rules/default-case))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent newlines before and after dots ([dot-location](http://eslint.org/docs/rules/dot-location))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce dot notation whenever possible ([dot-notation](http://eslint.org/docs/rules/dot-notation))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require the use of === and !== ([eqeqeq](http://eslint.org/docs/rules/eqeqeq))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require for-in loops to include an if statement ([guard-for-in](http://eslint.org/docs/rules/guard-for-in))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow the use of alert, confirm, and prompt ([no-alert](http://eslint.org/docs/rules/no-alert))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow the use of arguments.caller or arguments.callee ([no-caller](http://eslint.org/docs/rules/no-caller))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow division operators explicitly at the beginning of regular expressions ([no-div-regex](http://eslint.org/docs/rules/no-div-regex))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow else blocks after return statements in if statements ([no-else-return](http://eslint.org/docs/rules/no-else-return))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow empty functions ([no-empty-function](http://eslint.org/docs/rules/no-empty-function))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow null comparisons without type-checking operators ([no-eq-null](http://eslint.org/docs/rules/no-eq-null))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow the use of eval() ([no-eval](http://eslint.org/docs/rules/no-eval))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow extending native types ([no-extend-native](http://eslint.org/docs/rules/no-extend-native))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unnecessary calls to .bind() ([no-extra-bind](http://eslint.org/docs/rules/no-extra-bind))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unnecessary labels ([no-extra-label](http://eslint.org/docs/rules/no-extra-label))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow leading or trailing decimal points in numeric literals ([no-floating-decimal](http://eslint.org/docs/rules/no-floating-decimal))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow assignments to native objects or read-only global variables ([no-global-assign](http://eslint.org/docs/rules/no-global-assign))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow shorthand type conversions ([no-implicit-coercion](http://eslint.org/docs/rules/no-implicit-coercion))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow variable and function declarations in the global scope ([no-implicit-globals](http://eslint.org/docs/rules/no-implicit-globals))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow the use of eval()-like methods ([no-implied-eval](http://eslint.org/docs/rules/no-implied-eval))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow this keywords outside of classes or class-like objects ([no-invalid-this](http://eslint.org/docs/rules/no-invalid-this))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow the use of the __iterator__ property ([no-iterator](http://eslint.org/docs/rules/no-iterator))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow labeled statements ([no-labels](http://eslint.org/docs/rules/no-labels))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unnecessary nested blocks ([no-lone-blocks](http://eslint.org/docs/rules/no-lone-blocks))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow function declarations and expressions inside loop statements ([no-loop-func](http://eslint.org/docs/rules/no-loop-func))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow magic numbers ([no-magic-numbers](http://eslint.org/docs/rules/no-magic-numbers))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow multiple spaces ([no-multi-spaces](http://eslint.org/docs/rules/no-multi-spaces))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow multiline strings ([no-multi-str](http://eslint.org/docs/rules/no-multi-str))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow new operators outside of assignments or comparisons ([no-new](http://eslint.org/docs/rules/no-new))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow new operators with the Function object ([no-new-func](http://eslint.org/docs/rules/no-new-func))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow new operators with the String, Number, and Boolean objects ([no-new-wrappers](http://eslint.org/docs/rules/no-new-wrappers))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow octal escape sequences in string literals ([no-octal-escape](http://eslint.org/docs/rules/no-octal-escape))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow reassigning function parameters ([no-param-reassign](http://eslint.org/docs/rules/no-param-reassign))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow the use of the __proto__ property ([no-proto](http://eslint.org/docs/rules/no-proto))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow certain properties on certain objects ([no-restricted-properties](http://eslint.org/docs/rules/no-restricted-properties))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow assignment operators in return statements ([no-return-assign](http://eslint.org/docs/rules/no-return-assign))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unnecessary return await ([no-return-await](http://eslint.org/docs/rules/no-return-await))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow javascript: urls ([no-script-url](http://eslint.org/docs/rules/no-script-url))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow comparisons where both sides are exactly the same ([no-self-compare](http://eslint.org/docs/rules/no-self-compare))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow comma operators ([no-sequences](http://eslint.org/docs/rules/no-sequences))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow throwing literals as exceptions ([no-throw-literal](http://eslint.org/docs/rules/no-throw-literal))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unmodified loop conditions - ([no-unmodified-loop-condition](http://eslint.org/docs/rules/no-unmodified-loop-condition))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unused expressions ([no-unused-expressions](http://eslint.org/docs/rules/no-unused-expressions))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unnecessary calls to .call() and .apply() ([no-useless-call](http://eslint.org/docs/rules/no-useless-call))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unnecessary concatenation of literals or template literals ([no-useless-concat](http://eslint.org/docs/rules/no-useless-concat))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unnecessary escape characters ([no-useless-escape](http://eslint.org/docs/rules/no-useless-escape))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow redundant return statements ([no-useless-return](http://eslint.org/docs/rules/no-useless-return))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow void operators ([no-void](http://eslint.org/docs/rules/no-void))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow specified warning terms in comments ([no-warning-comments](http://eslint.org/docs/rules/no-warning-comments))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow with statements ([no-with](http://eslint.org/docs/rules/no-with))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require using Error objects as Promise rejection reasons ([prefer-promise-reject-errors](http://eslint.org/docs/rules/prefer-promise-reject-errors))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce the consistent use of the radix argument when using parseInt() ([radix](http://eslint.org/docs/rules/radix))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow async functions which have no await expression ([require-await](http://eslint.org/docs/rules/require-await))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require var declarations be placed at the top of their containing scope ([vars-on-top](http://eslint.org/docs/rules/vars-on-top))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require parentheses around immediate function invocations ([wrap-iife](http://eslint.org/docs/rules/wrap-iife))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow “Yoda” conditions ([yoda](http://eslint.org/docs/rules/yoda))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

## Strict Mode

These rules relate to strict mode directives:

- ### Require or disallow strict mode directives ([strict](http://eslint.org/docs/rules/strict))

  > Why? To enforce proper semantics.

  ```javascript
  // Good.
  'use strict';

  function foo() {
      // ...
  }

  // Bad.
  function foo() {
      // ...
  }
  ```

## Variables

These rules relate to variable declarations:

- ### Disallow identifiers from shadowing restricted names ([no-shadow-restricted-names](http://eslint.org/docs/rules/no-shadow-restricted-names))

  > Why? Just don't.

  ```javascript
  // Good.
  let foo;

  // Bad.
  const undefined = 'foo';
  ```

- ### Disallow initializing variables to undefined ([no-undef-init](http://eslint.org/docs/rules/no-undef-init))

  > Why? Same as above, just don't.

  ```javascript
  // Good.
  let foo;

  // Bad.
  const foo = undefined;
  ```

- ### Disallow the use of undefined as an identifier ([no-undefined](http://eslint.org/docs/rules/no-undefined))

  > Why? Same as above.

  ```javascript
  // Good.
  let foo;

  // Bad.
  const undefined = 'foo';
  ```

- ### Disallow the use of variables before they are defined ([no-use-before-define](http://eslint.org/docs/rules/no-use-before-define))

  > Why? Whilst vars will be hoisted, try not to use them. It is also easier to read.

  ```javascript
  // Good.
  const bar = 'bar';

  function foo() {
    return bar;
  }

  // Bad.
  function foo() {
    return bar;
  }

  var bar = 'bar';
  ```

## Node.js and CommonJS

These rules relate to code running in Node.js, or in browsers with CommonJS:

- ### Require return statements after callbacks ([callback-return](http://eslint.org/docs/rules/callback-return))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require require() calls to be placed at top-level module scope ([global-require](http://eslint.org/docs/rules/global-require))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require error handling in callbacks ([handle-callback-err](http://eslint.org/docs/rules/handle-callback-err))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow require calls to be mixed with regular variable declarations ([no-mixed-requires](http://eslint.org/docs/rules/no-mixed-requires))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow new operators with calls to require ([no-new-require](http://eslint.org/docs/rules/no-new-require))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow string concatenation with `__dirname` and `__filename` ([no-path-concat](http://eslint.org/docs/rules/no-path-concat))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow the use of process.env ([no-process-env](http://eslint.org/docs/rules/no-process-env))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow the use of process.exit() ([no-process-exit](http://eslint.org/docs/rules/no-process-exit))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow specified modules when loaded by require ([no-restricted-modules](http://eslint.org/docs/rules/no-restricted-modules))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow synchronous methods ([no-sync](http://eslint.org/docs/rules/no-sync))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

## Stylistic Issues

These rules relate to style guidelines, and are therefore quite subjective:

- ### Enforce consistent spacing inside array brackets ([array-bracket-spacing](http://eslint.org/docs/rules/array-bracket-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing inside single-line blocks ([block-spacing](http://eslint.org/docs/rules/block-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent brace style for blocks ([brace-style](http://eslint.org/docs/rules/brace-style))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce camelcase naming convention ([camelcase](http://eslint.org/docs/rules/camelcase))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce or disallow capitalization of the first letter of a comment ([capitalized-comments](http://eslint.org/docs/rules/capitalized-comments))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow trailing commas ([comma-dangle](http://eslint.org/docs/rules/comma-dangle))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing before and after commas ([comma-spacing](http://eslint.org/docs/rules/comma-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent comma style ([comma-style](http://eslint.org/docs/rules/comma-style))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing inside computed property brackets ([computed-property-spacing](http://eslint.org/docs/rules/computed-property-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent naming when capturing the current execution context ([consistent-this](http://eslint.org/docs/rules/consistent-this))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow newline at the end of files ([eol-last](http://eslint.org/docs/rules/eol-last))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow spacing between function identifiers and their invocations ([func-call-spacing](http://eslint.org/docs/rules/func-call-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require function names to match the name of the variable or property to which they are assigned ([func-name-matching](http://eslint.org/docs/rules/func-name-matching))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow named function expressions ([func-names](http://eslint.org/docs/rules/func-names))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce the consistent use of either function declarations or expressions ([func-style](http://eslint.org/docs/rules/func-style))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow specified identifiers ([id-blacklist](http://eslint.org/docs/rules/id-blacklist))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce minimum and maximum identifier lengths ([id-length](http://eslint.org/docs/rules/id-length))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require identifiers to match a specified regular expression ([id-match](http://eslint.org/docs/rules/id-match))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent indentation ([indent](http://eslint.org/docs/rules/indent))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce the consistent use of either double or single quotes in JSX attributes ([jsx-quotes](http://eslint.org/docs/rules/jsx-quotes))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing between keys and values in object literal properties ([key-spacing](http://eslint.org/docs/rules/key-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing before and after keywords ([keyword-spacing](http://eslint.org/docs/rules/keyword-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce position of line comments ([line-comment-position](http://eslint.org/docs/rules/line-comment-position))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent linebreak style ([linebreak-style](http://eslint.org/docs/rules/linebreak-style))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require empty lines around comments ([lines-around-comment](http://eslint.org/docs/rules/lines-around-comment))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow newlines around directives ([lines-around-directive](http://eslint.org/docs/rules/lines-around-directive))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce a maximum depth that blocks can be nested ([max-depth](http://eslint.org/docs/rules/max-depth))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce a maximum line length ([max-len](http://eslint.org/docs/rules/max-len))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce a maximum number of lines per file ([max-lines](http://eslint.org/docs/rules/max-lines))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce a maximum depth that callbacks can be nested ([max-nested-callbacks](http://eslint.org/docs/rules/max-nested-callbacks))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce a maximum number of parameters in function definitions ([max-params](http://eslint.org/docs/rules/max-params))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce a maximum number of statements allowed in function blocks ([max-statements](http://eslint.org/docs/rules/max-statements))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce a maximum number of statements allowed per line ([max-statements-per-line](http://eslint.org/docs/rules/max-statements-per-line))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce newlines between operands of ternary expressions ([multiline-ternary](http://eslint.org/docs/rules/multiline-ternary))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require constructor names to begin with a capital letter ([new-cap](http://eslint.org/docs/rules/new-cap))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require parentheses when invoking a constructor with no arguments ([new-parens](http://eslint.org/docs/rules/new-parens))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow an empty line after variable declarations ([newline-after-var](http://eslint.org/docs/rules/newline-after-var))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require an empty line before return statements ([newline-before-return](http://eslint.org/docs/rules/newline-before-return))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require a newline after each call in a method chain ([newline-per-chained-call](http://eslint.org/docs/rules/newline-per-chained-call))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow Array constructors ([no-array-constructor](http://eslint.org/docs/rules/no-array-constructor))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow bitwise operators ([no-bitwise](http://eslint.org/docs/rules/no-bitwise))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow continue statements ([no-continue](http://eslint.org/docs/rules/no-continue))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow inline comments after code ([no-inline-comments](http://eslint.org/docs/rules/no-inline-comments))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow if statements as the only statement in else blocks ([no-lonely-if](http://eslint.org/docs/rules/no-lonely-if))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow mixed binary operators ([no-mixed-operators](http://eslint.org/docs/rules/no-mixed-operators))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow use of chained assignment expressions ([no-multi-assign](http://eslint.org/docs/rules/no-multi-assign))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow multiple empty lines ([no-multiple-empty-lines](http://eslint.org/docs/rules/no-multiple-empty-lines))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow negated conditions ([no-negated-condition](http://eslint.org/docs/rules/no-negated-condition))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow nested ternary expressions ([no-nested-ternary](http://eslint.org/docs/rules/no-nested-ternary))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow Object constructors ([no-new-object](http://eslint.org/docs/rules/no-new-object))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow the unary operators ++ and -- ([no-plusplus](http://eslint.org/docs/rules/no-plusplus))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow specified syntax ([no-restricted-syntax](http://eslint.org/docs/rules/no-restricted-syntax))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow all tabs ([no-tabs](http://eslint.org/docs/rules/no-tabs))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow ternary operators ([no-ternary](http://eslint.org/docs/rules/no-ternary))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow trailing whitespace at the end of lines ([no-trailing-spaces](http://eslint.org/docs/rules/no-trailing-spaces))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow dangling underscores in identifiers ([no-underscore-dangle](http://eslint.org/docs/rules/no-underscore-dangle))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow ternary operators when simpler alternatives exist ([no-unneeded-ternary](http://eslint.org/docs/rules/no-unneeded-ternary))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow whitespace before properties ([no-whitespace-before-property](http://eslint.org/docs/rules/no-whitespace-before-property))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce the location of single-line statements ([nonblock-statement-body-position](http://eslint.org/docs/rules/nonblock-statement-body-position))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent line breaks inside braces ([object-curly-newline](http://eslint.org/docs/rules/object-curly-newline))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing inside braces ([object-curly-spacing](http://eslint.org/docs/rules/object-curly-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce placing object properties on separate lines ([object-property-newline](http://eslint.org/docs/rules/object-property-newline))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce variables to be declared either together or separately in functions ([one-var](http://eslint.org/docs/rules/one-var))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow newlines around variable declarations ([one-var-declaration-per-line](http://eslint.org/docs/rules/one-var-declaration-per-line))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow assignment operator shorthand where possible ([operator-assignment](http://eslint.org/docs/rules/operator-assignment))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent linebreak style for operators ([operator-linebreak](http://eslint.org/docs/rules/operator-linebreak))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow padding within blocks ([padded-blocks](http://eslint.org/docs/rules/padded-blocks))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require quotes around object literal property names ([quote-props](http://eslint.org/docs/rules/quote-props))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce the consistent use of either backticks, double, or single quotes ([quotes](http://eslint.org/docs/rules/quotes))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require JSDoc comments ([require-jsdoc](http://eslint.org/docs/rules/require-jsdoc))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow semicolons instead of ASI ([semi](http://eslint.org/docs/rules/semi))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing before and after semicolons ([semi-spacing](http://eslint.org/docs/rules/semi-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require object keys to be sorted ([sort-keys](http://eslint.org/docs/rules/sort-keys))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require variables within the same declaration block to be sorted ([sort-vars](http://eslint.org/docs/rules/sort-vars))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing before blocks ([space-before-blocks](http://eslint.org/docs/rules/space-before-blocks))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing before function definition opening parenthesis ([space-before-function-paren](http://eslint.org/docs/rules/space-before-function-paren))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing inside parentheses ([space-in-parens](http://eslint.org/docs/rules/space-in-parens))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require spacing around infix operators ([space-infix-ops](http://eslint.org/docs/rules/space-infix-ops))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing before or after unary operators ([space-unary-ops](http://eslint.org/docs/rules/space-unary-ops))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing after the // or /* in a comment ([spaced-comment](http://eslint.org/docs/rules/spaced-comment))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow spacing between template tags and their literals ([template-tag-spacing](http://eslint.org/docs/rules/template-tag-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow Unicode byte order mark (BOM) ([unicode-bom](http://eslint.org/docs/rules/unicode-bom))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require parenthesis around regex literals ([wrap-regex](http://eslint.org/docs/rules/wrap-regex))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

## ECMAScript 6

These rules relate to ES6, also known as ES2015:

- ### Require braces around arrow function bodies ([arrow-body-style](http://eslint.org/docs/rules/arrow-body-style))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require parentheses around arrow function arguments ([arrow-parens](http://eslint.org/docs/rules/arrow-parens))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing before and after the arrow in arrow functions ([arrow-spacing](http://eslint.org/docs/rules/arrow-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce consistent spacing around * operators in generator functions ([generator-star-spacing](http://eslint.org/docs/rules/generator-star-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow arrow functions where they could be confused with comparisons ([no-confusing-arrow](http://eslint.org/docs/rules/no-confusing-arrow))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow duplicate module imports ([no-duplicate-imports](http://eslint.org/docs/rules/no-duplicate-imports))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow specified modules when loaded by import ([no-restricted-imports](http://eslint.org/docs/rules/no-restricted-imports))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unnecessary computed property keys in object literals ([no-useless-computed-key](http://eslint.org/docs/rules/no-useless-computed-key))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow unnecessary constructors ([no-useless-constructor](http://eslint.org/docs/rules/no-useless-constructor))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow renaming import, export, and destructured assignments to the same name ([no-useless-rename](http://eslint.org/docs/rules/no-useless-rename))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require let or const instead of var ([no-var](http://eslint.org/docs/rules/no-var))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow method and property shorthand syntax for object literals ([object-shorthand](http://eslint.org/docs/rules/object-shorthand))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require arrow functions as callbacks ([prefer-arrow-callback](http://eslint.org/docs/rules/prefer-arrow-callback))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require const declarations for variables that are never reassigned after declared ([prefer-const](http://eslint.org/docs/rules/prefer-const))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require destructuring from arrays and/or objects ([prefer-destructuring](http://eslint.org/docs/rules/prefer-destructuring))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Disallow parseInt() in favor of binary, octal, and hexadecimal literals ([prefer-numeric-literals](http://eslint.org/docs/rules/prefer-numeric-literals))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require rest parameters instead of arguments ([prefer-rest-params](http://eslint.org/docs/rules/prefer-rest-params))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require spread operators instead of .apply() ([prefer-spread](http://eslint.org/docs/rules/prefer-spread))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require template literals instead of string concatenation ([prefer-template](http://eslint.org/docs/rules/prefer-template))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce spacing between rest and spread operators and their expressions ([rest-spread-spacing](http://eslint.org/docs/rules/rest-spread-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Enforce sorted import declarations within modules ([sort-imports](http://eslint.org/docs/rules/sort-imports))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require symbol descriptions ([symbol-description](http://eslint.org/docs/rules/symbol-description))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow spacing around embedded expressions of template strings ([template-curly-spacing](http://eslint.org/docs/rules/template-curly-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```

- ### Require or disallow spacing around the * in yield* expressions ([yield-star-spacing](http://eslint.org/docs/rules/yield-star-spacing))

  > Why?

  ```javascript
  // Good.


  // Bad.

  ```
