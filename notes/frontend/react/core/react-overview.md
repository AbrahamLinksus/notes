# What is React

> React is a declarative, component-based JS library from Meta, and it updates the UI efficiently through a virtual DOM.

studied: 2026-11-09 · status: done · source: React.pdf (p. 1)

## Key ideas
- React is a **JavaScript library**, maintained by **Meta**.
- Related model: **MVC**, which stands for Model, View, Controller.
- It's **declarative**: I describe the UI in components and React handles updating the page.
- It's **component-based**: the UI is built from small, self-contained pieces.
- **Benefits:**
  - **Performance**: efficient updates through a [virtual DOM](virtual-dom.md).
  - **Reusability**: components encourage reuse, so one piece of UI can be used in many places with different props.

## Example
A page as a tree of components, each one reusable on its own:

```
App
├── Navbar
├── Page
│   ├── Profile   ({ name, age })
│   └── ProductList ({ products, searchTerm })
└── Footer
```

```jsx
function Profile({ name, age }) {
  return <p>{name}, {age}</p>;
}
```

When `Profile`'s data changes, React works out the smallest DOM change through the virtual DOM instead of reloading the page.

## Pitfalls
- React is a **library**, not a full framework. Routing, SSR and a compiler aren't built in, which is why [Next.js](../../nextjs/why-nextjs.md) exists.
- "Declarative" doesn't mean free. Re-renders still cost something, which is why keys, memoization and Fiber matter.

## Related
- [Virtual DOM](virtual-dom.md)
- [JSX](jsx.md)
- [Functional vs class components](functional-vs-class-components.md)
- [Why Next.js](../../nextjs/why-nextjs.md)
