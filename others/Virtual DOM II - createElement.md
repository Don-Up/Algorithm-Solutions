# Virtual DOM II - createElement

Suppose you have solved above problem, now let's take a look at [React.createElement()](https://reactjs.org/docs/react-api.html#createelement):

```js
React.createElement(  type,  [props],  [...children])
```

1. First argument is type, it could be set to Custom Component, but here in this problem, **it would only be HTML tag name**.
2. Second argument is props, here in this problem, it would only be the (common) camelCased HTML attributes.
3. the rest arguments are the children, which in React supports many data types, but in this problem, it only has the element type of MyElement, or string for TextNode.

**You are asked to create your own createElement() and render()**, so that following code could create the exact HTMLElement in [113. Virtual DOM I](https://bigfrontend.dev/problem/Virtual-DOM-I).

```js
const h = createElement
render(h(
  'div',
  {},
  h('h1', {}, ' this is '), // TextNode
  h(
    'p',
    { className: 'paragraph' },
    ' a ',
    h('button', {}, ' button '),
    ' from ',
    h('a', 
      { href: 'https://bfe.dev' }, 
      h('b', {}, 'BFE'),
      '.dev')
  )
))
```

**Notes**

1. The goal of this problem is not to create the replica of React implementation, you can have your own object representation format other than the one in [113. Virtual DOM I](https://bigfrontend.dev/problem/Virtual-DOM-I).
2. Details about ref, key are ignored here, they will be put in other problems. Re-render is not covered here, it will be in another problem as well.

## Solution Approach

```js
/**
 * MyElement is the type your implementation supports
 *
 * type MyNode = MyElement | string
 */

/**
 * It takes a type (HTML tag name), props(attributes), and children (elements or text nodes).
 * @param { string } type - valid HTML tag name
 * @param { object } [props] - properties.
 * @param { ...MyNode} [children] - elements as rest arguments
 * @return { MyElement }
 */
function createElement(type, props, ...children) {
  // It returns an object representing the element, with the type, props and children.
  return {
    type,
    props: props || {},
    children
  }
}

/**
 * It takes a virtual DOM element and creates the actual DOM element.
 * @param { MyElement }
 * @returns { HTMLElement } 
 */
function render(myElement) {
  // If the element is a string, it creates a text node
  if(typeof myElement === "string"){
    return document.createTextNode(myElement)
  }
	
  const {type, props, children} = myElement
  // It creates as HTML element using `document.createElement` for non-text nodes.
  const element = document.createElement(type)
  
  for(let [key, value] of Object.entries(props)){
    // It sets the attributes for the element, converting `className` to `class`
    if(key === "className"){
      key = "class"
    }
    element.setAttribute(key, value)
  }

  children.forEach(child => {
    // It recursively processes and appends the children to the created element.
    element.appendChild(render(child))
  })

  return element
}
```

