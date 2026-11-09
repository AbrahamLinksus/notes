# useContext

> Create a context, wrap the tree in its `Provider`, and any descendant can read the value with `useContext` instead of receiving it through props.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 9, 16)

## Key ideas
- Used to **pass data deeply through components without passing it manually**. It's the fix for [prop drilling](../core/prop-drilling.md).
- **Use cases:** global state management such as **theme, preferences, authentication**.
- **Built from 2 parts:**
  1. `React.createContext()` creates the context, an empty "box" to reference later.
  2. `useContext()` reads it.
- In between, a **Provider** supplies the actual value. A child that wants the global state must be **wrapped in the `<Context.Provider>`** tag.

## Example
```jsx
// 1. Create the context
import { createContext } from 'react';
const UserContext = createContext();

// 2. Provide the data near the top of the tree
function App() {
  const user = { name: "Aditi" };
  return (
    <UserContext.Provider value={user}>
      <Page />
    </UserContext.Provider>
  );
}

// 3. Consume it in any descendant, however deep
import { useContext } from 'react';
function Profile() {
  const user = useContext(UserContext);
  return <h2>{user.name}</h2>;
}
```

Everything inside `<UserContext.Provider>`, no matter how deep, can access `user`.

## Pitfalls
- A component **outside** the Provider doesn't get the value.
- `createContext()` alone holds nothing useful. The value comes from the nearest `Provider`.
- Context is for genuinely shared, global data. Using it for everything hides where data comes from, the same problem prop drilling had.

## Related
- [Prop drilling](../core/prop-drilling.md)
- [Rules of hooks](rules-of-hooks.md)
- [Folder architecture](../architecture/folder-architecture.md)
