# JWT authentication

> A JWT is a signed `header.payload.signature` token that carries the user's identity itself, so the server can verify requests without storing any session. In other words, it's stateless.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 14–15, 18)

## Key ideas
- **Flow:**
  1. The user logs in with credentials.
  2. The server verifies them and generates a JWT.
  3. The server **signs** the JWT with a secret key. This ensures integrity: any tampering breaks the signature.
  4. The server sends the JWT back to the client, for example in a cookie.
  5. Subsequent requests send the JWT in the **request headers**.
  6. The server verifies the user from the JWT alone.
- **JWT is stateless:** there's no server-side session lookup.
- **Structure:** three **base64URL** chunks joined by dots: `header.payload.signature`.
- **Signing algorithms:**
  - **HMAC** uses the *same* secret key to sign and verify. Fits a **monolith**, where one app holds the key.
  - **RSA, ECDSA** use asymmetric signing: a private key signs and a public key verifies. Fit **microservices**, where many services verify but only the auth service signs.

## Example
```
eyJhbGciOiJIUzI1NiJ9 . eyJ1c2VySWQiOjQyfQ . 4Xk…sig
└──── header ──────┘   └──── payload ───┘   └ signature ┘
 {"alg":"HS256"}        {"userId":42}       HMAC(header.payload, secret)

GET /profile
Authorization: Bearer eyJhbGci…
server: recompute signature → matches → trust userId 42
```

## Pitfalls
- Base64URL is encoding, not encryption. Anyone can read the payload, so never put secrets in it.
- Stateless cuts both ways: unlike sessions, a JWT can't be easily revoked before it expires.
- With HMAC in microservices, every verifying service would need the signing secret. That's why asymmetric keys are used there.

## Related
- [API authentication](api-authentication.md)
- [Session authentication](session-authentication.md)
- [OAuth and SSO](oauth-and-sso.md)
- [Monolith vs microservices](../architecture/monolith-vs-microservices.md)
