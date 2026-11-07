# Web servers (Apache vs NGINX)

> A web server listens on a port and answers requests with the resource asked for. Apache uses a thread per connection, while NGINX is event-driven and async, which is why it copes better with high traffic.

studied: 2026-11-07 · status: done · source: Backend.pdf (p. 27)

## Key ideas
- **Web server:** software that serves web content.
- **What it does:** it listens on a port for requests sent over a transport protocol and returns a response with the requested resource.
- **Default ports:** HTTP goes to port **80** automatically, HTTPS to **443**.
- **Apache HTTP Server** is process-driven: each connection gets a dedicated thread.
- **NGINX** is event-driven and async, built to handle high traffic efficiently.

## Example
```
Apache (thread per connection)
  conn 1 ── thread 1  (blocked waiting on I/O)
  conn 2 ── thread 2
  conn 3 ── thread 3      → 10k connections ≈ 10k threads

NGINX (event loop)
  conn 1 ┐
  conn 2 ├── event loop: handles whichever connection is ready
  conn 3 ┘                → few workers, many connections
```
`http://site.com` is really `http://site.com:80`, and `https://site.com` is `:443`.

## Pitfalls
- The thread-per-connection model wastes memory on idle or slow clients, and that's exactly what hurts under heavy load.
- Event-driven servers suffer if one handler does blocking work, because it stalls everything sharing the loop.
- Running on a non-default port means the client has to name the port explicitly.

## Related
- [HTTP basics](http-basics.md)
- [Monolith vs microservices](../architecture/monolith-vs-microservices.md)
