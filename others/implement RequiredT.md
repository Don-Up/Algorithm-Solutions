#  implement Required`<T>

<audio src="assets/implement%20Required.mp3"></audio>

As the opposite of [Partial](https://bigfrontend.dev/typescript/implement-Partial-T), `Required<T>` sets all properties of `T` to required.

Please implement `MyRequired<T>` by yourself.

For example:

When using the type Foo with optional properties and creating variables a, b, c, d, and e of type MyRequired Foo, you should see errors for all except variable e, which includes all required properties.

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

The task is to implement a TypeScript utility type `MyRequired<T>` that converts all optional properties of a given type `T` to required properties. This is the opposite of the `Partial<T>` utility type, which makes all properties optional.

### Understanding Required<T>

In TypeScript, the built-in `Required<T>` utility type transforms all properties of `T` to required. For example:

```ts
tsCopy codetype Foo = {
  a?: string;
  b?: number;
  c?: boolean;
};

type RequiredFoo = Required<Foo>;

// Equivalent to:
// type RequiredFoo = {
//   a: string;
//   b: number;
//   c: boolean;
// };
```

To implement `MyRequired<T>`, we need to achieve the same effect using TypeScript's advanced types.

### Steps to Implement MyRequired<T>

1. **Mapped Types**:
   - We use a mapped type to iterate over each property in `T`.
2. **Key Remapping with `-?` Modifier**:
   - In the mapped type, the `-?` modifier is used to remove the optional flag (`?`) from each property in `T`.
3. **Preserve Original Types**:
   - We ensure that the type of each property remains the same, but the property itself is no longer optional.

The syntax for mapped types in TypeScript allows us to iterate over all keys in `T` and apply transformations. Specifically, the `-?` modifier is used to remove the optional marker from properties.

### Implementation Details

- `keyof T`: Retrieves the keys of `T`.
- `[P in keyof T]`: Iterates over each key `P` in `T`.
- `-?`: Removes the optional marker from the property `P`.
- `T[P]`: Ensures the type of property `P` remains unchanged.

## Full Code

```ts
type MyRequired<T> = {
  [P in keyof T]-?:T[P]
}
```

### Example Usage

Here is how you can use the `MyRequired` type and see it in action:

```ts
tsCopy codetype Foo = {
  a?: string;
  b?: number;
  c?: boolean;
};

const a: MyRequired<Foo> = {};
// Error: Property 'a' is missing in type '{}' but required in type 'MyRequired<Foo>'.

const b: MyRequired<Foo> = {
  a: 'BFE.dev',
};
// Error: Property 'b' is missing in type '{ a: string; }' but required in type 'MyRequired<Foo>'.

const c: MyRequired<Foo> = {
  b: 123,
};
// Error: Property 'a' is missing in type '{ b: number; }' but required in type 'MyRequired<Foo>'.

const d: MyRequired<Foo> = {
  b: 123,
  c: true,
};
// Error: Property 'a' is missing in type '{ b: number; c: boolean; }' but required in type 'MyRequired<Foo>'.

const e: MyRequired<Foo> = {
  a: 'BFE.dev',
  b: 123,
  c: true,
};
// Valid
```

In this solution, `MyRequired<T>` successfully transforms all optional properties of type `T` to required properties. This ensures that any type passed through `MyRequired` will have all its properties as non-optional.
