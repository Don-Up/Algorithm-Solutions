# lit-html 1 - tagged templates

<audio src="assets/lit-html%201%20-%20tagged%20templates.mp3"></audio>

According to [lit-html homepage](https://lit-html.polymer-project.org/),

> lit-html lets you write HTML templates in JavaScript, then efficiently render and re-render those templates together with data to create and update DOM

[This video](https://www.youtube.com/watch?v=ruql541T7gc&feature=emb_title) explains how it works pretty well. Let's take a look at the example.

First, import html and render from lit-html. The helloTemplate function takes a name parameter and returns an HTML template string with the name interpolated.

This renders a div with "Hello Steve!" to the document body.

Then, it updates to "Hello Kevin!" but only updates the name part.

```js
import {html, render} from 'lit-html'
const helloTemplate = (name) => html`<div>Hello ${name}!</div>`

// This renders <div>Hello Steve!</div> to the document body
render(helloTemplate('Steve'), document.body)

// This updates to <div>Hello Kevin!</div>, but only updates the ${name} part
render(helloTemplate('Kevin'), document.body);
```

The magic happens in the second call of `render()` which only updates the necessary parts.

But there will be a series of problems on BFE.dev leading to that, here you are asked to :

**implement html() and render() to make above example work, without considering the rerender**, so html() could just return the raw HTML string.

The input data are all valid.

## Solution Approach

<audio src="assets/lit-html%201%20-%20tagged%20templates1.mp3"></audio>

To implement the `html` and `render` functions as described, we'll focus on creating a simple template system where `html` returns a string and `render` inserts that string into the specified container. Here's a basic implementation of these functions:

```javascript
// html() function to generate a template literal string
// strings refer to ['<div>Hello ', '!</div>'] in this case.
// values refer to `['Steve']` or `['Kevin']` in this case.
function html(strings, ...values) {
  // Combine the strings and values into a single HTML string
  return strings.reduce((result, str, i) => {
    // Append the current string and the corresponding value
    return result + str + (values[i] !== undefined ? values[i] : '');
  }, '');
}

// render() function to insert the HTML into a container
function render(result, container) {
  // Set the innerHTML of the container to the result
  container.innerHTML = result;
}
```

```js
// Example usage:
const helloTemplate = (name) => html`<div>Hello ${name}!</div>`;

// This renders <div>Hello Steve!</div> to the document body
render(helloTemplate('Steve'), document.body);

// This updates to <div>Hello Kevin!</div>, but only updates the ${name} part
render(helloTemplate('Kevin'), document.body);
```

### Explanation:

1. **`html` Function**:
   - The `html` function uses tagged template literals. It takes `strings` (an array of literal strings) and `values` (an array of values interpolated within the template).
   - The function combines these `strings` and `values` into a single string by using `reduce`. For each part, it appends the literal string and the corresponding value (if it exists).

2. **`render` Function**:
   - The `render` function takes the resulting HTML string from the `html` function and a container (an HTML element).
   - It sets the `innerHTML` of the container to the HTML string, effectively rendering it in the DOM.

### Example Walkthrough:
1. **Creating a Template**:
   ```javascript
   const helloTemplate = (name) => html`<div>Hello ${name}!</div>`;
   ```
   - This defines a template function `helloTemplate` that takes a `name` and returns an HTML string using the `html` function.

2. **Rendering the Template**:
   ```javascript
   render(helloTemplate('Steve'), document.body);
   ```
   - This call generates the HTML string `<div>Hello Steve!</div>` and sets it as the `innerHTML` of the `document.body`.

3. **Updating the Template**:
   ```javascript
   render(helloTemplate('Kevin'), document.body);
   ```
   - This call generates the HTML string `<div>Hello Kevin!</div>` and updates the `innerHTML` of the `document.body` to this new string.

This basic implementation covers the fundamental functionality needed to make the provided example work, focusing on generating and rendering HTML templates. More advanced features, like efficient re-rendering, can be added by further enhancing these functions.