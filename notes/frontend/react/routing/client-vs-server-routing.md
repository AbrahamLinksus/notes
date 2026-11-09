# Client-side vs server-side routing

> Server-side routing fetches a fresh HTML page for every URL. Client-side routing (React Router) loads JS once, then swaps components in the browser with no reload.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 23–24)

## Key ideas
- **Who decides what to render:**
  - server-side: the **server**, based on the requested URL
  - client-side: the **browser/JS**, matching the current URL against `<Routes>`
- **On navigation:**
  - server-side: a new HTTP request, a full page reload and fresh HTML
  - client-side: JS intercepts, updates the URL and re-renders components, with **no reload**
- **Initial load:**
  - server-side: **fast**, because the server sends ready-to-display HTML immediately
  - client-side: **slower**, because the browser must download and run the whole JS bundle before anything meaningful renders
- **Later navigation:** server-side is slow (a full round-trip every time), while client-side is fast (no network round-trip).
- **State across "pages":** server-side has none, since every load starts fresh. Client-side preserves it, because the app stays alive.

## Example
| | Server-side | Client-side (React Router) |
|---|---|---|
| Who decides | server | browser / JS |
| On navigation | request + full reload | URL update + re-render |
| Initial load | fast | slower (JS bundle) |
| Later navigation | slow | fast |
| State across pages | lost | kept |

```
Server:  click → GET /about → new HTML → page reload → state gone
Client:  click → pushState("/about") → <Routes> match → swap component → state kept
```

## Pitfalls
- Client-side routing's slow first load and JS-only rendering are why Next.js adds server rendering. See [rendering strategies](../../nextjs/rendering-strategies.md).
- An internal `<a href>` in a React app quietly switches you back to server-style full reloads.

## Related
- [React Router basics](react-router-basics.md)
- [Next.js rendering strategies](../../nextjs/rendering-strategies.md)
- [Browser rendering](../../../backend/web-fundamentals/browser-rendering.md)
