# Next.js file-based routing

> In Next.js the folder structure *is* the router. Each folder is a URL segment, and its `page.tsx` is what renders there.

studied: 2026-11-09 · status: done · source: React.pdf (p. 30)

## Key ideas
- Next.js follows **file-based routing**: the **file and folder structure inside the project directory dictates the website's URLs**.
- **`page.tsx` is the entry point** of a folder, and it's what renders for that URL.
- **If `page.tsx` doesn't exist** for a path, the result is **404 Not Found**.
- No separate route config is needed, unlike React Router's `<Routes>`/`<Route>`.
- Components inside the `app` folder are [server components by default](server-and-client-components.md).

## Example
```
app/
├── page.tsx              → /
├── about/
│   └── page.tsx          → /about
├── products/
│   └── page.tsx          → /products
└── dashboard/
    ├── settings/
    │   └── page.tsx      → /dashboard/settings
    └── (no page.tsx)     → /dashboard → 404 Not Found
```

Compared with React Router:
```
React Router:  <Route path="/about" element={<About />} />   (declared in code)
Next.js:       app/about/page.tsx                            (declared by folders)
```

## Pitfalls
- A folder without `page.tsx` isn't a page. Visiting it gives a 404 even if other files sit there.
- Renaming or moving a folder changes the public URL, so links elsewhere can break.
- Next.js's `<Link>` uses `href`, while React Router's uses `to`. See [React Router basics](../react/routing/react-router-basics.md).

## Related
- [Why Next.js](why-nextjs.md)
- [React Router basics](../react/routing/react-router-basics.md)
- [Server and client components](server-and-client-components.md)
