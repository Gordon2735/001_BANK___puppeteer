# Node: nextSibling property

The read-only **`nextSibling`** property of the [`Node`](https://developer.mozilla.org/en-US/docs/Web/API/Node) interface returns the node immediately following the specified one in their parent's [`childNodes`](https://developer.mozilla.org/en-US/docs/Web/API/Node/childNodes 'childNodes'), or returns `null` if the specified node is the last child in the parent element.

**Note:** Browsers insert [`Text`](https://developer.mozilla.org/en-US/docs/Web/API/Text) nodes into a document to represent whitespace in the source markup. Therefore a node obtained, for example, using [`Node.firstChild`](https://developer.mozilla.org/en-US/docs/Web/API/Node/firstChild) or [`Node.previousSibling`](https://developer.mozilla.org/en-US/docs/Web/API/Node/previousSibling) may refer to a whitespace text node rather than the actual element the author intended to get.

The article [Whitespace in the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Whitespace) contains more information about this behavior.

You can use [`Element.nextElementSibling`](https://developer.mozilla.org/en-US/docs/Web/API/Element/nextElementSibling) to obtain the next element skipping any whitespace nodes, other between-element text, or comments.

To navigate the opposite way through the child nodes list use [Node.previousSibling](https://developer.mozilla.org/en-US/docs/Web/API/Node/previousSibling).

## [Value](https://developer.mozilla.org/en-US/docs/Web/API/Node/nextSibling#value)

A [`Node`](https://developer.mozilla.org/en-US/docs/Web/API/Node) representing the next sibling of the current node, or `null` if there are none.

## [Example](https://developer.mozilla.org/en-US/docs/Web/API/Node/nextSibling#example)

```html
<div id="div-1">Here is div-1</div>
<div id="div-2">Here is div-2</div>
<br />
<output><em>Not calculated.</em></output>
```

```typescript
let el = document.getElementById('div-1').nextSibling;
let i = 1;

let result = 'Siblings of div-1:<br/>';

while (el) {
	result += `${i}. ${el.nodeName}<br/>`;
	el = el.nextSibling;
	i++;
}

const output = document.querySelector('output');
output.innerHTML = result;
```

play

## [Specifications](https://developer.mozilla.org/en-US/docs/Web/API/Node/nextSibling#specifications)
