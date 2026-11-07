# HTTP status codes

> A status code's first digit says who is responsible: 1xx info, 2xx success, 3xx redirect, 4xx client's fault, 5xx server's fault.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 2–3)

## Key ideas
- **1xx Informational:** the request was received and is still being processed.
- **2xx Success:** the request was received and accepted.
- **3xx Redirect:** the client must take further action to complete the request.
- **4xx Client error:** the request is missing something it needs, for example bad syntax, no auth or a wrong path.
- **5xx Server error:** the request was fine but the server failed.
- Read the class first, then the exact code.

## Example
Common codes to know cold:

| Code | Meaning | Typical case |
|---|---|---|
| 200 | OK | successful GET |
| 201 | Created | successful POST that made a resource |
| 301 | Moved permanently | resource lives at a new URL |
| 304 | Not modified | use your cached version |
| 400 | Bad request | malformed body or params |
| 401 | Unauthorized | missing or invalid credentials |
| 404 | Not found | no resource at that path |
| 500 | Internal server error | unhandled crash on the server |

```
POST /orders      → 201 Created
GET  /orders/999  → 404 Not Found
GET  /orders/1    (no token)  → 401 Unauthorized
GET  /logo.png    (cached, unchanged) → 304 Not Modified
```

## Pitfalls
- Don't return 200 with an error message in the body. Clients and caches trust the code.
- 4xx vs 5xx: if retrying the exact same request can never succeed, it's a 4xx.
- 304 has no body. The client is expected to already hold the cached copy.

## Related
- [HTTP basics](http-basics.md)
- [Caching basics](../caching/caching-basics.md)
- [API authentication](../auth/api-authentication.md)
