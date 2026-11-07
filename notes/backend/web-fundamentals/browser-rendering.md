# Browser rendering

> The browser turns raw bytes into a DOM and a CSSOM, merges them into a render tree, computes layout, then paints. Scripts and CSS can block that pipeline.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 5–7)

## Key ideas
- **Browser goals:** display content and let you interact with it.
- **Components:**
  - UI
  - **browser engine**, responsible for HTML/CSS
  - rendering engine
  - **JS engine**
  - network
  - **timers**: `setTimeout`/`setInterval` live in the browser, and JS borrows them from there. Node implements its own version.
  - data storage
- **HTML → DOM:**
  1. Load the file as raw bytes.
  2. Convert the bytes to characters using the `charset`.
  3. Turn the characters into tokens (`<h1>`, `<p>`, …).
  4. Turn the tokens into objects.
  5. Link the objects into a model, the **DOM tree** (a node list).
- **CSS → CSSOM:** the same chain, raw → char → token → object → relation, produces the CSS object model.
- **Render tree:** the engine combines DOM and CSSOM, does the layout maths (size, margin, etc.), then displays the content.
- **Blocking:**
  - When a `<script>` tag comes into view, rendering halts and JS gets priority.
  - If the CSSOM isn't ready yet, scripts halt too.
  - The fix is to defer scripts or load them async.

## Example
```
bytes → chars → tokens → objects → DOM ─┐
                                        ├→ render tree → layout → paint
bytes → chars → tokens → objects → CSSOM┘

token → object:
<h1 title="eg">Hi</h1>  →  { tag: "h1", title: "eg", data: "Hi" }
```

## Pitfalls
- React-style apps are JS-driven, so all the JS must reach the browser before the page is visible. Big bundles mean a slow first paint.
- A `<script>` in `<head>` without `defer`/`async` blocks the whole page.
- Slow CSS delays JS as well, because scripts wait on the CSSOM.

## Related
- [DNS resolution](dns-resolution.md)
- [HTTP basics](http-basics.md)
- [Cache types](../caching/cache-types.md)
