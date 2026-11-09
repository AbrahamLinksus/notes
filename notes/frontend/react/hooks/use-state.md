# useState

> `useState` gives a component a value plus a setter, and calling the setter is what triggers a re-render.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 10, 12–13, 17)

## Key ideas
- It's a way to **store data that can change over time** by adding a **state variable** to the component.
- It's a **hook**, so it only works inside components.
- It returns a **field and a setter**: `[state, setState]`.
- **Updating through the setter re-renders** the component. If the field is changed directly, the value changes but **React won't re-render**.
- **Functional updates** (`prev => prev + 1`) are preferred for **async updates or batches**.
- **Stale state problem:** the setter works from an **old value** instead of the current one. Functional updates avoid it.
- For **complex state** with several sub-values, use `useReducer` instead.

## Example
```jsx
const [state, setState] = useState(initialValue);
```

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  // ❌ direct change: value changes, no re-render
  // count = count + 1;

  return (
    <button onClick={() => setCount(count + 1)}>
      Clicked {count} times
    </button>
  );
}
```

Stale state vs a functional update:
```jsx
// both read the same old `count` → +1, not +2
setCount(count + 1);
setCount(count + 1);

// each gets the latest value → +2
setCount(prevCount => prevCount + 1);
setCount(prevCount => prevCount + 1);
```

## Pitfalls
- Mutating state directly (`count = 5`, `obj.x = 1`) doesn't trigger a re-render. Always use the setter.
- `setCount(count + 1)` inside async code or repeated calls can read a stale `count`. Prefer the functional form.
- Expensive initial values run on every render unless you use [lazy initialization](lazy-state-initialization.md).
- Objects and arrays need new copies, not in-place edits. See [objects and arrays in state](objects-and-arrays-in-state.md).

## Related
- [Lazy state initialization](lazy-state-initialization.md)
- [Objects and arrays in state](objects-and-arrays-in-state.md)
- [Props vs state](../core/props-vs-state.md)
- [Rules of hooks](rules-of-hooks.md)
