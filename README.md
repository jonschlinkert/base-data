# base-data [![NPM version](https://badge.fury.io/js/base-data.svg)](http://badge.fury.io/js/base-data)

> adds a `data` method to base-methods.

Adds a `data` method to [base-methods](https://github.com/jonschlinkert/base-methods) that can be used for setting, getting and loading data onto a specified object in your application.

## Install

Install with [npm](https://www.npmjs.com/)

```sh
$ npm i base-data --save
```

## Usage

```js
var Base = require('base-methods');
var data = require('base-data');

// create your application and inherit `Base`
function App() {
  Base.call(this);
}
Base.extend(App);
var app = new App();

// add the `data` method to `App`
// note that `data()` is a function that is called 
app.mixin('data', data());

// set/get/load data
app.data('foo', 'bar');
app.data({a: 'b'});
console.log(app.cache.data);
//=> {foo: 'bar', a: 'b'}
```

## Glob patterns

Glob patterns may be passed as a string or array. All of these work:

```js
app.data('foo.json');
app.data('*.json');
app.data(['*.json']);
// pass options to node-glob
app.data(['*.json'], {dot: true});
```

## Namespacing

Namespacing allows you to load data onto a specific key, optionally using part of the file path as the key.

**Example**

Given that `foo.json` contains `{a: 'b'}`:

```js
app.data('foo.json');
console.log(app.cache.data);
//=> {a: 'b'}

app.data('foo.json', {namespace: true});
console.log(app.cache.data);
//=> {foo: {a: 'b'}}

app.data('foo.json', {
  namespace: function(fp) {
    return path.basename(fp);
  }
});
console.log(app.cache.data);
//=> {'foo.json': {a: 'b'}}
```

## API

### [.data](index.js#L28)

**Params**

* `key` **{String|Object}**: Pass a key-value pair or an object to set.
* `val` **{any}**: Any value when a key-value pair is passed. This can also be options if a glob pattern is passed as the first value.
* `returns` **{Object}**: Returns an instance of `Templates` for chaining.

**Example**

```js
app.data('a', 'b');
app.data({c: 'd'});
console.log(app.cache.data);
//=> {a: 'b', c: 'd'}
```

## Related projects

* [base-methods](https://www.npmjs.com/package/base-methods): Starter for creating a node.js application with a handful of common methods, like `set`, `get`,… [more](https://www.npmjs.com/package/base-methods) | [homepage](https://github.com/jonschlinkert/base-methods)
* [base-options](https://www.npmjs.com/package/base-options): Adds an `option` method to base-methods. | [homepage](https://github.com/jonschlinkert/base-options)
* [class-utils](https://www.npmjs.com/package/class-utils): Utils for working with JavaScript classes and prototype methods. | [homepage](https://github.com/jonschlinkert/class-utils)

## Running tests

Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/base-data/issues/new).

## Author

**Jon Schlinkert**

+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2015 Jon Schlinkert
Released under the MIT license.

***

_This file was generated by [verb-cli](https://github.com/assemble/verb-cli) on October 12, 2015._