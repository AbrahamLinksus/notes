# Reconciliation and diffing

> On every change, React compares the new tree with the previous one and computes the minimal set of changes for the real DOM. Two heuristics make that O(n) instead of O(n³).

studied: 2026-11-09 · status: done · source: React.pdf (pp. 2–3)

## Key ideas
- **Reconciliation:** when changes are made, React compares the current DOM to the previous DOM and computes the **minimal set of changes** needed to update the real DOM. It's essentially comparing 2 versions.
- **Diffing heuristics:** a full tree diff is **O(n³)**. React gets it to **O(n)** with two rules:
  1. **Different element types produce different trees.** If a `<div>` becomes a `<span>`, React tears down the div and builds the span from scratch.
  2. **Elements of the same type are compared by their attributes/props**, and only what changed is updated.
- **Children are matched by index** by default. This breaks when items are reordered, changed or deleted, so a **stable key** is required. See [keys in lists](keys-in-lists.md).

## Example
```
Rule 1: type changed → rebuild subtree
old: <div  className="card"><Counter /></div>
new: <span className="card"><Counter /></span>
→ div and everything under it destroyed, span + new Counter built

Rule 2: same type → patch attributes
old: <div className="card" />
new: <div className="card active" />
→ same div kept, only className updated
```

## Pitfalls
- Swapping a wrapper element's type (div ↔ span, or one component ↔ another) throws away the whole subtree, including the children's state.
- Index-based matching for lists silently mixes up items on reorder or delete. Give each item a unique, stable key.
- O(n) is only possible because of these assumptions. React doesn't search for "moved" subtrees, and keys are its only hint.

## Related
- [Virtual DOM](virtual-dom.md)
- [Keys in lists](keys-in-lists.md)
- [React Fiber](react-fiber.md)
