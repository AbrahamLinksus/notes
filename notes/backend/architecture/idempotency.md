# Idempotency

> An idempotent operation gives the same result whether it runs once or many times. It matters because retries happen, and a retried payment must not charge twice.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 35–36)

## Key ideas
- **Idempotency:** executing the same operation multiple times gives the same result as applying it once.
- **Where it matters:**
  - a payment not going through twice
  - not placing the same order twice
  - not sending the same message again
- **Cause:** usually **retries** after an API failure or timeout, when the first attempt may actually have succeeded.
- **Solutions:**
  1. **Don't auto-retry.** Without automatic retries you don't need idempotency: just throw an error and let the user retry explicitly.
  2. **Check and update:** before processing, check whether the first transaction was already processed.
- **Idempotent payment flow:**
  1. The payment service talks to the payment gateway and generates a **payment ID**. That ID is shared between the user, the payment service and the gateway.
  2. The service initiates the payment using that payment ID.
  3. On a **retry, the same payment ID** is reused, so the gateway recognises it as a repeat and doesn't charge again.

## Example
```
payment service                         payment gateway
  ── request ID ─────────────────────────►
  ◄──────────────────── payment ID P1122 ─
  ── pay(P1122) ─────────────────────────►  charged ✔
  ◄─────────────── response lost  ✗ ───────
  ── retry pay(P1122) ───────────────────►  "P1122 already done" → no 2nd charge
  ◄──────────────────────── success ✔ ────
```
```python
def pay(payment_id, amount):
    if store.exists(payment_id):        # check
        return store.get(payment_id)    # same result as first time
    result = gateway.charge(amount)
    store.set(payment_id, result)       # update
    return result
```

## Pitfalls
- Generating a **new** ID on each retry defeats the whole scheme.
- Doing check-then-update non-atomically lets two concurrent retries both pass the check.
- `GET`, `PUT` and `DELETE` are meant to be idempotent, but `POST` usually isn't, so that's where you need keys.

## Related
- [Monolith vs microservices](monolith-vs-microservices.md)
- [API styles overview](../apis/api-styles-overview.md)
- [HTTP basics](../web-fundamentals/http-basics.md)
