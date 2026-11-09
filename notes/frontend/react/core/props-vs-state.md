# Props vs state

> Props are immutable configuration passed down from a parent. State is mutable data a component owns and manages itself.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 7–8)

## Key ideas
- **Props (properties)** are the mechanism for passing data **down from parent to child**.
- Props are **immutable**: the child reads them and doesn't change them.
- The same component is **reusable with different prop values**.
- **Props should be type-checked** for validation. TypeScript types do this.
- **Props vs state:**

| | Props | State |
|---|---|---|
| Source | parent | local (the component itself) |
| Mutability | immutable | mutable |
| Purpose | configuration | data management |

## Example
TypeScript validating the props of `Profile`:

```tsx
type ProfileProps = {
  name: string;
  age?: number;      // optional
};

const Profile: React.FC<ProfileProps> = ({ name, age }) => (
  <p>{name}, {age}</p>
);

// parent configures it, reused with different values:
<Profile name="Aditi" age={22} />
<Profile name="Sam" />
```

State, by contrast, lives in the component and changes over time:

```jsx
const [count, setCount] = useState(0);
```

## Pitfalls
- Don't mutate props inside the child. If a value needs to change, it's state, either here or in the parent.
- Without type checking, a wrong prop type (a string where a number is expected) passes silently.
- Passing props through many layers that don't use them is [prop drilling](prop-drilling.md).

## Related
- [Prop drilling](prop-drilling.md)
- [useState](../hooks/use-state.md)
- [Functional vs class components](functional-vs-class-components.md)
