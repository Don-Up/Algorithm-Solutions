# what is Composition? create a pipe()

what is Composition? It is actually not that difficult to understand, see [@dan_abramov 's explanation](https://whatthefuck.is/composition).

Here you are asked to create a `pipe()` function, which chains multiple functions together to create a new function.

Suppose we have some simple functions like this

```js
const times = (y) =>  (x) => x * y
const plus = (y) => (x) => x + y
const subtract = (y) =>  (x) => x - y
const divide = (y) => (x) => x / y
```

Your `pipe()` would be used to generate new functions

```js
pipe([
  times(2), // (x) => x * 2
  times(3)  // (x) => x * 3
])  
// x * 2 * 3

pipe([
  times(2),
  plus(3),
  times(4)
]) 
// (x * 2 + 3) * 4

pipe([
  times(2),
  subtract(3),
  divide(4)
]) 
// (x * 2 - 3) / 4
```

**notes**

1. to make things simple, functions passed to `pipe()` will all accept 1 argument

```js

/**
 * @param {Array<(arg: any) => any>} funcs 
 * @return {(arg: any) => any}
 */
function pipe(funcs) {
	// your code here
}
```

## Solution Approach

```js
const times = (y) => (x) => x * y;

const pipeFunc = pipe([
  times(2), // (x) => x * 2
  times(3)  // (x) => x * 3
]);  

pipeFunc(1); // 1 * 2 * 3
```

As we can see from the above example, `pipe` returns a function that serves as the initial value.

In the array of functions, the `x` of the first function is the initial value, the `x` of the second function is the result of the first function's computation, and so on.

We can use `reduce` to easily implement this chaining procedure.

## Full Code

```js


/**
 * @param {Array<(arg: any) => any>} funcs 
 * @return {(arg: any) => any}
 */
function pipe(funcs) {
	return function(initialValue){
		return funcs.reduce((value, func)=>func(value), initialValue)
	}
}
```



