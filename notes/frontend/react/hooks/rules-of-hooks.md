# Rules of hooks

> Hooks are plain functions that hook into React features without a class, and they must be called at the top level of a component or another hook.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 10–11)

## Key ideas
- **Hooks** are plain functions that let you **"hook into"** React features such as **state, side effects and context** without writing a class component.
- Examples: `useState`, `useEffect`, `useContext`, `useRef`, `useReducer`, `useMemo`, `useCallback`, `useNavigate`.
- **The 2 rules:**
  1. **Only call hooks at the top level**, never inside a condition, a loop or a nested function.
  2. **Only call hooks inside a React component or another hook.**
- Hooks only work inside components, which is part of what makes [functional components](../core/functional-vs-class-components.md) so powerful.
- Custom hooks (your own functions that call hooks) are how you share logic without [HOCs](../core/higher-order-components.md).

## Example
```jsx
function Profile({ showBio }) {
  const [name, setName] = useState("");      // ✅ top level
  const user = useContext(UserContext);      // ✅ top level

  if (showBio) {
    const [bio, setBio] = useState("");      // ❌ inside a condition
  }

  items.forEach(() => {
    useEffect(() => {});                     // ❌ inside a loop / nested fn
  });

  return <h2>{user.name}</h2>;
}

function helper() {
  useState(0);                               // ❌ not a component or hook
}
```

Fix for the conditional case: call the hook unconditionally, and put the condition inside it or in the JSX.

## Pitfalls
- A hook inside an `if` can run on one render and be skipped on the next. React then mixes up which state belongs to which hook.
- Calling a hook from an ordinary helper function or an event handler breaks rule 2.
- Hooks can't be used in class components at all.

## Related
- [useState](use-state.md)
- [useEffect](use-effect.md)
- [Higher-order components](../core/higher-order-components.md)
