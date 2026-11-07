# Session authentication

> In session auth the server stores the login state and hands the client only a random session ID in a cookie. That makes revoking easy, but every server needs access to the session store.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 13–14)

## Key ideas
- **Flow:**
  1. The user sends login credentials.
  2. The server authenticates them.
  3. The server creates a session and stores its data in a session store or an in-memory DB like **Redis**.
  4. The server sends back the **session ID** as a **cookie**.
  5. The client sends that session ID with every subsequent request.
  6. The server uses the ID to authenticate the user until the session expires.
- The **session ID has nothing to do with the email/password**. It's usually a random hashed string.
- The **server is responsible for session management**: it's a stateful scheme.
- **Pro:** revoking a session is easy. Delete it from the store and the user is logged out.
- **Distributed systems:** all servers have to read a **centralized session store** (Redis or a central SQL store), which **adds latency** to every request.

## Example
```
POST /login {email, pass}
  server: verify → sessions["a9f3…"] = {userId: 42, exp: …}
  ← Set-Cookie: sid=a9f3…

GET /cart   Cookie: sid=a9f3…
  server: sessions["a9f3…"] → userId 42 ✔

Logout / ban:  delete sessions["a9f3…"]  → next request fails
```
```
app server 1 ┐
app server 2 ├──► Redis (shared session store)   ← extra network hop per request
app server 3 ┘
```

## Pitfalls
- Keeping sessions in one server's local memory breaks as soon as there's a second server behind a load balancer.
- The central session store becomes a latency cost and a dependency for every request.
- The session ID should never be derived from user credentials.

## Related
- [API authentication](api-authentication.md)
- [JWT authentication](jwt-authentication.md)
- [Cache types](../caching/cache-types.md)
