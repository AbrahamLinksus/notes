# useRef

> `useRef` gives a mutable box (`.current`) that survives re-renders, and changing it does **not** cause a re-render.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 16–17)

## Key ideas
- Lets you reference a value that **persists across renders without causing a re-render** when it's updated.
- It gives a **"box" holding a mutable value**. React doesn't track it as state.
- `useRef` returns an object with exactly one property: **`.current`**. You read and write the value through it.
- Used for **values that don't affect the UI**.
- **Uses:**
  1. avoid re-renders while still keeping track of a value
  2. interface with 3rd-party libraries
  3. access and manipulate **DOM elements/nodes**
  4. store **interval or timeout IDs**
- In forms, [uncontrolled inputs](../forms/controlled-vs-uncontrolled.md) (managed by the DOM) are read through `useRef`.

## Example
```jsx
import { useRef } from 'react';

const myRef = useRef(initialValue);
console.log(myRef);          // { current: initialValue }

myRef.current = 5;
console.log(myRef.current);  // 5, and no re-render happened
```

| | `useState` | `useRef` |
|---|---|---|
| Changing it re-renders? | yes | no |
| Read/write | `value` / `setValue` | `.current` |
| Good for | data shown in UI | IDs, DOM nodes, values not shown |

## Pitfalls
- Showing `ref.current` in JSX won't update the screen when it changes, because no re-render happens. If the UI depends on it, use [useState](use-state.md).
- Read and write `.current`, not the ref itself. `myRef = 5` replaces the box and loses it.

## Related
- [useState](use-state.md)
- [useEffect](use-effect.md)
- [Controlled vs uncontrolled](../forms/controlled-vs-uncontrolled.md)
