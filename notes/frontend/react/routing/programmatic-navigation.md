# Programmatic navigation

> When navigation has to happen from code (after a form submits, after an auth check), call the function returned by `useNavigate()` instead of rendering a link.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 23, 25)

## Key ideas
- Use it when a page navigation is needed **after an event other than a simple link click**.
- **`useNavigate()`** returns a function for redirecting from code: `navigate('/success')`.
- **Typical cases:**
  1. after a **form submission**
  2. based on **user authentication**
  3. after a **button click that isn't a simple link**
- Pattern: validate first, then navigate only on success.

## Example
```jsx
function SignupForm() {
  const navigate = useNavigate();
  const [formData, setFormData] = useState({ username: "", email: "" });
  const [errors, setErrors] = useState({});

  const handleSubmit = (e) => {
    e.preventDefault();
    const newErrors = validate();
    setErrors(newErrors);

    if (Object.keys(newErrors).length === 0) {
      console.log("Submitting:", formData);
      navigate('/welcome'); // redirect only after successful validation
    }
  };

  return <form onSubmit={handleSubmit}>{/* fields */}</form>;
}
```

```
submit → preventDefault → validate
          ├─ errors   → setErrors, stay on page
          └─ no errors → navigate('/welcome')
```

## Pitfalls
- Without `e.preventDefault()`, the browser does its own full-page form submit before your code can navigate.
- For a plain click-to-go-somewhere, use `<Link>`. `useNavigate` is for logic-driven redirects.
- `useNavigate` is a hook, so it's called at the top of the component and not inside the handler. See [rules of hooks](../hooks/rules-of-hooks.md).

## Related
- [React Router basics](react-router-basics.md)
- [Yup validation](../forms/yup-validation.md)
- [Controlled vs uncontrolled](../forms/controlled-vs-uncontrolled.md)
