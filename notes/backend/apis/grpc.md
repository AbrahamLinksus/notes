# gRPC

> gRPC is a remote-procedure-call framework for server-to-server traffic. It's fast because Protocol Buffers send compact binary instead of bloated JSON, and HTTP/2 multiplexes many calls over one TCP connection.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 11–12)

## Key ideas
- **gRPC (Remote Procedure Calls)** is mostly used for communication **between servers**, for example between microservices. It's highly scalable.
- **Protocol Buffers** act as the **interface definition language**: they define the service and messages and serialize structured data into compact binary.
- **Why it beats JSON on performance:**
  - JSON data is rarely flat. Nested objects and repeated key names bloat the payload.
  - gRPC sends binary, so the same data takes much less space.
- It supports **full bi-directional streaming**.
- It's built on **HTTP/2**, which supports **multiplexing** many requests over a single TCP connection.

## Example
```proto
// user.proto: the contract both services compile against
service UserService {
  rpc GetUser (GetUserRequest) returns (User);
}
message GetUserRequest { int32 id = 1; }
message User { int32 id = 1; string name = 2; }
```
```
JSON on the wire:   {"id":42,"name":"Jake"}   ← key names sent every time
protobuf on wire:   field 1 = 42, field 2 = "Jake"  ← numbered fields, binary
```
HTTP/2 multiplexing: calls A, B and C are interleaved on one TCP connection, instead of opening three connections or waiting in line.

## Pitfalls
- Binary payloads aren't human-readable, so debugging needs tooling rather than just reading the response.
- Both sides have to share the `.proto` contract. Changing field numbers breaks clients.
- It's a poor fit for browser-facing public APIs, which is why it's described as server-to-server.

## Related
- [API styles overview](api-styles-overview.md)
- [SOAP](soap.md)
- [Monolith vs microservices](../architecture/monolith-vs-microservices.md)
