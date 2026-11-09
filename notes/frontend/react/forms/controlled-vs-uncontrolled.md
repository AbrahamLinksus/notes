# Controlled vs uncontrolled components

> A controlled input's value lives in React state (`useState`). An uncontrolled input's value lives in the DOM (`useRef`).

studied: 2026-11-09 · status: done · source: React.pdf (pp. 10, 19, 22)

## Key ideas
- In React forms, **form elements are bound to React state**.
- **Controlled components:**
  - the input is **managed by React state**
  - built with **`useState`**, so every keystroke goes through `onChange` → setter → re-render
- **Uncontrolled components:**
  - the input is **managed by the DOM**
  - read with **`useRef`** when the value is needed
- **Handling events:** run a task when an event is triggered. Common ones are `onClick`, `onChange`, `onSubmit` and `onMouseOver`, all camelCase JSX props that take a function.

## Example
Controlled text input:

```jsx
import { useState } from "react";

const RegularInputExample = () => {
  const [name, setName] = useState("");

  return (
    <>
      <label htmlFor="name">Name:
        <input
          type="text"
          id="textInput"
          placeholder="Enter name"
          onChange={(e) => setName(e.target.value)}
        />
      </label>
      <p>Your name is {name}</p>
    </>
  );
};

export default RegularInputExample;
```

```
Controlled:    keystroke → onChange → setName → state → re-render → UI
Uncontrolled:  keystroke → DOM keeps value → read via ref.current when needed
```

## Pitfalls
- Pass a **function** to event props: `onClick={() => setCount(count + 1)}`. Writing `onClick={setCount(count + 1)}` calls it immediately during render.
- Mixing models (a `value` from state with no `onChange`) leaves an input that can't be typed in.
- A form `onSubmit` usually needs `e.preventDefault()` to stop the browser's full-page submit. See [programmatic navigation](../routing/programmatic-navigation.md).

## Related
- [Form inputs](form-inputs.md)
- [useState](../hooks/use-state.md)
- [useRef](../hooks/use-ref.md)
- [Yup validation](yup-validation.md)
