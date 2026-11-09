# Next.js rendering strategies (CSR, SSR, static, dynamic)

> CSR renders in the browser and is invisible to search bots. SSR renders on the server for SEO and smaller bundles, either at build time (static) or at request time (dynamic).

studied: 2026-11-09 · status: done · source: React.pdf (pp. 30–32)

## Key ideas
- **Client-side rendering (CSR):**
  - bundles the code and sends it to the browser, which does the rendering
  - **search engine bots cannot index** the content well, which is plain React's SEO problem
- **Server-side rendering (SSR):**
  - renders the webpage **on the server** and sends the result to the browser
  - **allows for SEO**
  - **smaller bundle** sent to the client
  - **cannot access browser events or state**
- **Static rendering:** rendering at **build time**.
- **Dynamic rendering:** rendering at **request time**.
- **Static and dynamic rendering both come under server-side rendering.**
- SSG (static site generation) is the static flavour, and it's one of the things plain React lacks.

## Example
```
CSR:      browser ← JS bundle → browser runs JS → HTML appears   (bots see little)

SSR ─┬─ Static:   build ──► HTML generated once ──► served to every request
     └─ Dynamic:  request ──► server renders HTML now ──► sent to that user
```

| | CSR | SSR (static) | SSR (dynamic) |
|---|---|---|---|
| Where | browser | server | server |
| When | on load in browser | build time | request time |
| SEO | poor | good | good |
| Browser events/state | yes | no | no |

## Pitfalls
- SSR components can't use browser events or state. Interactive parts need `'use client'`. See [server and client components](server-and-client-components.md).
- "Static" doesn't mean "not server-side". It's server rendering done ahead of time at build.

## Related
- [Server and client components](server-and-client-components.md)
- [Data fetching and caching](data-fetching-and-caching.md)
- [Client vs server routing](../react/routing/client-vs-server-routing.md)
