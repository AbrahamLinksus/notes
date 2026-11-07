# API styles overview

> Pick the API style for the job: SOAP for strict enterprise contracts, REST for resource-based web APIs, GraphQL to stop over/underfetching, gRPC for fast server-to-server calls, WebSockets for live two-way data, and webhooks for events.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 10, 12)

## Key ideas
- **SOAP:** XML-based, used for enterprise applications, with security and reliability as the focus.
- **REST:** resource-based, for web servers. The default for most public APIs.
- **GraphQL:** a query language that reduces network load. It mainly solves **overfetching** (getting fields you don't need) and **underfetching** (needing several calls to get everything), usually through just **one HTTP endpoint**.
- **gRPC:** high performance, aimed at microservices and server-to-server traffic.
- **WebSocket:** bi-directional, low-latency data exchange. The server can push to the client.
- **Webhook:** asynchronous, for event-driven applications. The provider calls *your* URL when something happens.

## Example
Fetching a user's name plus their last 3 order totals:
```
REST     GET /users/42            → whole user object (overfetch)
         GET /users/42/orders     → all orders (overfetch + 2nd call = underfetch)

GraphQL  POST /graphql
         { user(id: 42) { name orders(last: 3) { total } } }
         → exactly those fields, one round trip
```
Event example: instead of polling `GET /payments/7` every 5 s, register a webhook and the payment provider POSTs to `/hooks/payment` when the status changes.

## Pitfalls
- GraphQL fixes fetching shape, not query cost. Nested resolvers can still trigger N+1 queries on the backend.
- WebSockets keep connections open, so they're overkill when the client only needs a response now and then.
- Webhooks are async calls into your system, so expect retries and handle them idempotently.

## Related
- [REST API](rest-api.md)
- [SOAP](soap.md)
- [gRPC](grpc.md)
- [N+1 problem](../databases/n-plus-one-problem.md)
- [Idempotency](../architecture/idempotency.md)
