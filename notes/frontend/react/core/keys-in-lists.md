# Keys in lists

> Keys give each list item a stable identity, so React can tell which items changed instead of matching them by position.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 3, 10)

## Key ideas
- By default React matches old and new children **by index** during [reconciliation](reconciliation-and-diffing.md).
- Index matching breaks when items are **reordered, changed or deleted**, so a **stable key** is needed.
- Keys **must be unique**.
- They help React **identify which items changed**.
- They help **prevent unnecessary re-renders**: an unchanged item keeps its key, so React leaves it alone.

## Example
A stable ID from the data as the key (from the `useMemo` product list):

```jsx
<ul>
  {filteredProducts.map(p => <li key={p.id}>{p.name}</li>)}
</ul>
```

What goes wrong with index keys when an item is removed from the front:

```
before:  key 0 → "apple"   key 1 → "mango"   key 2 → "orange"
delete "apple"
after:   key 0 → "mango"   key 1 → "orange"
→ React thinks item 0 changed apple→mango, item 1 changed mango→orange,
  and item 2 was deleted. Every row is touched.

with key={p.id}: "apple" is removed; mango and orange are untouched
```

## Pitfalls
- `key={idx}` (array index, as in the `<select>` options example) brings index matching straight back. It's only safe when the list never reorders, inserts or deletes.
- Duplicate keys break identification, so keys must be unique among the siblings.
- The key goes on the element returned from `map`, not on something inside it.

## Related
- [Reconciliation and diffing](reconciliation-and-diffing.md)
- [Form inputs](../forms/form-inputs.md)
- [useMemo and useCallback](../hooks/use-memo-and-use-callback.md)
