# Create a simple store for DOM element

<audio src="assets/Create%20a%20simple%20store%20for%20DOM%20element.mp3"></audio>

We have `Map` in es6, so we could use any data as key, such as DOM element.

For example, you can use:

First, create a Map and set a DOM node as the key with some data as the value.

```js
const map = new Map()
map.set(domNode, somedata)
```

What if we need to support old JavaScript env like es5, how would you create your own Node Store as above?

You are asked to implement a Node Store, which supports DOM element as key.

```js
class NodeStore {
  set(node, value) {
  }
  
  get(node) {
  }
  
  has(node) {
  }
}

```

*note*

Map is disabled when judging your code, it is against the goal of practicing.

You can create a simple general Map polyfill. Or since you are asked to support specially for DOM element, what is special about DOM element?

What is the Time / Space cost of your solution?

## Solution Approach

To create a `NodeStore` class that supports using DOM elements as keys in a JavaScript environment that does not support ES6 `Map`, we need to consider the uniqueness of DOM elements. Since each DOM element has a unique identity and we can store additional properties directly on these elements, we can leverage this feature to implement our own store.

Here is an implementation of the `NodeStore` class:

```js
class NodeStore {
  constructor() {
    this.storeKey = Symbol('NodeStore');
  }

  /**
   * @param {Node} node
   * @param {any} value
   */
  set(node, value) {
    if (!node[this.storeKey]) {
      node[this.storeKey] = {};
    }
    node[this.storeKey].value = value;
  }

  /**
   * @param {Node} node
   * @return {any}
   */
  get(node) {
    return node[this.storeKey] ? node[this.storeKey].value : undefined;
  }

  /**
   * @param {Node} node
   * @return {Boolean}
   */
  has(node) {
    return !!node[this.storeKey];
  }
}

// Example usage
const nodeStore = new NodeStore();
const node1 = document.createElement('div');
const node2 = document.createElement('span');

nodeStore.set(node1, { some: 'data' });
console.log(nodeStore.get(node1)); // { some: 'data' }
console.log(nodeStore.has(node1)); // true
console.log(nodeStore.has(node2)); // false
```

### Explanation:

1. **Constructor:** We define a unique symbol `this.storeKey` to avoid potential naming conflicts with other properties that might be added to the DOM nodes. This symbol is used as a property key on the DOM nodes to store the associated value.

2. **Set Method:** The `set` method checks if the node already has a property with the `storeKey` symbol. If not, it initializes an object for storing the value. The value is then assigned to this property.

3. **Get Method:** The `get` method retrieves the value associated with the node if it exists. If the property does not exist, it returns `undefined`.

4. **Has Method:** The `has` method checks whether the node has a property with the `storeKey` symbol.

### Time / Space Complexity:

- **Time Complexity:** 
  - `set` method: O(1) - Adding a property to an object (DOM node) is a constant-time operation.
  - `get` method: O(1) - Accessing a property of an object is a constant-time operation.
  - `has` method: O(1) - Checking for the existence of a property on an object is a constant-time operation.

- **Space Complexity:** 
  - The space complexity depends on the number of DOM nodes and the size of the values being stored. Each node will have an additional property, but this is efficient in terms of space since we are not storing extra data structures like arrays or objects for mapping.

This implementation efficiently uses the uniqueness of DOM elements and their ability to store properties directly, providing a solution that works in environments without native `Map` support.