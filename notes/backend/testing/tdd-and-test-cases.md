# TDD and what to test

> TDD is the red → green → refactor loop: write a failing test, make it pass with minimal code, then clean up while it stays green. Whatever the method, cover the happy path, edge cases, error handling and business-critical paths.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 30–31)

## Key ideas
- **TDD (Test-Driven Development):**
  1. Write a **failing** test.
  2. Write the **minimal** code to make it pass.
  3. **Improve** the code while the tests keep passing.
- **Don't force TDD** where it doesn't fit.
- **What to test:**
  - **Happy path:** the main way users interact with the feature.
  - **Edge cases:** empty inputs, maximum values, special characters.
  - **Error handling:** what happens when things go wrong.
  - **Business-critical features:** where bugs would cost the most.

## Example
TDD for `apply_discount(price, pct)`:
```python
# 1. RED: test first, function doesn't exist yet → fails
def test_ten_percent_off():
    assert apply_discount(200, 10) == 180

# 2. GREEN: minimal code to pass
def apply_discount(price, pct):
    return price - price * pct / 100

# 3. REFACTOR while green, and add the other case types:
def test_zero_percent():          # edge case
    assert apply_discount(200, 0) == 200

def test_negative_pct_rejected(): # error handling
    with pytest.raises(ValueError):
        apply_discount(200, -5)
```
The last test fails until a `ValueError` guard is added, which kicks off the next red → green loop.

## Pitfalls
- Writing more code than the test needs in the green step. Minimal really means minimal.
- Skipping refactor, so the tests pass but the code rots.
- Only testing the happy path. Bugs live at the edges and in the error branches.
- Applying TDD dogmatically to exploratory or throwaway code.

## Related
- [Testing pyramid](testing-pyramid.md)
- [CI/CD](../devops/ci-cd.md)
