# Testing Prompts

This section provides prompts for generating, improving, and understanding tests using GitHub Copilot.

## Unit Test Generation

### Python Function Unit Test

**Use Case:** Generating unit tests for a Python function using pytest.

**The Prompt:**
```python
# Write pytest unit tests for the following function:
def add(a, b):
    return a + b
```

**Example Output:**
```python
import pytest

def add(a, b):
    return a + b

def test_add_positive_numbers():
    assert add(2, 3) == 5

def test_add_negative_numbers():
    assert add(-2, -3) == -5

def test_add_zero():
    assert add(0, 0) == 0
    assert add(0, 5) == 5
    assert add(5, 0) == 5
```

**Explanation:** This prompt is effective because it provides a simple function and asks Copilot to generate comprehensive tests, including edge cases. The use of pytest is specified, guiding Copilot to use the correct testing framework and conventions.

## Test Coverage

### JavaScript Test Coverage

**Use Case:** Ensuring all code paths are tested in a JavaScript function.

**The Prompt:**
```javascript
// Write Jest tests to achieve 100% coverage for this function:
function isLeapYear(year) {
  if (year % 4 !== 0) return false;
  if (year % 100 !== 0) return true;
  return year % 400 === 0;
}
```

**Example Output:**
```javascript
describe('isLeapYear', () => {
  it('returns true for typical leap years', () => {
    expect(isLeapYear(2020)).toBe(true);
    expect(isLeapYear(2004)).toBe(true);
  });

  it('returns false for typical non-leap years', () => {
    expect(isLeapYear(2019)).toBe(false);
    expect(isLeapYear(2018)).toBe(false);
  });

  it('returns false for years divisible by 100 but not 400', () => {
    expect(isLeapYear(1900)).toBe(false);
    expect(isLeapYear(2100)).toBe(false);
  });

  it('returns true for years divisible by 400', () => {
    expect(isLeapYear(2000)).toBe(true);
    expect(isLeapYear(1600)).toBe(true);
  });
});
```

**Explanation:** This prompt asks Copilot to generate tests that cover all logical branches, ensuring robust test coverage. By specifying the use of Jest and the goal of 100% coverage, Copilot is guided to create thorough tests.

## Property-Based Testing

### Property-Based Test Example

**Use Case:** Writing property-based tests for a function using Hypothesis in Python.

**The Prompt:**
```python
# Write property-based tests for this function using Hypothesis:
def reverse_string(s):
    return s[::-1]
```

**Example Output:**
```python
from hypothesis import given, strategies as st

def reverse_string(s):
    return s[::-1]

@given(st.text())
def test_reverse_string_involution(s):
    assert reverse_string(reverse_string(s)) == s

@given(st.text())
def test_reverse_string_length(s):
    assert len(reverse_string(s)) == len(s)
```

**Explanation:** This prompt is effective because it asks Copilot to use property-based testing, which checks general properties of the function rather than specific cases. The use of Hypothesis is specified, guiding Copilot to use the correct library and approach.
