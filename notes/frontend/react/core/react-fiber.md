# React Fiber

> Fiber splits rendering into small units of work, so React can pause, prioritise and resume rendering instead of doing the whole tree in one go.

studied: 2026-11-09 · status: done · source: React.pdf (p. 3)

## Key ideas
- **Incremental rendering:** instead of rendering the entire component tree in one go, Fiber breaks it into **small units**. That lets React:
  1. **Pause** rendering,
  2. **Prioritise** important updates,
  3. **Resume** rendering.
- **Priority:** Fiber renders according to how important the task is.
  - **High**: user input.
  - **Low**: background data fetch.
- **Concurrency (React 18+):** React can prepare **multiple versions of the UI at the same time**.
- Fiber is also where React keeps per-component data between renders. For example, the stored state value from [lazy initialization](../hooks/lazy-state-initialization.md) lives in a fiber.

## Example
```
Without incremental rendering (one big block):
[ render whole tree █████████████████ ]  ← typing feels laggy, input waits

With Fiber (small units + priority):
[unit][unit][⌨ user input][unit][unit][unit]
             ↑ high priority jumps the queue,
               background fetch result rendered later
```

## Pitfalls
- Fiber is React's internal engine. I don't call it directly; I get the benefits through normal rendering and the concurrent features.
- Concurrency is **React 18+** only.
- Pausing and resuming means a render can be interrupted, so render code should just describe the UI. Side effects belong in [useEffect](../hooks/use-effect.md).

## Related
- [Virtual DOM](virtual-dom.md)
- [Reconciliation and diffing](reconciliation-and-diffing.md)
- [Lazy state initialization](../hooks/lazy-state-initialization.md)
