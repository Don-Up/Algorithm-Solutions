# Detect data type in JavaScript

This is an easy problem.

For [all the basic data types](https://javascript.info/types) in JavaScript, how could you write a function to detect the type of arbitrary data?

Besides basic types, you need to also handle also commonly used complex data type including `Array`, `ArrayBuffer`, `Map`, `Set`, `Date` and `Function`

The goal is not to list up all the data types but to show us how to solve the problem when we need to.

The type should be lowercase

```js
detectType(1) // 'number'
detectType(new Map()) // 'map'
detectType([]) // 'array'
detectType(null) // 'null'

// more in judging step
```

## Solution Approach

In JavaScript, data types are generally divided into primitive types and object types. 

There are some complex cases that need to be handled, such as `null` being a primitive type, but `typeof null` returning 'object', as well as several special object types like `Function`, `Date`, `Map`, and `Set`.

In general, we can use `typeof` to check primitive data types and `Object.prototype.toString.call` to check object data types.

First, we check if `data` is equal to `null` and return `"null"` if it is.

```js
if (data === null) {
    return 'null';
}
```

Next, we call `typeof` on `data` and assign the result to a string `type`. If `type` is not equal to `"object"`, we return `type`.

After that, we need to handle special objects like `Function` and `Map`. We call `Object.prototype.toString.call` with `data` to get the `typeString`. `typeString` shoud be  comprised of square brackets, `object` and a specific type, so we can check it using regex.

```js
const typeString = Object.prototype.toString.call(data);
const match = typeString.match(/\[object (\w+)\]/);
```

We call `typeString.match` and get the `match`. If `match` is not null, we return `match[1].toLowerCase()`

```js
if (match) {
    // Convert the matched type to lowercase
    return match[1].toLowerCase();
}
```

So far, we have handled `null`, primitive data types, and special objects. The only remaining case is regular objects, so we can return `"object"` to finish this function.

## Full Code

```js
function detectType(data) {
    if (data === null) {
        return 'null';
    }

    const type = typeof data;
    if (type !== 'object') {
        return type;
    }

    // For object types, use Object.prototype.toString
    const typeString = Object.prototype.toString.call(data);
    const match = typeString.match(/\[object (\w+)\]/);

    if (match) {
        // Convert the matched type to lowercase
        return match[1].toLowerCase();
    }

    // Default case, if no match is found
    return 'object';
}
```

