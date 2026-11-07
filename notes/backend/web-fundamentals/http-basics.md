# HTTP basics

> HTTP is the stateless request/response protocol web clients and servers talk over. HTTPS is the same thing with everything encrypted by SSL/TLS.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 1–2)

## Key ideas
- **HTTP (HyperText Transfer Protocol)** is how web servers and clients communicate: the client sends a request and the server sends back a response.
- **Stateless:** every request is independent, and the server doesn't remember earlier requests. Anything like "who is logged in" has to travel with each request (see the auth notes).
- **HTTPS** is HTTP made secure: all data in transit is encrypted by SSL or TLS.
- Core **methods**:
  1. `GET`: retrieve data
  2. `POST`: send new data
  3. `PUT`: update existing data
  4. `DELETE`: delete data
- A response has two parts:
  - **headers**: attributes about the message, grouped as request, response or general headers
  - **body**: the actual content

## Example
```
GET /users/42 HTTP/1.1          ← method + path
Host: api.example.com           ← request header
Accept: application/json

HTTP/1.1 200 OK                 ← status line
Content-Type: application/json  ← response header

{ "id": 42, "name": "Jake" }    ← body
```
The four methods applied to one resource:
```
GET    /users/42   → read user 42
POST   /users      → create a new user
PUT    /users/42   → update user 42
DELETE /users/42   → remove user 42
```

## Pitfalls
- Stateless doesn't mean an app can't have sessions. It means the session has to be carried by each request, for example as a cookie or token.
- Plain HTTP sends everything readable on the wire. Credentials only belong on HTTPS.
- Data that already exists is updated with `PUT`, not `POST`.

## Related
- [HTTP status codes](http-status-codes.md)
- [DNS resolution](dns-resolution.md)
- [REST API](../apis/rest-api.md)
- [Web servers](web-servers.md)
