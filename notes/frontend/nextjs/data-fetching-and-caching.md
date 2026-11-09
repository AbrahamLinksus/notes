# Next.js data fetching and caching

> Because server components render on the server, they can fetch data directly, without `useState` + `useEffect`. Next.js caches that data automatically in its data cache.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 31–32)

## Key ideas
- **Plain React data fetching:** `useState()` + `useEffect()`. You fetch after render, store the result in state and re-render.
- **Next.js:** since components are **rendered on the server**, there's **no need to manage a state value or use `useEffect`** for fetching. It's cleaner.
- **Caching:**
  - Next.js **automatically stores data in its data cache**.
  - The cache is **customisable via parameters**.
  - This caching **only works in the data cache**.
- Whether a page is built ahead of time or per request depends on [static vs dynamic rendering](rendering-strategies.md).

## Example
Plain React (client):
```jsx
function Products() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('/api/products')
      .then(res => res.json())
      .then(setData);
  }, []);

  if (!data) return <p>Loading…</p>;
  return <ul>{data.map(p => <li key={p.id}>{p.name}</li>)}</ul>;
}
```

Next.js server component (sketch):
```
page.tsx (server component)
   └─ fetch data on the server ──► Next.js data cache (automatic)
   └─ render HTML with the data ──► browser
   (no useState, no useEffect, no loading flicker from client fetch)
```

```
React:    render empty → useEffect fetch → setState → re-render with data
Next.js:  fetch on server → render with data → send HTML
```

## Pitfalls
- Copying the `useState` + `useEffect` pattern into a server component fails, because hooks there need `'use client'`. See [server and client components](server-and-client-components.md).
- Cached data can be stale. Use the cache parameters when data must be fresh.
- The automatic caching applies to the **data cache** only, not to everything.

## Related
- [Rendering strategies](rendering-strategies.md)
- [Server and client components](server-and-client-components.md)
- [useEffect](../react/hooks/use-effect.md)
