# Monolith vs microservices

> A monolith ships as one unit on one shared DB, so ACID transactions are easy but scaling is all-or-nothing. Microservices split by business capability with private data and independent deploys, and need patterns like SAGA for consistency.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 31–33)

## Key ideas
- **Monolithic architecture:**
  - The whole app is **one deployable unit**, or N identical copies of that process behind a load balancer.
  - **One shared DB** means **ACID transactions** can be enforced across the whole domain.
  - **Uniform scaling:** the whole app has to scale up, because there are no separate units to scale.
  - A **modular monolith** enforces internal boundaries (no cross-module table access) while still deploying as one unit.
- **Microservices:**
  - The system is split into **independently deployable services**, each owning a **business capability** (inventory, notification…).
  - They communicate over the network via HTTP or gRPC, or **async via a message broker**.
  - **Independently deployable** means, for example, Payments can ship without touching Orders. If they can't, you've built a **distributed monolith**, the worst of both.
  - **Private data:** each service owns its own data store.
  - **Decentralized governance:** each service picks its own language, data store and release cycle.
- **SAGA pattern:** handles **distributed transactions**, keeping data consistent across services when one ACID transaction can't span them.

## Example
"Place order" in each style:
```
Monolith:   BEGIN; insert order; decrement stock; charge payment; COMMIT;
            (one DB, all-or-nothing)

Microservices:
  Orders svc ──event──► Inventory svc ──event──► Payments svc
  each has its own DB → no single transaction
  SAGA: if payment fails → Inventory re-adds stock, Orders cancels
```

## Pitfalls
- Shared tables between "microservices" turn them into a distributed monolith.
- Splitting too early: you lose easy ACID and gain network failures and latency.
- Forgetting that network calls can be retried, so services need idempotency.

## Related
- [Idempotency](idempotency.md)
- [gRPC](../apis/grpc.md)
- [JWT authentication](../auth/jwt-authentication.md)
- [Indexing and sharding](../databases/indexing-and-sharding.md)
