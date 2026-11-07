# Cache eviction policies

> When the cache is full, the eviction policy decides who leaves. Match it to the access pattern: LRU for "recent is likely again", MRU when you never want the same item twice, LFU when popularity matters.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 20–21)

## Key ideas
- Eviction exists because the cache is small: a new entry needs space.
- **Policies:**
  1. **LRU (Least Recently Used):** evict the entry that was used least recently.
  2. **MRU (Most Recently Used):** evict the *freshest* entry. Example: a Tinder profile roll, where you shouldn't see the same person again.
  3. **LFU (Least Frequently Used):** evict the entry used the fewest times. Example: emoji suggestions, where frequently used emojis stay.
  4. **RR (Random Replacement):** evict a random entry.
  5. **FIFO (First In, First Out):** evict the oldest inserted entry.
  6. **LIFO (Last In, First Out):** evict the newest inserted entry.
- LRU/MRU care about **when** an entry was last used, LFU about **how often**, and FIFO/LIFO about **insertion order**.

## Example
Cache size 3, access sequence `A B C A D`:
```
after A B C:  [A, B, C]           (A oldest use)
access A:     [B, C, A]           (A now most recent)
insert D, cache full:
  LRU  → evict B  → [C, A, D]
  MRU  → evict A  → [B, C, D]
  FIFO → evict A  → [B, C, D]   (A was inserted first)
  LFU  → A used 2×, B/C 1× → evict B or C
```
```python
from functools import lru_cache
@lru_cache(maxsize=128)       # LRU out of the box
def get_user(uid): ...
```

## Pitfalls
- FIFO ≠ LRU. FIFO ignores that an old entry is still being used heavily.
- LFU can keep once-popular entries forever if their counts never decay.
- MRU looks odd, but it's right for "don't repeat what was just seen" workloads.

## Related
- [Caching basics](caching-basics.md)
- [Write strategies](write-strategies.md)
- [Read strategies](read-strategies.md)
