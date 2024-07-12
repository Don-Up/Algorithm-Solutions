#  implement Required`<T>

As the opposite of [Partial](https://bigfrontend.dev/typescript/implement-Partial-T), `Required<T>` sets all properties of `T` to required.

Please implement `MyRequired<T>` by yourself.

```ts
// all properties are optional
type Foo = {
  a?: string
  b?: number
  c?: boolean
}


const a: MyRequired<Foo> = {}
// Error

const b: MyRequired<Foo> = {
  a: 'BFE.dev'
}
// Error

const c: MyRequired<Foo> = {
  b: 123
}
// Error

const d: MyRequired<Foo> = {
  b: 123,
  c: true
}
// Error

const e: MyRequired<Foo> = {
  a: 'BFE.dev',
  b: 123,
  c: true
}
// valid
```

## Solution Approach



## Full Code

```ts
type MyRequired<T> = {
  [P in keyof T]-?:T[P]
}
```

