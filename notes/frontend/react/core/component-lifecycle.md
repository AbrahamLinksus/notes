# Component lifecycle

> Every component goes through three phases: mounting, updating and unmounting. In functional components, `useEffect` covers all three.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 12, 15)

## Key ideas
- The **lifecycle** is the series of phases a component goes through:
  1. **Mounting**: created and inserted into the DOM.
  2. **Updating**: being re-rendered.
  3. **Unmounting**: removed from the DOM.
- [Class components](functional-vs-class-components.md) have dedicated **lifecycle methods** to track these phases.
- In functional components, [useEffect](../hooks/use-effect.md) does the same job through its dependency array and cleanup:
  - `[]` (empty): runs only once, after the first render, i.e. on **mount**.
  - no array: runs after **every** render, i.e. every **update**.
  - `[a, b]`: runs when `a` or `b` changes.
  - **cleanup function**: runs on **unmount** or before the effect re-runs.

## Example
A timer that starts on mount and is cleaned up on unmount:

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("tick");
  }, 1000);

  return () => {
    clearInterval(timer); // unmount: stop the timer
  };
}, []); // [] → mount only
```

```
mount    → effect runs, timer starts
update   → [] unchanged, effect doesn't re-run
unmount  → cleanup runs, timer cleared
```

## Pitfalls
- Forgetting the cleanup leaves timers or subscriptions running after unmount, which causes **memory leaks**.
- Leaving the dependency array out entirely means "run on every render", not "run once".
- Cleanup also runs **before each re-run**, not only on unmount.

## Related
- [useEffect](../hooks/use-effect.md)
- [Functional vs class components](functional-vs-class-components.md)
