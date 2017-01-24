# Idearium Node.js Style Guide

This is a guide for writing consistent and aesthetically pleasing Node.js code. It is inspired by what is popular within the community, and flavoured with some personal opinions.

It is licensed under the [CC BY-SA 3.0][cc] license. You are encouraged to fork this repository and make adjustments according to your preferences.

[cc]: http://creativecommons.org/licenses/by-sa/3.0/

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## 4 Spaces for indention

Use 4 **spaces** for indenting your code and swear an oath to never mix tabs and spaces - a special kind of hell is awaiting you otherwise.

## Newlines

Use UNIX-style newlines (`\n`), and a newline character as the last character of a file. Windows-style newlines (`\r\n`) are forbidden inside any repository.

## No trailing whitespace

Just like you brush your teeth after every meal, you clean up any trailing whitespace in your JS files before committing. Otherwise the rotten smell of careless neglect will eventually drive away contributors and/or co-workers.

## Use Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is a core value of our community. Consider the points of [the opposition][theopposition], but be a traditionalist when it comes to abusing error correction mechanisms for cheap syntactic pleasures.

[theopposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

## Use single quotes

Use single quotes, unless you are writing JSON.

*Right:*

```js
const foo = 'bar';
```

*Wrong:*

```js
const foo = "bar";
```

## Opening braces go on the same line

Your opening braces go on the same line as the statement.

*Right:*

```js
if (true) {
    console.log('winning');
}
```

*Wrong:*

```js
if (true)
{
    console.log('losing');
}
```

Also, notice the use of whitespace before and after the condition statement.

## Use lowerCamelCase for variables, properties and function names

Variables, properties and function names should use `lowerCamelCase`.  They should also be descriptive. Single character variables and uncommon abbreviations should generally be avoided.

*Right:*

```js
const adminUser = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
const admin_user = db.query('SELECT * FROM users ...');
```

## Use UpperCamelCase for class names

Class names should be capitalized using `UpperCamelCase`.

*Right:*

```js
class BankAccount() {
}
```

*Wrong:*

```js
class bankAccount() {
}
```

## Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote keys when your interpreter complains:

*Right:*

```js
const a = ['hello', 'world'];
const b = {
    good: 'code',
    'is generally': 'pretty',
};
```

*Wrong:*

```js
const a = [
    'hello', 'world'
];
const b = {"good": 'code'
        , is generally: 'pretty'
      };
```

Use

## Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use the triple equality operator as it will work just as expected.

*Right:*

```js
const a = 0;
if (a === '') {
    console.log('winning');
}

```

*Wrong:*

```js
const a = 0;
if (a == '') {
    console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

## Use multi-line ternary operator

The ternary operator should only be used on a single line for very basic assignment. Do not use multiple ternary operators, they are hard too read.

*Right:*

```js
const foo = (a === b) ? 1 : 2;
```

*Wrong:*

```js
const foo = (a === b)
    ? 1
    : 2;
```

*Wrong:*

```js
const tags = tags
    ? (this.tags ? this.tags.concat(this.tagFilter(tags)) : this.tagFilter(tags))
    : this.tags;
```

## Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will be forever grateful.

*Right:*

```js
const a = [];
if (!a.length) {
    console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = function() {
    return !this.length;
}

const a = [];
if (a.empty()) {
    console.log('losing');
}
```

## Whitespace in function body

Use whitespace on the first and last line of the function body, unless it's going to be a one line function.

*Right:*

```js
const toDegrees = angle => angle * (180 / Math.PI);
```

*Right:*

```js
const copy = (constants, terms) => {

    let copy = new Expression();

    copy.constants = constants.map((c) => c.copy());
    copy.terms = terms.map((t) => t.copy());

    return copy;

};
```

*Wrong:*

```js
const toDegrees = angle => {

    return angle * (180 / Math.PI);

}
```

*Wrong:*

```js
const copy = (constants, terms) => {
    let copy = new Expression();

    copy.constants = constants.map((c) => c.copy());
    copy.terms = terms.map((t) => t.copy());

    return copy;
}
```

## Write small functions

Keep your functions short. A good function fits on a slide that the people in the last row of a big room can comfortably read. So don't count on them having perfect vision and limit yourself to lines of code per function.

## Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible. The last return should be the default.

*Right:*

```js
const isPercentage = val => {

    if (val < 0) {
        return false;
    }

    if (val > 100) {
        return false;
    }

    return true;

}
```

*Wrong:*

```js
const isPercentage = val => {

    if (val >= 0) {
        if (val < 100) {
            return true;
        } else {
            return false;
        }
    } else {
        return false;
    }

}
```

Or for this particular example it may also be fine to shorten things even further:

```js
const isPercentage = val => (val >= 0 && val <= 100);
```

## Avoid if else statements

The devil invented if else, and unless you're a worshipper of his ways, be advised to avoid it.

*Right:*

```js
const isPercentage = val => {

    if (val < 0 || val > 100) {
        return false;
    }

    return true;

};
```

*Wrong:*

```js
const isPercentage = val => {

    if (val < 0) {
        return false;
    } else (val > 100) {
        return false;
    } else {
        return true;
    }

};
```

## Name your closures

Give your closures a name. It shows that you care about them, and will produce better stack traces, heap and cpu profiles.

*Right:*

```js
req.on('end', onEnd = () => console.log('winning'));
```

*Wrong:*

```js
req.on('end', () => console.log('losing'));
```

## Use slashes for comments

Use slashes for both single line and multi line comments. Try to write comments that explain higher level mechanisms or clarify difficult segments of your code. Don't use comments to restate trivial things.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE'', 'SOMETHING', 'VALUE']
const matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
const loadUser = (id, cb) => {
    // ...
}

const isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
    // ...
}
```

*Wrong:*

```js
// Execute a regex
const matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// Usage: loadUser(5, function() { ... })
const loadUser = (id, cb) => {
    // ...
}

// Check if the session is valid
const isSessionValid = (session.expires < Date.now());

// If the session is valid
if (isSessionValid) {
    // ...
}
```

## Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

## Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)

## Clarity is better than cleverness

Keep things simple. Keep things easy to read (really important). Make sure your code is easily comprehendible. Write code such that the most important communication they do is not to the computer that executes them but to the human beings who will read and maintain the source code in the future (including yourself).

This comes from the ['Basics of the Unix Philosophy handbook'][unixphilosophyruleofclarity].

[unixphilosophyruleofclarity]: http://www.faqs.org/docs/artu/ch01s06.html#id2877610
