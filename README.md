# redux-immutable-ops
---

[![Build Status](https://travis-ci.org/nitishkr88/redux-immutable-ops.svg?branch=master)](https://travis-ci.org/nitishkr88/redux-immutable-ops)
[![codecov.io](https://codecov.io/gh/nitishkr88/redux-immutable-ops/branch/master/graph/badge.svg)](https://codecov.io/gh/nitishkr88/redux-immutable-ops)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)

A collection of helper functions to perform immutable operations on plain JavaScript objects and arrays.
Works on the immutable update patters as defined by [Redux](https://redux.js.org/docs/recipes/reducers/ImmutableUpdatePatterns.html).

## Installation
```
npm install --save redux-immutable-ops
yarn add redux-immutable-ops
```

## Features

* Small
* [Lodash](https://lodash.com/) inspired API
* Conforms to [Redux](https://redux.js.org/docs/recipes/reducers/ImmutableUpdatePatterns.html) standards
* Interoperable with JavaScript
* Structural Sharing
* Typed with [Flow](https://flow.org/)

## Example Usage
 ```javascript

 ```

## API

### setIn(state: Object | Array<\*>, path: string, value: any): Object | Array<\*>

Returns an object, with the value at `path` set to `value`. `path` can be a dot-separated list of attribute
values to traverse. Index of array value which need to be updated can also be specified in the `path`. Paths not already
existing would be created.

```javascript
import { setIn } from "redux-immutable-ops"

const state = {
  foo: {
    bar: ['baz', { dog: 42 }]
  }
}

const result1 = setIn(state, 'tv.best.canines[0]', 'scooby')
expect(result1).not.toBe(state)
expect(result1).toEqual({
  foo: {
    bar: [
      'baz',
      {
        dog: 42
      }
    ]
  },

  tv: {
    best: {
      canines: ['scooby']
    }
  }
})

const result2 = setIn(state, 'foo.bar[0]', 'cat')
expect(result2).not.toBe(state)
expect(result2).toEqual({
  foo: {
    bar: [
      'cat',
      {
        dog: 42
      }
    ]
  }
})
```

### getIn(state: Object | Array<\*>, path: string): any

Returns the value specified by `path`. `path` can be a dot-separated list of attribute
values to traverse. Index of array value which need to be fetched can also be specified in the `path`.

```javascript
import { getIn } from "redux-immutable-ops"

const state = {
  foo: {
    bar: ['baz', { dog: 42 }]
  }
}

expect(getIn(state, 'foo.bar[0]')).toBe('baz')
expect(getIn(state, 'foo.bar[1].dog')).toBe(42)
```

### deleteIn(state: Object | Array<\*>, path: string): ?(Object | Array<\*>)

Returns a new object, without the key specified in `path`. `path` can be a dot-separated list of attribute
values to traverse. Index of array value which need to be deleted can also be specified in the `path`.

```javascript
import { deleteIn } from "redux-immutable-ops"

const state = ['the', 'quick', 'brown', 'fox']

expect(deleteIn(state, 0)).toEqual(['quick', 'brown', 'fox'])
expect(deleteIn(state, 0)).not.toBe(state)
expect(deleteIn(state, 2)).toEqual(['the', 'quick', 'fox'])
expect(deleteIn(state, 2)).not.toBe(state)

const state = {
  foo: {
    bar: ['baz', { dog: 42 }]
  }
}

const result1 = deleteIn(state, 'foo.bar[0]')
expect(result1).not.toBe(state)

expect(result1).toEqual({
  foo: {
    bar: [
      {
        dog: 42
      }
    ]
  }
})

```

### splice(array: Array<\*>, index: number, removeNum: number, value: any): Array<\*>

Similar to [Array.splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice), but returns a shallow copy.

```javascript
import { splice } from "redux-immutable-ops"

expect(splice(['b', 'c', 'd'], 0, 0, 'a')).toEqual(['a', 'b', 'c', 'd'])
expect(splice(['a', 'b', 'c'], 3, 0, 'd')).toEqual(['a', 'b', 'c', 'd'])
expect(splice(['a', 'b', 'd'], 2, 0, 'c')).toEqual(['a', 'b', 'c', 'd'])
expect(splice(['a', 'b', 'c', 'd'], 1, 1, 'e')).toEqual(['a', 'e', 'c', 'd'])
```

---
## License

MIT. See `LICENSE`
