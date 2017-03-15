# Promises Usage Guide

## Creating Promises

The standard way for creating Promises is by using the `new Promise` constructor:

```javascript
// Pending state.
const promise = new Promise((resolve, reject) => { ... });
```

This creates a Promise in a `Pending` state which will need to be *settled* (can only be done once).

A Promise can be *settled* by calling:

- `resolve` to *settle* the Promise in a `Fulfilled` state. ✅
- `reject` to *settle* the Promise in a `Rejected` state. ❌

You can also create immediately resolved Promises using the following, although they are rarely needed:

```javascript
// Immediately resolved.
const promise = Promise.resolve(...);

// Immediately rejected.
const promise = Promise.reject(...);
```

## Consuming Promises

To consume a Promise, we attach a handler to the Promise using it's `.then()` method. This method takes a function that will be passed the resolved value of the Promise once it is fulfilled.

```javascript
const foo = 'foo';

function compare (a, b) {

    return new Promise((resolve, reject) => {

        if (a === b) {
            return resolve('Resolved!');
        }

        return reject('Rejected!');

    });

}

compare(foo, 'foo')

    // This will log Resolved!
    .then(msg => console.log(msg))

    // This will not be called.
    .catch(e => console.log(e));
```

## Dealing with Errors

To handle Promise errors, use the `.catch()` method. Note that when chaining Promises, the `.catch()` method will handle any rejection or thrown exceptions from either the original promise or any of it's handlers.

```javascript
const foo = 'foo';
const bar = 'bar'

function compare (a, b) {

    return new Promise((resolve, reject) => {

        if (a === b) {
            return resolve('Resolved!');
        }

        return reject('Rejected!');

    });

}

compare(foo, bar)

  // This will not be called.
  .then(msg => console.log(msg))

  // This will log Rejected!
  .catch(e => console.log(e));
```

## Promise Chaining

When working with multiple Promises in a *series* fashion, you can chain them together:

```javascript
function foo (param) {

    return new Promise((resolve, reject) => {

        if (typeof param !== 'undefined') {
            return resolve(param);
        }

        return reject('Rejected!');

    });

}

function compare (a, b) {

    return new Promise((resolve, reject) => {

        if (a === b) {
            return resolve('Resolved!');
        }

        return reject('Rejected!');

    });

}

foo('foo')
  .then(foo => compare(foo, 'foo'))

  // This will log Resolved!
  .then(msg => console.log(msg))

  // This will not be called.
  .catch(e => console.log(e));
```

When working with multiple Promises in a *parallel* fashion, you should use the `Promise.all()` method:

```javascript
function foo (param) {

    return new Promise((resolve, reject) => {

        if (typeof param !== 'undefined') {
            return resolve(param);
        }

        return reject('Rejected!');

    });

}

function bar (param) {

    return new Promise((resolve, reject) => {

        if (typeof param !== 'undefined') {
            return resolve(param);
        }

        return reject('Rejected!');

    });

}

function compare (a, b) {

    return new Promise((resolve, reject) => {

        if (a === b) {
            return resolve('Resolved!');
        }

        return reject('Rejected!');

    });

}

Promise.all([foo('foo'), bar('bar')])

  // Results are available as an array.
  .then(results => compare(results[0], results[1]))

  // This will not be called.
  .then(msg => console.log(msg))

  // This will log Rejected!
  .catch(e => console.log(e));
```
