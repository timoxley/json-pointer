# json-pointer

[![Build Status](https://travis-ci.org/manuelstofer/json-pointer.png)](https://travis-ci.org/manuelstofer/json-pointer)


Some utilities for JSON pointers described by RFC 6901

Provides some additional stuff i needed but is not included in [node-jsonpointer](https://github.com/janl/node-jsonpointer)


## Installation

[node.js](http://nodejs.org)
```bash
$ npm install json-pointer
```

[component](https://github.com/component/component)
```bash
$ component install manuelstofer/json-pointer
```

## API

```Javascript
var pointer = require('json-pointer');
```


### .get(object, pointer)

Looks up a json pointer in an object

```Javascript
var obj = {
    example: {
        bla: 'hello'
    }
};
pointer.get(obj, '/example/bla');
```



### .set(object, pointer, value)

Sets a new value on object at the location described by pointer

```Javascript
var obj = {};
pointer.set(obj, '/example/bla', 'hello');
```


### .dict(object)

Creates a dictionary object (pointer -> value)

```Javascript
var obj = {
    hello: {bla: 'example'}
};
pointer.dict(obj);

// Returns:
// {
//    '/hello/bla': 'example'
// }
```


### .walk(object, iterator)

Just like:
```Javascript
each(pointer.dict(obj), iterator);
```


### .has(object, pointer)

Tests if an object has a value for a json pointer

```Javascript
var obj = {
    bla: 'hello'
};

pointer.has(obj, '/bla');               // -> true
pointer.has(obj, '/non/existing');      // -> false
```



### .escape(str)

Escapes a reference token

```Javascript
pointer.escape('hello~bla');            // -> 'hello~0bla'
pointer.escape('hello/bla');            // -> 'hello~1bla'
```



### .unescape(str)

Unescape a reference token

```Javascript
pointer.unescape('hello~0bla');         // -> 'hello~bla'
pointer.unescape('hello~1bla');         // -> 'hello/bla'
```


### .parse(str)

Converts a json pointer into a array of reference tokens

```Javascript
pointer.parse('/hello/bla');            // -> ['hello', 'bla']
```


### .compile(str)

Builds a json pointer from a array of reference tokens

```Javascript
pointer.compile(['hello', 'bla']);      // -> '/hello/bla'
```
