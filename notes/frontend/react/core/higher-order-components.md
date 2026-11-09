# Higher-order components (HOC)

> A HOC is a function that takes a component as an argument and returns a modified one. Stacking many of them leads to wrapper hell, which hooks avoid.

studied: 2026-11-09 · status: done · source: React.pdf (p. 11)

## Key ideas
- **HOC:** a component is **passed as an argument** and a **modified component is returned**. It's the component version of a higher-order function.
- It was the way to share extra behaviour across components before hooks.
- **Wrapper hell:** when several HOCs are nested at once, the code becomes **hard to trace**. It's unclear which wrapper adds which prop or behaviour.
- **Hooks fix this.** Instead of wrapping, you create a hook and call it **inside** the component, so the logic stays visible where it's used.

## Example
Wrapping vs calling a hook (the HOC names here are just illustrations):

```jsx
// HOC style: Profile is wrapped three times
const EnhancedProfile = withAuth(withTheme(withLogger(Profile)));
// Where did `user` come from? Which wrapper set `theme`? → wrapper hell

// Hook style: the same needs, read directly inside
function Profile() {
  const user = useContext(UserContext);
  const [count, setCount] = useState(0);
  return <h2>{user.name}</h2>;
}
```

```
HOC tree:   withAuth → withTheme → withLogger → Profile   (4 layers)
Hook tree:  Profile                                       (1 layer)
```

## Pitfalls
- Deeply nested HOCs make debugging painful because the component tree fills up with wrappers.
- Hooks still follow the [rules of hooks](../hooks/rules-of-hooks.md): top level only, and only inside components or other hooks.

## Related
- [Rules of hooks](../hooks/rules-of-hooks.md)
- [Functional vs class components](functional-vs-class-components.md)
- [useContext](../hooks/use-context.md)
