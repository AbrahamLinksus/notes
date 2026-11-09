# Prop drilling

> Prop drilling is passing props down through components that don't use them, just so they reach a deeply nested child.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 8–9)

## Key ideas
- **What it is:** props have to be passed through a hierarchy of components that have **no use for them**.
- **Why it's a problem:**
  - leads to **coupling**, since the middle components now depend on data they don't care about
  - **not scalable**
  - **hard to trace** where the data comes from
- **Solutions:**
  1. **Component composition**: pass components as children instead of threading data through.
  2. **Context API**: **globally shared state**, so values don't have to be passed down manually. See [useContext](../hooks/use-context.md).

## Example
```
Drilling:
App (user)
 └─ Layout (user)        ← doesn't use it, just forwards
     └─ Sidebar (user)   ← doesn't use it, just forwards
         └─ Avatar (user) ← actually uses it

With Context:
App  <UserContext.Provider value={user}>
 └─ Layout
     └─ Sidebar
         └─ Avatar   const user = useContext(UserContext);
```

```jsx
// Provide once near the top
<UserContext.Provider value={user}>
  <Page />
</UserContext.Provider>

// Any descendant grabs it directly
function Profile() {
  const user = useContext(UserContext);
  return <h2>{user.name}</h2>;
}
```

## Pitfalls
- Context is for genuinely global state such as theme, preferences and authentication. It doesn't replace every prop.
- A component that reads context must sit **inside** the matching `Provider`, or it won't see the value.
- Composition is often the simpler fix when only one or two levels are involved.

## Related
- [Props vs state](props-vs-state.md)
- [useContext](../hooks/use-context.md)
