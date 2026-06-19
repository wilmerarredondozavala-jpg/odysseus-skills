---
name: test-driven-development
description: "TDD: enforce RED-GREEN-REFACTOR, tests before code."
---

# Test-Driven Development (TDD)

## When to use
For new features, bug fixes, refactoring, or behavior changes. Always, except throwaway prototypes.

## How

### The Iron Law
**NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST**

### RED — Write Failing Test
```python
def test_retries_failed_operations_3_times():
    attempts = 0
    def operation():
        nonlocal attempts
        attempts += 1
        if attempts < 3:
            raise Exception('fail')
        return 'success'
    result = retry_operation(operation)
    assert result == 'success'
    assert attempts == 3
```
- One behavior per test
- Clear descriptive name
- Real code, not mocks (unless unavoidable)

### Verify RED — Watch It Fail
```bash
pytest tests/test_feature.py::test_name -v
```
Confirm: test fails, failure message is expected, fails because feature is missing.

### GREEN — Minimal Code
Write the simplest code to pass. Nothing more.
```python
def add(a, b):
    return a + b  # Nothing extra
```
Cheating OK: hardcode return values, copy-paste, duplicate code. Fix in REFACTOR.

### Verify GREEN — Watch It Pass
```bash
pytest tests/test_feature.py::test_name -v
pytest tests/ -q  # No regressions
```

### REFACTOR — Clean Up
- Remove duplication, improve names, extract helpers
- Keep tests green throughout
- Don't add behavior

### Repeat
Next failing test for next behavior. One cycle at a time.

### Verification Checklist
- [ ] Every new function/method has a test
- [ ] Watched each test fail before implementing
- [ ] Each test failed for expected reason
- [ ] Wrote minimal code to pass
- [ ] All tests pass
- [ ] Edge cases and errors covered
