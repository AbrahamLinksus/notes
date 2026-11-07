# REST API

> REST is a client-server, stateless style for resource-based APIs, defined by five constraints: client-server, stateless, cacheable, layered and uniform interface.

studied: 2026-11-07 · status: done · source: Backend.pdf (p. 10)

## Key ideas
- **REST (Representational State Transfer)** uses a client-server architecture.
- **Stateless:** the server doesn't store client context or session data between requests. Each request carries everything needed.
- **The five constraints:**
  1. **Client-server:** UI and data storage are separated.
  2. **Stateless:** no session kept on the server between calls.
  3. **Cacheability:** a response should say whether it's cacheable.
  4. **Layered system:** intermediate servers can be used without the client knowing.
  5. **Uniform interface:** resources are accessed the same consistent way, through URLs plus HTTP methods.
- These constraints make REST easy to scale horizontally, because any server can handle any request.

## Example
```
GET    /books          → list books           (cacheable)
GET    /books/7        → one book             (cacheable)
POST   /books          → create a book   → 201
PUT    /books/7        → update book 7
DELETE /books/7        → delete book 7

Stateless: each call carries its own auth
GET /books/7
Authorization: Bearer <token>
```
Layered: client → CDN / load balancer → API server. The client only ever sees one URL.

## Pitfalls
- Storing per-user session state in server memory breaks statelessness. Requests then only work on the one server that holds it.
- Verbs in URLs (`/getBook?id=7`) go against the uniform interface. The HTTP method should carry the action.
- Missing cache headers waste the cacheability constraint.

## Related
- [API styles overview](api-styles-overview.md)
- [HTTP basics](../web-fundamentals/http-basics.md)
- [SOAP](soap.md)
- [JWT authentication](../auth/jwt-authentication.md)
