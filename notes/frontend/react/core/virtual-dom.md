# Virtual DOM

> React keeps two copies of the DOM in memory, compares them, and writes only the differences to the real DOM.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 1–2)

## Key ideas
- **The problem:** with the plain HTML DOM, an update in one component makes the browser re-render the whole page. That's a **performance penalty**.
- **React's fix:** keep **2 copies of the DOM in memory**, the **current** one and the **previous** one.
- They live in memory, so updating them is much faster than touching the real DOM.
- **Flow:**
  1. Changes are made to the current copy.
  2. The current copy is compared to the previous one.
  3. Only the changes are applied to the main (real) DOM.
- The comparison step is called [reconciliation](reconciliation-and-diffing.md).

## Example
```
setCount(count + 1)
        │
        ▼
current VDOM (new) ──compare── previous VDOM (old)
        │
        ▼
diff: <button> text "Clicked 3 times" → "Clicked 4 times"
        │
        ▼
real DOM: patch only that text node; nothing else is re-rendered
```

The HTML DOM itself is a tree: `Document → <html> → <head>/<body> → <title>, <link>, <img>, <p> …`. The virtual DOM mirrors that tree in memory.

## Pitfalls
- The virtual DOM isn't a second browser DOM. It's React's in-memory copy, and the browser only ever sees the real one.
- React still has to compare the two trees, so it isn't free. The win is that it touches far fewer real DOM nodes.
- Bad keys or wrapper-type changes can make the diff throw away more of the tree than it needs to. See [keys in lists](keys-in-lists.md).

## Related
- [Reconciliation and diffing](reconciliation-and-diffing.md)
- [React Fiber](react-fiber.md)
- [Browser rendering](../../../backend/web-fundamentals/browser-rendering.md)
