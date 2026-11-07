# Basic authentication

> Basic auth sends `username:password`, Base64-encoded, in a request header on every request. Base64 is just encoding, so it's only safe over TLS.

studied: 2026-11-07 · status: done · source: Backend.pdf (p. 15)

## Key ideas
- The client authenticates itself with a **username and password** on each request.
- The credentials are joined as `username:password` and **Base64-encoded**.
- The encoded string travels in the **request header**.
- The server **decodes** it to get the username and password back, then checks them.
- It **must be done over TLS**. Base64 is encoding, not encryption, so anyone who can see the traffic can decode it.
- There's no session or token: the raw credentials go out every time.

## Example
```
username = jake, password = s3cret
"jake:s3cret"  --base64-->  amFrZTpzM2NyZXQ=

GET /reports HTTP/1.1
Authorization: Basic amFrZTpzM2NyZXQ=

server: base64-decode → "jake:s3cret" → split on ":" → verify
```
```python
import base64
base64.b64decode("amFrZTpzM2NyZXQ=").decode()   # 'jake:s3cret' (trivially reversible)
```

## Pitfalls
- Treating Base64 as security is the classic mistake. Without HTTPS the password is effectively plain text.
- The credentials go out on *every* request, so there are more chances to leak them than with a short-lived token.
- There's no built-in logout or expiry: revoking means changing the password.

## Related
- [API authentication](api-authentication.md)
- [JWT authentication](jwt-authentication.md)
- [HTTP basics](../web-fundamentals/http-basics.md)
