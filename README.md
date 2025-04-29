# ⚗️ filterclone

`filterclone` is a *very* tiny, zero-dependency JavaScript function for selectively deep-cloning and/or modifying the cloned DOM subtree.
It applies a filter function to control which nodes are cloned and included in the resulting subtree.

## Features

- Recursively clones DOM nodes with filtering logic
- Non-mutating: original DOM remains untouched
- Super lightweight and framework-agnostic

## Installation

```bash
npm install filterclone
```

Or simply use it via CDN:

```html
<script type="module">
  import filterclone from 'https://esm.sh/@camilaprav/filterclone';
</script>
```

## Usage

```js
<script type="module">
  import filterclone from 'https://esm.sh/@camilaprav/filterclone';

  let filtered = filterclone(document.body, x => {
    if (x.ELEMENT_NODE && x.tagName === 'SCRIPT') return;
    return x;
  });

  console.log(filtered.outerHTML);
</script>
```

The example above clones the body excluding all `<script>` tags.

## API

### `filterclone(root, filterFn)`

- **`root`**: `Node` - The root of the DOM subtree to clone.
- **`filterFn`**: `(node: Node, original: Node) => Node | falsy` - A function called on each node (including root) with its clone and original. Return the clone (or a modified version) to keep it, or falsy to exclude it from the final tree. Anything else will throw.

Returns: A cloned subtree root node, or `null` if the root itself was filtered out.

## Why?

Sometimes you need to deeply clone a DOM structure but with control over what gets included. `filterclone` gives you that flexibility without heavy dependencies or awkward tree-walking boilerplate.

Used in: [htmlsnap](https://github.com/camilaprav/htmlsnap) and [KittyGPT](https://github.com/camilaprav/kittygpt).

## Testing

This library is implicitly tested by the extensive test coverage found in [KittyGPT](https://github.com/camilaprav/kittygpt), which exercises all of its functionality.

---

## License

### ISC (Internet Systems Consortium)

filterclone is free software: you can redistribute it and/or modify it under the terms of the [ISC License](COPYING).

## Exclusion of warranty

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
