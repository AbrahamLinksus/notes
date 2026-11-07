# Testing pyramid

> Have many fast, cheap unit tests at the base, fewer integration tests in the middle, and a few slow, expensive end-to-end tests on top. Not testing costs more than testing.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 29–30)

## Key ideas
- The cost of **not** testing software is generally higher than the cost of testing it.
- **Unit tests** (base: fast, cheap, many):
  - test a single unit of code, like a function, method or class
  - run in **isolation**
  - cover different inputs
  - **precise**: a failure points at exactly one unit
- **Integration tests** (middle: medium speed, some):
  - verify that different components work together correctly
  - higher level than unit tests
- **E2E tests** (top: slow, expensive, few):
  - interact with the app through the **same interface as a user**: click buttons, fill forms
  - use a library like **Playwright**
- **Other test types:**
  - **smoke**: quick check that basic functionality works
  - **regression**: previously working features haven't broken
  - **performance**: how fast the app responds under load
  - **security**: vulnerabilities like SQL injection or XSS
  - **accessibility**: works for users with disabilities

## Example
Signup feature, tested at each level:
```
unit:         validate_email("a@x") → False        (one function, no DB)
integration:  POST /signup → row appears in users table   (API + DB together)
E2E:          Playwright opens /signup, types email, clicks "Create",
              sees "Welcome"                       (real browser, full stack)

        /\        E2E        – few
       /  \       Integration – some
      /____\      Unit        – many
```

## Pitfalls
- An inverted pyramid (mostly E2E) gives a slow, flaky, expensive suite.
- "Unit" tests that hit a real DB are really integration tests, and lose the precision.
- Only testing the levels you like: each level catches bugs the others miss.

## Related
- [TDD and what to test](tdd-and-test-cases.md)
- [CI/CD](../devops/ci-cd.md)
