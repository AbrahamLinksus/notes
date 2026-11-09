# Why Next.js

> Next.js is a React framework that adds what React alone lacks: routing, server-side rendering, static generation and better SEO.

studied: 2026-11-09 · status: done · source: React.pdf (pp. 29–30)

## Key ideas
- **Next.js is a dynamic React framework.** React itself is more of an open-source library of tools.
- **The essentials of a web app**, which a framework has to cover:
  1. **User interface**: how users engage with the app
  2. **Routing**: navigation
  3. **Data fetching**: retrieving information
  4. **Rendering**: presenting static or dynamic content
  5. **Integrations**: connecting to other services
  6. **Infrastructure**: the environment where app code is deployed
  7. **Performance**: improving user experience
  8. **Scalability**: the app keeps working as data and traffic grow
  9. **Developer experience**: how easily the team can develop
- **What plain React lacks:**
  1. no built-in routing system
  2. no compiler (solved from React 19 onward)
  3. weak **SEO**, because rendering happens client-side
  4. no **SSR** (server-side rendering)
  5. no **SSG** (static site generation)
- Next.js splits work between a **client** (browser/frontend) and a **server** (backend).

## Example
```
┌──────────────────┐        ┌──────────────────────────┐
│  Next.js client  │ ◄────► │  Next.js server          │
│  components      │        │  components, actions,    │
│  (browser /      │        │  route handlers          │
│   frontend)      │        │  (backend)               │
└──────────────────┘        └──────────────────────────┘
```

## Pitfalls
- "No compiler" is no longer true from React 19. Don't use it as a reason in interviews without that caveat.
- Next.js doesn't replace React. Components, hooks and JSX all still apply. It adds routing, rendering modes and a server.

## Related
- [File-based routing](file-based-routing.md)
- [Rendering strategies](rendering-strategies.md)
- [Server and client components](server-and-client-components.md)
- [What is React](../react/core/react-overview.md)
