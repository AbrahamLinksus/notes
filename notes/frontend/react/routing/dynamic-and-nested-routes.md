# Dynamic and nested routes

> `:id` in a path is a placeholder that `useParams` reads. `<Outlet />` marks where a matched child route renders inside a shared parent layout.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 23–24)

## Key ideas
- **Dynamic segment:** `:id` in `path="/products/:id"` matches whatever value sits in that part of the URL.
  - `/products/42` → `id = "42"`
  - `/products/apple` → `id = "apple"`
- **`useParams()`** reads the dynamic segments inside the matched component.
- `useParams` **always returns strings**, even for values that look like numbers.
- **`Outlet`** is the **placeholder where the child component renders**.
  - It sits inside a parent route's component and marks where a matched **child route** goes.
  - It enables **nested routes**: a shared layout (nav bars, sidebars, headers) stays in place while only the inner content swaps.
  - Child routes are declared by nesting `<Route>` elements inside a parent `<Route>`.

## Example
```jsx
// the route with a dynamic segment
<Route path="/products/:id" element={<ProductDetail />} />

// reading it inside the matched component
import { useParams } from 'react-router-dom';

function ProductDetail() {
  const { id } = useParams();
  return <h2>Product ID: {id}</h2>;
}
```

Nested routes with `Outlet` (layout sketch):
```
<Route path="/dashboard" element={<DashboardLayout />}>   ← nav + sidebar + <Outlet />
   <Route path="stats"    element={<Stats />} />          → /dashboard/stats
   <Route path="settings" element={<Settings />} />       → /dashboard/settings
</Route>

DashboardLayout
├── Sidebar   (stays)
└── <Outlet/> ← Stats or Settings swaps in here
```

## Pitfalls
- `id === 42` is false, because `id` is `"42"`. Convert explicitly (`Number(id)`) before comparing or doing maths.
- A parent layout without `<Outlet />` renders, but its child routes never appear.

## Related
- [React Router basics](react-router-basics.md)
- [Programmatic navigation](programmatic-navigation.md)
- [Next.js file-based routing](../../nextjs/file-based-routing.md)
