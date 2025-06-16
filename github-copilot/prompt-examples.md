# GitHub Copilot Prompt Examples

This document provides example prompts for getting the most out of GitHub Copilot. Use these as templates or inspiration for your own coding tasks.

## Function Generation

**Prompt:**
```python
# Write a Python function to calculate the factorial of a number
```

**Prompt:**
```javascript
// Create a function that reverses a string
```

## Test Generation

**Prompt:**
```python
# Write pytest unit tests for the following function:
def add(a, b):
    return a + b
```

**Prompt:**
```javascript
// Write Jest tests for this function:
function isEven(n) {
  return n % 2 === 0;
}
```

## Code Explanation

**Prompt:**
```python
# Explain what this function does:
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)
```

## Refactoring

**Prompt:**
```javascript
// Refactor this code to use async/await instead of callbacks
```

## Code Review

**Prompt:**
```python
# Review this function for readability and suggest improvements:
def process(data):
    # ...
```

## Automation

**Prompt:**
```bash
# Write a Bash script to monitor a directory and print a message when a new file is added
```

## Creative Tasks

**Prompt:**
```javascript
// Suggest 5 creative ways to visualize time-series data in JavaScript
```
