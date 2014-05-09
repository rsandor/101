101
===

common utils / helpers that can be required selectively

## exists

Simple exists function

```js
var exists = require('101/exists');

exists('foo');     // true
exists(null);      // false
exists(undefined); // false
```

## findIndex

Just like ES6's array.findIndex

Finds the first value in the list that passes the given function (predicate) and returns it's index.
If list is not provided findIndex will return a partial-function which accepts a list as the first argument.

```js
var findIndex = require('101/find-index');
var arr = [1, 2, 3];

var index = findIndex(arr, function (val, i, arr) {
  return val === 2;
});
// returns 1
// returns -1 if not found
```

## hasKeypaths

Determines whether the keypaths exist and have the specified values.

```js
var hasKeypaths = require('101/has-keypaths');
var obj = {
  foo: {
    bar: {
      qux: 1
    }
  }
};

hasKeypaths(obj, ['foo.bar.qux']);      // true
hasKeypaths(obj, { 'foo.bar.qux': 1 }); // true
hasKeypaths(obj, ['foo.qux']);          // false
hasKeypaths(obj, { 'foo.bar': 2 });     // false
hasKeypaths(obj, { 'foo.bar': 1, 'nope': 1 }); // false

// optional 'deep' arg, defaults to true
var barObj = { bar: 1 };
hasKeypaths(obj, { 'foo.bar': barObj });         // true
hasKeypaths(obj, { 'foo.bar': barObj }, true);   // true
hasKeypaths(obj, { 'foo.bar': barObj }, false);  // false
hasKeypaths(obj, { 'foo.bar': obj.foo }, false); // true
hasKeypaths(obj, ['foo.bar'], false);            // true, uses [hasOwnProperty vs in](http://stackoverflow.com/questions/13632999/if-key-in-object-or-ifobject-hasownpropertykey)
```

## hasProperties

Determines whether the keys exist and, if specified, has the values.

```js
var hasProperties = require('101/has-properties');
var obj = {
  foo: {
    bar: 1
  },
  qux: 1
};

hasProperties(obj, ['foo', 'qux']); // true
hasProperties(obj, { qux: 1 }) // true

// optional 'deep' arg, defaults to true
var barObj = { bar: 1 };
hasProperties(obj, { 'foo.bar': barObj });         // true
hasProperties(obj, { 'foo.bar': barObj }, true);   // true
hasProperties(obj, { 'foo.bar': barObj }, false);  // false
hasProperties(obj, ['foo.bar'], false);            // true, uses [hasOwnProperty vs in](http://stackoverflow.com/questions/13632999/if-key-in-object-or-ifobject-hasownpropertykey)
```

## instanceOf

Functional version of JavaScript's instanceof, returns a
partial function which expects a value argument and returns

```js
var instanceOf = require('101/instance-of');

['foo', 'bar', 1].map(instanceOf('string')); // [true, true, false]
```

## isBoolean

Functional version of val typeof 'boolean'

```js
var isBoolean = require('101/is-boolean');

[true, false, 1].map(isBoolean); // [true, true, false]
```

## isFunction

Functional version of val typeof 'function'

```js
var isFunction = require('101/is-function');

[parseInt, function () {}, 'foo'].map(isFunction); // [true, true, false]
```

## isObject

Functional *strict* version of val typeof 'object' (and not array or regexp)

```js
var isObject = require('101/is-object');

[{}, { foo: 1 }, 100].map(isObject); // [true, true, false]
```

## isString

Functional version of val typeof 'string'

```js
var isObject = require('101/is-object');

[{}, { foo: 1 }, 100].map(isObject); // [true, true, false]
```

## last

Returns the last value of the item.

```js
var last = require('101/last');

last([1, 2, 3]); // 3
last('hello');   // 'o'
last({
  foo: 1,
  bar: 2
});              // 2
```

## pick

Returns a new object with the specified keys (with key values from obj)

```js
var pick = require('101/pick');
var obj = {
  foo: 1,
  bar: 2
};

pick(obj, 'foo');          // { foo: 1 }
pick(obj, ['foo']);        // { foo: 1 }
pick(obj, ['foo', 'bar']); // { foo: 1, bar: 2 }

// use it with array.map
[obj, obj, obj].map(pick('foo')); // [{ foo: 1 }, { foo: 1 }, { foo: 1 }];
```

## pluck

Functional version of obj[key], returns the value of the key from obj.

```js
var pluck = require('101/pluck');
var obj = {
  foo: 1,
  bar: 2
};

pluck(obj, 'foo'); // 1

// use it with array.map
[obj, obj, obj].map(pluck('foo')); // [1, 1, 1]
```
