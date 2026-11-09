# useEffect

> `useEffect` runs side effects (anything that isn't describing UI) after render. The dependency array controls when it runs, and the cleanup function stops leaks.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 14–15)

## Key ideas
- Lets a functional component run code that reaches **"outside" the normal render process**.
- A **side effect** is anything that isn't describing the UI: fetching data, setting timers, manual DOM manipulation.
- **Dependency array:**
  1. `[]` empty → runs **only once**, after the first render
  2. no array → runs after **every render**
  3. `[a, b]` → runs **when those elements change**
- **Cleanup function:** return a function from the effect.
  - It **prevents memory leaks**.
  - It **runs on unmount, or before the effect re-runs**.

## Example
```jsx
import { useEffect } from 'react';

useEffect(() => {
  // side-effect code goes here
}, [dependencyArray]);
```

With cleanup:
```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("tick");
  }, 1000);

  return () => {
    clearInterval(timer); // stops the timer
  };
}, []);
```

| Array | Runs |
|---|---|
| `[]` | once, on mount |
| none | every render |
| `[x]` | when `x` changes |

## Pitfalls
- Leaving the array out means every render, not once. A state update inside can then loop forever.
- No cleanup for intervals or subscriptions means they keep running after unmount, which is a memory leak.
- Missing a dependency in `[...]` means the effect keeps using old values.
- In Next.js server components you often don't need `useState` + `useEffect` for fetching at all. See [data fetching](../../nextjs/data-fetching-and-caching.md).

## Related
- [Component lifecycle](../core/component-lifecycle.md)
- [useState](use-state.md)
- [useRef](use-ref.md)
- [Next.js data fetching](../../nextjs/data-fetching-and-caching.md)
