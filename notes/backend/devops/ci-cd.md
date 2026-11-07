# CI/CD

> CI builds and tests every push automatically so breakage shows up immediately. CD takes a passing build and packages it for staging/production: delivery when a human releases it, deployment when it goes out automatically.

studied: 2026-11-07 · status: done · source: Backend.pdf (p. 28)

## Key ideas
- **CI/CD** stands for **Continuous Integration** and **Continuous Delivery/Deployment**, a DevOps practice.
- **CI:**
  - every push to the repo triggers an automated pipeline
  - the pipeline **builds** the code and runs the **test suite**
  - you find out instantly if new changes broke something that previously worked
- **CD:** if the pipeline passes, the same automation **packages the app** and pushes it to staging or production.
  - **Continuous delivery:** the package is ready to release.
  - **Continuous deployment:** it goes out automatically, with no manual step.
- CI is only as good as the tests it runs, so a weak test suite means a weak safety net.

## Example
```
git push
   │
   ▼
[CI] checkout → install deps → build → run tests
   │ fail → ✗ notify, stop (nothing ships)
   │ pass
   ▼
[CD] package (e.g. docker image) → staging
   │  delivery:   wait for manual "release" click → production
   │  deployment: automatically → production
```
```yaml
# minimal shape of a CI workflow
on: push
jobs:
  test:
    steps:
      - run: pip install -r requirements.txt
      - run: pytest
```

## Pitfalls
- Mixing up delivery and deployment. The difference is whether a human approves the release.
- Turning on continuous deployment without good tests ships bugs straight to production faster.
- Slow pipelines get skipped or ignored, so keep CI fast (that's why the unit-test base of the pyramid is large).

## Related
- [Git basics](git-basics.md)
- [Testing pyramid](../testing/testing-pyramid.md)
- [TDD and what to test](../testing/tdd-and-test-cases.md)
