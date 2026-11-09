# useMemo and useCallback

> `useMemo` caches a computed **result**, and `useCallback` caches a **function**. Both recompute only when their dependency array changes.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 17–18)

## Key ideas
- **`useMemo`:**
  - **memoizes a result** to avoid expensive recomputation on re-render
  - **recalculates only when its dependency array contents change**
- **`useCallback`:**
  - **returns a memoized version of a callback function**
  - in short, it **caches a function**
- Both take a dependency array, like [useEffect](use-effect.md).

## Example
```jsx
import { useMemo, useState } from 'react';

function ProductList({ products, searchTerm }) {
  const [count, setCount] = useState(0);

  const filteredProducts = useMemo(() => {
    console.log("Filtering ran");
    return products.filter(p =>
      p.name.toLowerCase().includes(searchTerm.toLowerCase())
    );
  }, [products, searchTerm]); // only re-run if these actually change

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Clicked {count} times</button>
      <ul>
        {filteredProducts.map(p => <li key={p.id}>{p.name}</li>)}
      </ul>
    </div>
  );
}
```

Clicking the button changes `count` and re-renders, but "Filtering ran" doesn't print, because `products` and `searchTerm` didn't change.

```
useMemo(() => compute(a, b), [a, b])   → cached value
useCallback(fn, [a, b])                → cached fn
```

## Pitfalls
- A missing dependency means a stale cached result.
- `useMemo` returns the **value**, while `useCallback` returns the **function**. Mixing them up is the classic mistake.
- For an expensive **initial** state only, [lazy initialization](lazy-state-initialization.md) is simpler.

## Related
- [Lazy state initialization](lazy-state-initialization.md)
- [useEffect](use-effect.md)
- [Keys in lists](../core/keys-in-lists.md)
