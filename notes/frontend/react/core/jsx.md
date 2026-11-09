# JSX

> JSX lets me write HTML-like markup with JavaScript embedded in it, and it's how components describe their UI.

studied: 2026-11-09 · status: done · source: React.pdf (p. 5)

## Key ideas
- **JSX = XML + JS.** In practice it's HTML with embedded JavaScript.
- JavaScript goes inside `{ }`: variables, expressions, `map` calls, inline handlers.
- **Attributes use camelCase**: `onClick`, `onChange`, `htmlFor`, `className`.
- **Nesting:** one component can be embedded inside another, just like HTML tags.
- Functional components **receive props and return JSX**.

## Example
Embedded JS, camelCase attributes and nesting together:

```jsx
const RegularInputExample = () => {
  const [name, setName] = useState("");

  return (
    <>
      <label htmlFor="name">Name:
        <input
          type="text"
          placeholder="Enter name"
          onChange={(e) => setName(e.target.value)}
        />
      </label>
      <p>Your name is {name}</p>
    </>
  );
};
```

Nesting a component inside another:

```jsx
<UserContext.Provider value={user}>
  <Page />
</UserContext.Provider>
```

`<> … </>` is a fragment. It groups siblings without adding an extra DOM node.

## Pitfalls
- HTML attribute names don't carry over as-is. It's `onClick`, not `onclick`, and `htmlFor` instead of `for`.
- Anything dynamic needs `{ }`. `value="bio"` is the literal string, while `value={bio}` is the variable.
- A component must return one root element. Wrap siblings in a fragment `<>…</>`.

## Related
- [Functional vs class components](functional-vs-class-components.md)
- [Controlled vs uncontrolled](../forms/controlled-vs-uncontrolled.md)
- [What is React](react-overview.md)
