# React Router basics

> React Router maps URL paths to components in a single-page app. `Link` changes the URL without a page reload, and `NavLink` adds an active state.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 22–23)

## Key ideas
- **SPA (single-page application):** one page, with components swapped as the URL changes.
- React Router **maps different URL paths to different components**.
- **`BrowserRouter`:** the outer wrapper that enables routing for everything nested inside it.
- **`Routes` + `Route`:** map paths to components. Only the **first matching** `Route` renders.
- **`Link to="..."`:** navigates **without a full page reload**. A plain `<a href>` triggers the browser's native navigation, which reloads everything and destroys app state. `Link` does a client-side URL update (`history.pushState`) and a re-render instead.
- **Catch-all:** `path="*"` as the **last** route acts as a 404 fallback.
- **`NavLink`** = `Link` + an **`isActive`** state option, handy for highlighting the current nav item.

## Example
```jsx
import { BrowserRouter, Routes, Route, Link, NavLink } from 'react-router-dom';

<BrowserRouter>
  <nav>
    <Link to="/">Home</Link>
    <NavLink
      to="/about"
      className={({ isActive }) => isActive ? "active-link" : ""}
    >
      About
    </NavLink>
  </nav>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/products/:id" element={<ProductDetail />} />
    <Route path="*" element={<NotFound />} />   {/* catch-all, must be last */}
  </Routes>
</BrowserRouter>
```

## Pitfalls
- `Link` takes **`to`**, not `href`. That's a common slip coming from Next.js `<Link href>`.
- Using `<a href>` for internal links reloads the page and wipes all React state.
- Put the `*` catch-all **last**, or it will swallow other routes.

## Related
- [Client vs server routing](client-vs-server-routing.md)
- [Dynamic and nested routes](dynamic-and-nested-routes.md)
- [Programmatic navigation](programmatic-navigation.md)
- [Next.js file-based routing](../../nextjs/file-based-routing.md)
