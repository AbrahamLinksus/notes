# React folder architecture

> Pick the folder layout to match what has to scale: business features (feature-first), UI reuse (atomic design), or plain separation of concerns (layered, the default).

studied: 2026-11-09 · status: done · source: React.pdf (pp. 4–5)

## Key ideas
- **Feature-first / domain-driven:**
  - Use it when the app has to **scale around business features or domains**.
  - Each feature (auth, dashboard, …) gets its own isolated components, hooks, services and slice.
  - Pros: **clear separation of domains**, and it's **scalable**.
- **Atomic design:**
  - Use it when the system needs **high UI reusability** and a **strict separation of visual hierarchy**.
  - Pros: a clear **UI hierarchy** and **design consistency**.
- **Layered architecture:**
  - Use it when **separation of concerns** is the main need: components, logic, services and so on in separate layers.
  - This is the **default** starting point.

## Example
Feature-first:
```
src/
├── features/
│   ├── auth/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── authSlice.js
│   │   └── index.js
│   └── dashboard/
│       ├── components/
│       ├── pages/
│       └── dashboardSlice.js
├── app/
│   └── store.js
└── shared/
    ├── components/
    ├── utils/
    └── hooks/
```

Layered (default):
```
src/
├── components/   # dumb/presentational components
├── hooks/        # custom React hooks
├── services/     # API calls and integrations
├── pages/        # page-level components
├── utils/        # pure utility functions
├── constants/    # global constants
├── contexts/     # React Context providers
├── App.jsx
└── main.jsx
```

## Pitfalls
- In feature-first, anything used by more than one feature belongs in `shared/`. Otherwise features start importing from each other and lose their isolation.
- Layered is fine for small apps, but as features grow each layer folder gets crowded. That's the signal to move to feature-first.
- Atomic design is about **UI** structure. It doesn't say where business logic or API calls go.

## Related
- [Functional vs class components](../core/functional-vs-class-components.md)
- [useContext](../hooks/use-context.md)
