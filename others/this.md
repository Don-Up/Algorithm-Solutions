# this

What does the code snippet to the down output by `console.log`?

```js
const obj = {
  a: 1,
  b: function() {
    console.log(this.a)
  },
  c() {
    console.log(this.a)
  },
  d: () => {
    console.log(this.a)
  },
  e: (function() {
    return () => {
      console.log(this.a);
    }
  })(),
  f: function() {
    return () => {
      console.log(this.a);
    }
  }
}

console.log(obj.a)
obj.b()
;(obj.b)()
const b = obj.b
b()
obj.b.apply({a: 2})
obj.c()
obj.d()
;(obj.d)()
obj.d.apply({a:2})
obj.e()
;(obj.e)()
obj.e.call({a:2})
obj.f()()
;(obj.f())()
obj.f().call({a:2})
```

## Solution Approach

Here is the breakdown of what each `console.log` call will output:

1. `console.log(obj.a)`
    - Outputs: `1`
    - Explanation: `obj.a` is `1`.

2. `obj.b()`
    - Outputs: `1`
    - Explanation: `obj.b` is a regular function, so `this` refers to `obj`.

3. `;(obj.b)()`
    - Outputs: `1`
    - Explanation: This is the same as `obj.b()`. The semicolon doesn't affect the `this` binding.

4. `const b = obj.b; b()`
    - Outputs: `undefined`
    - Explanation: `b` is called in the global context, so `this` refers to the global object (or `undefined` in strict mode).

5. `obj.b.apply({a: 2})`
    - Outputs: `2`
    - Explanation: `this` is explicitly set to `{a: 2}`.

6. `obj.c()`
    - Outputs: `1`
    - Explanation: `obj.c` is a shorthand method, so `this` refers to `obj`.

7. `obj.d()`
    - Outputs: `undefined`
    - Explanation: `obj.d` is an arrow function, so `this` refers to the surrounding lexical context, which is the global object (or `undefined` in strict mode).

8. `;(obj.d)()`
    - Outputs: `undefined`
    - Explanation: This is the same as `obj.d()`. The semicolon doesn't affect the `this` binding.

9. `obj.d.apply({a: 2})`
    - Outputs: `undefined`
    - Explanation: `obj.d` is an arrow function, so `this` cannot be changed and remains the global object (or `undefined` in strict mode).

10. `obj.e()`
    - Outputs: `undefined`
    - Explanation: `obj.e` is an IIFE that returns an arrow function. The `this` inside the arrow function refers to the lexical scope of the IIFE, which is the global object (or `undefined` in strict mode).

11. `;(obj.e)()`
    - Outputs: `undefined`
    - Explanation: This is the same as `obj.e()`. The semicolon doesn't affect the `this` binding.

12. `obj.e.call({a: 2})`
    - Outputs: `undefined`
    - Explanation: The `this` inside the IIFE is not affected by the `call` method because it returns an arrow function. The arrow function's `this` still refers to the lexical scope of the IIFE.

13. `obj.f()()`
    - Outputs: `1`
    - Explanation: `obj.f` returns an arrow function. The `this` in `obj.f` refers to `obj`, so `this.a` is `1` inside the arrow function.

14. `;(obj.f())()`
    - Outputs: `1`
    - Explanation: This is the same as `obj.f()()`. The semicolon doesn't affect the `this` binding.

15. `obj.f().call({a: 2})`
    - Outputs: `1`
    - Explanation: The `this` in the arrow function returned by `obj.f` cannot be changed. It still refers to the `this` in `obj.f`, which is `obj`. Therefore, `this.a` is `1`.

So, the outputs in order are:

```plaintext
1
1
1
undefined
2
1
undefined
undefined
undefined
undefined
undefined
undefined
1
1
1

1
1
1
undefined
2
1
undefined
undefined
undefined
undefined
undefined
1
1
1
```