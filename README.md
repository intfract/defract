# Defract 
A modern JavaScript utility library that delivers functions for data structures, calculations, and more! 

Made by [intfract](https://github.com/intfract) 

## Install 

```sh
npm i defract
```

## Import 

### CJS

```js
const _ = require('defract')
```

### ESM

```js
import _ from "defract"
```

## Integrate 

Defract has over **40** methods. This module offers the powerful `_.must` and `_.countif` functions. It allows dynamic filtration and distillation of arrays of objects. More functions will be added to `defract` in the future, but some of the best are shown below. 

```js
console.log(_.chunk([0, 'text', [], {}], 3))
// [[0, 'text', []], [{}]]

console.log(_.eq([], []))
console.log(_.eq([0, 'text'], [0, 'text']))
console.log(_.eq([0, 'text', [], {}], [0, 'text', [], {}]))
console.log(_.eq({}, {}))
console.log(_.eq({ a: 0 }, { a: 0 }))
console.log(_.eq({ a: 0, b: [] }, { a: 0, b: [] }))
// true

const users = [
  {
    name: 'John',
    age: 18,
    deleted: false
  },
  {
    name: 'Jane',
    age: 13,
    deleted: false
  },
  {
    name: 'Bob',
    age: 69,
    deleted: true
  },
]

console.log(_.countif(users, '.age > 13'))
// 2
console.log(_.countif(users, ['&&', '.age > 13', '.deleted === false']))
// 1

console.log(_.ifelse(users, 'Yes', 'No', (item) => item.age > 13 ))
// ['Yes', 'No', 'Yes']

console.log(_.filter(users, _.must({ age: '> 16' })))
// [{ name: 'John', age: 18, deleted: false }, { name: 'Bob', age: 69, deleted: true }]
console.log(_.filter(users, { age: 13 })) // _.matches shorthand
// [{ name: 'Jane', age: 13, deleted: false }]
console.log(_.filter(users, ['name', 'John'])) // _.matchesProperty shorthand
// [{ name: 'John', age: 18, deleted: false }]
console.log(_.filter(users, 'deleted')) // _.property shorthand
// [{ name: 'Bob', age: 69, deleted: true }]

console.log(_.find(users, _.must({ age: '> 16' })))
// { name: 'John', age: 18, deleted: false }
console.log(_.find(users, { age: 13 })) // _.matches shorthand
// { name: 'Jane', age: 13, deleted: false }
console.log(_.find(users, ['name', 'John'])) // _.matchesProperty shorthand
// { name: 'John', age: 18, deleted: false }
console.log(_.find(users, 'deleted')) // _.property shorthand
// { name: 'Bob', age: 69, deleted: true }

console.log(_.findIndexes(users, _.must({ age: '> 16' })))
// [0, 2]
console.log(_.findIndexes(users, { age: 13 })) // _.matches shorthand
// [1]
console.log(_.findIndexes(users, ['name', 'John'])) // _.matchesProperty shorthand
// [0]
console.log(_.findIndexes(users, 'deleted')) // _.property shorthand
// [2]

console.log(_.distill(users, _.must({ age: ['&&', '>= 13', '<= 18'] })))
// [[John, Jane], [Bob]]
console.log(_.distill(users, { age: 13 })) // _.matches shorthand
// [[Jane], [John, Bob]]
console.log(_.distill(users, ['name', 'John'])) // _.matchesProperty shorthand
// [[John], [Jane, Bob]]
console.log(_.distill(users, 'deleted')) // _.property shorthand
// [[Bob], [John, Jane]]

console.log(_.unite([0, 'text', [], {}], [0, 'text'], [0, 'text', [], {}]))
// [0, 'text', [], {}, 0, 'text', 0, 'text', [], {}]
console.log(_.unite([0, 'text', [], {}], 'string'))
// [0, 'text', [], {}, 'string']

console.log(_.subtract([0, 'text', [], {}, [0, 1]], [0, []], [{}]))
// ['text', [0, 1]]

console.log(_.intersect([0, 'text', [], {}], [0, 'text'], ['text', {}]))
// ['text', 'text', 'text']

console.log(_.exclude([0, 'text', [], {}], [0, 'text'], ['text', {}]))
// [[]]

console.log(_.mapKeys({ apple: 'alpha', ball: 'beta' }, k => k[0]))
// { a: 'alpha', b: 'beta' }

console.log(_.mapValues({ apple: 'alpha', ball: 'beta' }, v => v[0]))
// { apple: 'a', ball: 'b' }

console.log(_.unique([0, 'text', [], {}, 'text', {}]))
// [0, 'text', [], {}]

for (let num of _.range(10, 0)) {
  console.log(num)
}
// 10 9 8 7 6 5 4 3 2 1
for (let num of _.range(0, 10, 2)) {
  console.log(num)
}
// 0 2 4 6 8 

console.log(_.search([[], {}, 'a', 'b', 'c'], {})) // binary search
// 1

console.log(_.shuffle([0, 1, 2, 3], 2))
// [2, 3, 0, 1]

console.log(_.zip(['id', 0, 1, 2], ['username', 'int', 'bob', 'npm']))
// [['id', 'username'], [0, 'int'], [1, 'bob'], [2, 'npm']]

console.log(_.indexes([0, 'text', [], {}, 'text', ['text']], 'text'))
// [1, 4]

console.log(_.last([0, 'text', [], {}]))
// {}
console.log(_.last(_.indexes([0, 'text', [], {}, 'text', ['text']], 'text')))
// 4

console.log(_.nth([0, 'text', [], {}], -1))
// {}

console.log(_.factors(-12))
// [1, -12, -1, 12, 2, -6, -2, 6, 3, -4, -3, 4]

console.log(_.perfectsq(4))
// true
console.log(_.perfectsq(1))
// true

console.log(_.prime(2))
// true
console.log(_.prime(1))
// false

console.log(_.insert([0, 'text', [], {}], 2, { a: 0 }))
// [0, 'text', { a: 0 }, [], {}]

console.log(_.fromPairs([['a', 0], ['b', []]]))
// { a: 0, b: [] }

console.log(_.iterate([['id', 0, 1, 2], ['username', 'int', 'bob', 'npm']], (a) => {
  return a
}))
// same output as _.zip(['id', 0, 1, 2], ['username', 'int', 'bob', 'npm'])

const space = _.ndarray(2, 3)
console.log(space)
/*
{
  length: 2,
  dimensions: 3,
  data: [
    [ 0, 0, 0 ],
    [ 1, 0, 0 ],
    [ 0, 1, 0 ],
    [ 1, 1, 0 ],
    [ 0, 0, 1 ],
    [ 1, 0, 1 ],
    [ 0, 1, 1 ],
    [ 1, 1, 1 ]
  ]
}
*/

console.log(_.ndindex([1, 0, 1], space.length))
// 5
console.log(space.data[_.ndindex([1, 0, 1], space.length)])
// [1, 0, 1]

console.log(_.ndpoint(5, space.length, space.dimensions))
// [1, 0, 1]

console.log(_.filter(['alpha', 'beta', 'gamma'], _.compare('????a'))) // ? = wildcard character 
// ['alpha', 'gamma']

console.log(_.random(0, 10))
// random single digit numbers 

console.log(_.choice(['alpha', 'beta', 'gamma']))
// random choice 

class X {
  constructor() {
    
  }
}

console.log(_.isPlainObject({ a: 0, b: [] })) // true
console.log(_.isPlainObject({})) // true
console.log(_.isPlainObject(new X())) // false

console.log(_.isEmptyObject({ a: 0, b: [] })) // false
console.log(_.isEmptyObject({})) // true
console.log(_.isEmptyObject(new X())) // false

console.log(_.isNumber(0)) // true
console.log(_.isNumber('0')) // false
console.log(_.isNumber(NaN)) // false

console.log(_.isPositive(1)) // true
console.log(_.isNegative(-1)) // true
```