# SOAP

> SOAP is a strict, XML-only, W3C-standard protocol built around security and reliability. It exposes actions rather than resources and isn't tied to HTTP.

studied: 2026-11-07 · status: done · source: Backend.pdf (p. 11)

## Key ideas
- **SOAP (Simple Object Access Protocol)** focuses on **security and reliability**, which makes it common in enterprise systems.
- It's a **strict protocol** defined by W3C standards, with SSL support and ACID compliance.
- It relies entirely on **XML**.
- It's **stateless by default**, but can be made stateful.
- It's **function-driven**: it exposes actions like `GetUser` or `GetAccount`, not resources.
- It's **transport-agnostic**: it can run over HTTP, SMTP, UDP, etc.

## Example
REST vs SOAP for "get user 42":
```
REST:  GET /users/42

SOAP:  POST /UserService
       <soap:Envelope>
         <soap:Body>
           <GetUser>
             <UserId>42</UserId>
           </GetUser>
         </soap:Body>
       </soap:Envelope>
```
In SOAP the action name (`GetUser`) lives inside the XML body, while in REST the resource is in the URL and the action is the HTTP method.

| | REST | SOAP |
|---|---|---|
| Format | usually JSON | XML only |
| Style | resource-based | function/action-based |
| Transport | HTTP | HTTP, SMTP, UDP… |
| Strictness | style/guidelines | formal protocol |

## Pitfalls
- REST and SOAP aren't the same kind of thing: REST is an architectural style and SOAP is a protocol.
- XML envelopes are verbose, so SOAP is heavier on the wire than JSON.
- "Stateless by default" doesn't mean always stateless. A stateful SOAP service loses the easy-scaling benefit.

## Related
- [API styles overview](api-styles-overview.md)
- [REST API](rest-api.md)
- [gRPC](grpc.md)
