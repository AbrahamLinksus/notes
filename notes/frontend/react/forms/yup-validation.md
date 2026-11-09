# Form validation with Yup

> Yup lets me define a schema for form data once, chain rules onto each field, and validate against it, either directly or through React Hook Form's `yupResolver`.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 26–27)

## Key ideas
- **Schema first:** `yup.object({...})` describes each field and its rules.
- **Validate:** `schema.validate(data)` returns a promise. `.then` gets the valid object, and `.catch` gets `err.errors`, an array of messages.
- **Types:** `string`, `number`, `boolean`, `date`, `array`, `object`, `mixed`.
- **Chaining:** `.required()`, `.min()`, `.max()`, `.email()`, `.positive()`, `.integer()`, `.matches(regex, msg)`. Each rule can take its own error message.
- **Nesting:** objects inside objects, and `yup.array().of(...)` for lists.
- **Custom rules:** `.test(name, message, fn)`, where `this.parent` gives access to sibling fields.
- **React Hook Form:** pass `yupResolver(schema)` to `useForm` and errors land in `formState.errors`.

## Example
```js
import * as yup from 'yup';

const passwordSchema = yup.string()
  .min(8, 'Password must be at least 8 characters')
  .matches(/[A-Z]/, 'Must contain an uppercase letter')
  .required('Password is required');

const schema = yup.object({
  startDate: yup.date().required(),
  endDate: yup.date().required().test(
    'is-after-start', 'End date must be after start date',
    function (value) { return value > this.parent.startDate; }
  ),
});
```

With React Hook Form:
```jsx
const { register, handleSubmit, formState: { errors } } =
  useForm({ resolver: yupResolver(schema) });

<form onSubmit={handleSubmit(onSubmit)}>
  <input {...register('email')} />
  <p>{errors.email?.message}</p>
</form>
```

## Pitfalls
- `.test()` needs a regular `function`, not an arrow function, because arrows don't get `this.parent`.
- `validate` is async. Forgetting `.catch` (or `try/await`) means errors go unhandled.
- `err.errors` is an **array**. Show every message (or map them per field), not just the first.

## Related
- [Controlled vs uncontrolled](controlled-vs-uncontrolled.md)
- [Form inputs](form-inputs.md)
- [Programmatic navigation](../routing/programmatic-navigation.md)
