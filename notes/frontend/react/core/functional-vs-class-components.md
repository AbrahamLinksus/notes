# Functional vs class components

> Components bundle UI and logic into reusable building blocks. Functional components with hooks are now preferred over class components.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 6–7)

## Key ideas
- **Components** encapsulate **business logic and UI**. They're **reusable and composable** and are the **building blocks** of React.
- **Functional components:**
  - plain JS functions
  - receive props and return JSX
  - **hooks** make them very powerful (state, effects, context and so on)
- **Class components:**
  - what was used **before hooks** were introduced
  - hold **state** and **lifecycle methods** to track the [component lifecycle](component-lifecycle.md)
- **Why functional is preferred:**
  1. dynamic and readable
  2. easier to test
  3. separated concerns

## Example
A functional component: a function in, JSX out.

```jsx
type ProfileProps = {
  name: string;
  age?: number;
};

const Profile: React.FC<ProfileProps> = ({ name, age }) => (
  <p>{name}, {age}</p>
);
```

Adding state is just a hook call:

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Clicked {count} times</button>;
}
```

## Pitfalls
- A functional component has no state of its own until it uses a hook like [useState](../hooks/use-state.md).
- Hooks only work inside functional components or other hooks, never in class components. See [rules of hooks](../hooks/rules-of-hooks.md).
- Class lifecycle methods map onto [useEffect](../hooks/use-effect.md) in functional components, so the logic moves rather than disappears.

## Related
- [Props vs state](props-vs-state.md)
- [Component lifecycle](component-lifecycle.md)
- [Rules of hooks](../hooks/rules-of-hooks.md)
- [Higher-order components](higher-order-components.md)
