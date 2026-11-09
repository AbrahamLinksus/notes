# Server vs client components

> In the Next.js `app` folder every component is a server component by default. Add `'use client'` at the top of a file to make it a client component that runs in the browser.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 29, 31)

## Key ideas
- **All components in the `app` folder are server components by default.**
- **`'use client';`** at the **top of the file** marks it as a **client component**.
- **Server side (backend):** server components, **actions** and **route handlers**.
- **Client side (browser/frontend):** client components.
- Server-rendered components **cannot access browser events or state**. Anything that needs `onClick`, `useState` or `useEffect` has to be a client component.
- Server components can fetch data directly, with no `useState` + `useEffect` needed. See [data fetching](data-fetching-and-caching.md).

## Example
```tsx
// app/products/page.tsx: server component (default, no directive)
export default function ProductsPage() {
  return (
    <>
      <h1>Products</h1>
      <LikeButton />   {/* interactive bit lives in a client component */}
    </>
  );
}
```

```tsx
// app/products/LikeButton.tsx: client component
'use client';
import { useState } from 'react';

export default function LikeButton() {
  const [likes, setLikes] = useState(0);
  return <button onClick={() => setLikes(likes + 1)}>Likes: {likes}</button>;
}
```

```
Server (backend):  page.tsx, actions, route handlers  → no browser APIs
Client (browser):  'use client' files                 → state, events, effects
```

## Pitfalls
- Using `useState`, `useEffect` or `onClick` in a file without `'use client'` fails, because server components can't access browser events or state.
- `'use client'` must be the **first line** of the file.
- Don't mark everything as a client component. You lose SSR's smaller bundle and SEO benefits.

## Related
- [Rendering strategies](rendering-strategies.md)
- [Data fetching and caching](data-fetching-and-caching.md)
- [Why Next.js](why-nextjs.md)
