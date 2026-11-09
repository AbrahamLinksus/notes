# Objects and arrays in state

> Never edit state objects or arrays in place. Build a new copy with the spread operator (or `filter`/`map`) and pass it to the setter.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 13–14)

## Key ideas
- The **spread operator** `...` can be used to **keep the previous values** while changing one part.
- Spread is a **JavaScript (ES6)** feature, not React.
- It **takes all the elements out of an object (or array) and spreads them individually** into a new one.
- **Arrays:**
  - add → spread the old array and append the new item
  - remove → `filter`
  - update → `map`, swapping in the updated item by id
- Always use the functional form `prev => …` so you work from the latest state.

## Example
Managing an array in state:

```js
// Add item
setList(prev => [...prev, newItem]);

// Remove item
setList(prev => prev.filter(item => item.id !== id));

// Update item
setList(prev =>
  prev.map(item =>
    item.id === updated.id ? updated : item
  )
);
```

Managing an object in state (form data):

```js
const [formData, setFormData] = useState({ username: "", email: "" });

// keep username, change only email
setFormData(prev => ({ ...prev, email: "new@mail.com" }));
```

## Pitfalls
- `list.push(item)` or `formData.email = x` mutates in place. React sees the same reference and **won't re-render**.
- `setFormData({ email: x })` without `...prev` **drops** every other field.
- Spread is shallow. Nested objects need their own spread at each level you change.

## Related
- [useState](use-state.md)
- [Keys in lists](../core/keys-in-lists.md)
- [Programmatic navigation](../routing/programmatic-navigation.md)
