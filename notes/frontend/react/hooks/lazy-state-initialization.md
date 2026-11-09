# Lazy state initialization

> Pass `useState` a function instead of a value, and an expensive initial computation runs only once instead of on every render.

studied: 2026-11-09 · status: done · source: React.pdf (p. 13)

## Key ideas
- **Problem:** `useState(computeExpensiveValue())` calls the function on **every render**. React ignores the result after the first render, but the heavy work still runs every time.
- **Solution:** pass a **function** to `useState`, as in `useState(() => computeExpensiveValue())`. It **only runs once**.
- **How it works:**
  1. During **mount**, React sees the argument is a function, calls it, and stores the returned value as the state.
  2. On every **re-render**, React only sees the stored returned value, which is kept in a **fiber**. The function isn't called again.
- Use it for expensive state setup: heavy computations, parsing large data and so on.

## Example
```js
// ❌ runs computeExpensiveValue() on every render
const [value, setValue] = useState(computeExpensiveValue());

// ✅ runs only on mount
const [value, setValue] = useState(() => computeExpensiveValue());
```

```
render 1 (mount):  useState(fn) → React calls fn() → stores result in fiber
render 2:          useState(fn) → React reads stored value, fn NOT called
render 3:          useState(fn) → React reads stored value, fn NOT called
```

## Pitfalls
- `useState(computeExpensiveValue())` with the parentheses is **not** lazy, because the call happens before `useState` even sees it. Pass the function: `() => compute…()`.
- Lazy init only covers the **initial** value. For an expensive value derived from changing props or state, use [useMemo](use-memo-and-use-callback.md).

## Related
- [useState](use-state.md)
- [useMemo and useCallback](use-memo-and-use-callback.md)
- [React Fiber](../core/react-fiber.md)
