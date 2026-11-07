# API authentication and token-based auth

> Authentication verifies who the client is so only authorized callers reach a resource. Token-based auth does that once, then hands back a token so the user doesn't re-enter credentials on every request.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 13, 15–16)

## Key ideas
- **API authentication** verifies a client's identity so that only authorized clients can access resources.
- **Why it matters:**
  - it protects data
  - it prevents unauthorized access
  - it enables tracking of who did what
- HTTP is stateless, so *something* has to prove identity on each request: a session ID, a token or encoded credentials.
- **Token-based authentication:**
  1. The server verifies the user's identity once.
  2. It issues a unique **access token**.
  3. Until the token expires, the user doesn't have to re-enter username/password.
- **Examples of token-style schemes:** JWT auth, session auth, OAuth, SAML.
- The schemes differ in **where the state lives**:
  - session: on the server
  - JWT: inside the token itself
  - OAuth: tokens issued by a separate authorization server

## Example
```
1. POST /login  {user, pass}        → server verifies
2.            ← 200 + token
3. GET /orders
   Authorization: Bearer <token>     → server checks token, no password
4. ...repeat until token expires → log in again
```

| Scheme | State lives… | Revoke |
|---|---|---|
| Session | server (store / Redis) | easy: delete session |
| JWT | in the signed token | hard: wait for expiry |
| Basic | nowhere: creds every time | change password |
| OAuth | auth server issues tokens | via auth server |

## Pitfalls
- Authentication (who are you) isn't authorization (what may you do). These notes cover the first.
- Tokens are bearer credentials: whoever holds one is treated as the user. Only send them over TLS.

## Related
- [Session authentication](session-authentication.md)
- [JWT authentication](jwt-authentication.md)
- [Basic authentication](basic-authentication.md)
- [OAuth and SSO](oauth-and-sso.md)
