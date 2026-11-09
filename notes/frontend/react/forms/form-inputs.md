# Form inputs: textarea, select, checkbox

> Every input type follows the same controlled pattern: a state value, `value`/`checked` bound to it, and `onChange` calling the setter. Only the field you read changes.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 19–21)

## Key ideas
- **Text area:** `value={bio}` plus `onChange` → `setBio(e.target.value)`.
- **Select (dropdown):** `value={fruit}` on the `<select>`. Options are rendered with `map`, each with a `key`.
- **Checkbox:** bind **`checked`**, not `value`, and read **`e.target.checked`** (true/false).
- The pattern is always state → bound attribute → `onChange` → setter. That makes them [controlled components](controlled-vs-uncontrolled.md).

## Example
```jsx
// Text area
const [bio, setBio] = useState("");
<textarea
  value={bio}
  onChange={(e) => setBio(e.target.value)}
  placeholder="Type something"
/>
<p>The typed content for bio is {bio}</p>

// Select
const allFruits = ["apple", "mango", "orange", "banana"];
const [fruit, setFruit] = useState("");
<select id="fruitInput" value={fruit}
        onChange={(e) => setFruit(e.target.value)}>
  {allFruits.map((current_fruit, idx) => (
    <option key={idx} value={current_fruit}>{current_fruit}</option>
  ))}
</select>
<p>The chosen fruit: {fruit}</p>

// Checkbox
const [isCheckedItem, setIsCheckedItem] = useState(false);
<input
  type="checkbox"
  checked={isCheckedItem}
  onChange={(e) => setIsCheckedItem(e.target.checked)}
/>
<p>The current chosen value is: {`${isCheckedItem}`}</p>
```

| Input | Bind | Read in `onChange` |
|---|---|---|
| text / textarea | `value` | `e.target.value` |
| select | `value` on `<select>` | `e.target.value` |
| checkbox | `checked` | `e.target.checked` |

## Pitfalls
- For a checkbox, `e.target.value` is not the on/off state. Use `e.target.checked`.
- My original checkbox example started with `useState("")`. A boolean (`false`) fits `checked` better.
- `key={idx}` is fine for a fixed option list but not for one that reorders. See [keys in lists](../core/keys-in-lists.md).

## Related
- [Controlled vs uncontrolled](controlled-vs-uncontrolled.md)
- [Keys in lists](../core/keys-in-lists.md)
- [Yup validation](yup-validation.md)
