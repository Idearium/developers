# Idearium JavaScript Style Guide

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
var foo = 'bar';
```

*Wrong:*

```js
var foo = "bar";
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
var adminUser = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
var admin_user = db.query('SELECT * FROM users ...');
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
class bank_Account() {
}
```

## Use UPPERCASE for Constants

Constants should be declared with `const` or static class properties, using all uppercase letters.

*Right:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const second = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote keys when your interpreter complains:

*Right:*

```js
var a = ['hello', 'world'];
var b = {
    good: 'code',
    'is generally': 'pretty',
};
```

*Wrong:*

```js
var a = [
    'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Promises

Always put `.then()` and `.catch()` on new lines.

*Right:*

```js
Model1.findById(model1Id).exec()
    .then((doc) => {

        doc.active = false;
        return doc.save();

    })
    .then(doc => log.info(doc, 'Doc saved'))
    .catch(e => log.error(e, 'An error occurred'));
```

*Wrong:*

```js
Model1.findById(model1Id).exec().then((doc) => {

    doc.active = false;
    return doc.save();

}).then(doc => log.info(doc, 'Doc saved')).catch((e) => {

    return log.error(e, 'An error occurred');

});
```

Where possible, don't nest promises.

*Right:*

```js
Model1.findById(model1Id).exec()
    .then(doc => Model2.findOne({ someRef: doc._id }).exec())
    .then((doc2) => {

        doc2.active = false;
        return doc2.save();

    })
    .then(() => log.info('User updated'))
    .catch(e => log.error(e, 'An error occurred'));
```

*Wrong:*

```js
Model1.findById(model1Id).exec()
    .then((doc) => {

      Model2.findOne({ someRef: doc._id }).exec()
          .then((doc2) => {

              doc2.active = false;
              doc2.save()
                  .then(log.info('User updated'));

          })

    })
    .catch(e => log.error(e, 'An error occurred'));
```

*Right:*

```js

Model1.findById(model1Id).exec()
    .then(doc => Model2.find({ someRef: doc._id }).exec())
    .then((docs) => {

        const updates = [];

        docs.forEach((doc) => {

            updates.push(new Promise((resolve, reject) => {

                doc.active = false;
                doc.save()
                    .then(savedDoc => resolve(savedDoc))
                    .catch(e => reject(e));

            }));

        });

        return updates;

    })
    .then(updates => Promise.all(updates))
    .then(results => log.info({ results }, 'All users updated'))
    .catch(e => log.error(e, 'An error occurred'));
```

*Wrong:*

```js
Model1.findById(model1Id).exec()
    .then((doc) => {

        Model2.find({ someRef: doc._id }).exec()
            .then((docs) => {

                docs.forEach((doc) => {

                    doc.active = false;
                    doc.save()
                        .then(savedDoc => log.info(savedDoc, 'Doc saved'))
                        .catch(e => log.error(e, 'An error occurred'));

                });

            })
            .catch(e => log.error(e, 'An error occurred'));

    })
    .catch(e => log.error(e, 'An error occurred'));
```

## Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use the triple equality operator as it will work just as expected.

*Right:*

```js
var a = 0;
if (a === '') {
    console.log('winning');
}

```

*Wrong:*

```js
var a = 0;
if (a == '') {
    console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

## Use multi-line ternary operator

The ternary operator should only be used on a single line for very basic assignment. If the assignment itself involves anything of length, it should be split up into multiple lines.

*Right:*

```js
var foo = (a === b) ? 1 : 2;
```

*Wrong:*

```js
var foo = (a === b)
    ? 1
    : 2;
```

*Right:*

```js
var tags = tags
    ? (this.tags ? this.tags.concat(this.tagFilter(tags)) : this.tagFilter(tags))
    : this.tags;
```

*Wrong:*

```js
var tags = tags ? (this.tags ? this.tags.concat(this.tagFilter(tags)) : this.tagFilter(tags)) : this.tags;
```

## Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will be forever grateful.

*Right:*

```js
var a = [];
if (!a.length) {
    console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = function() {
    return !this.length;
}

var a = [];
if (a.empty()) {
    console.log('losing');
}
```

## Whitespace in function body

Use whitespace on the first and last line of the function body, unless it's going to be a one line function.

*Right:*

```js
function toDegrees (angle) {
    return angle * (180 / Math.PI);
}
```

*Right:*

```js
function copy (constants, terms) {

    var copy = new Expression();

    copy.constants = constants.map((c) => c.copy());
    copy.terms = terms.map((t) => t.copy());

    return copy;

}
```

*Wrong:*

```js
function toDegrees (angle) {

    return angle * (180 / Math.PI);

}
```

*Wrong:*

```js
function copy (constants, terms) {
    var copy = new Expression();

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
function isPercentage(val) {

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
function isPercentage(val) {
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
function isPercentage(val) {
    return (val >= 0 && val <= 100);
}
```

## Avoid if else statements

The devil invented if else, and unless you're a worshipper of his ways, be advised to avoid it.

*Right:*

```js
function isPercentage(val) {

    if (val < 0 || val > 100) {
        return false;
    }

    return true;

}
```

*Wrong:*

```js
function isPercentage(val) {

    if (val < 0) {
        return false;
    } else (val > 100) {
        return false;
    } else {
        return true;
    }

}
```

## Name your closures

Give your closures a name. It shows that you care about them, and will produce better stack traces, heap and cpu profiles.

*Right:*

```js
req.on('end', function onEnd () {
    console.log('winning');
});
```

*Wrong:*

```js
req.on('end', function () {
    console.log('losing');
});
```

## Use slashes for comments

Use slashes for both single line and multi line comments. Try to write comments that explain higher level mechanisms or clarify difficult segments of your code. Don't use comments to restate trivial things.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE'', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
    // ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
    // ...
}
```

*Wrong:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
    // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());

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
