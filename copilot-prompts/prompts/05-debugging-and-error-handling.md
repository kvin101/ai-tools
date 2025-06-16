# Debugging and Error Handling Prompts

This section provides prompts for generating code that helps with debugging and robust error handling using GitHub Copilot.

## Debugging Code

### Add Debug Logging

**Use Case:** Adding debug logging to trace the execution of a function.

**The Prompt:**
```python
# Add debug logging to this function to trace its execution:
def calculate_area(radius):
    return 3.14159 * radius * radius
```

**Example Output:**
```python
import logging

def calculate_area(radius):
    logging.debug(f"Calculating area for radius: {radius}")
    area = 3.14159 * radius * radius
    logging.debug(f"Calculated area: {area}")
    return area
```

**Explanation:** This prompt is effective because it asks Copilot to add logging statements, making it easier to trace the function's execution and debug issues.

## Error Handling

### Robust Error Handling in JavaScript

**Use Case:** Improving error handling in a JavaScript function.

**The Prompt:**
```javascript
// Add robust error handling to this function:
function fetchData(url) {
  const response = fetch(url);
  return response.json();
}
```

**Example Output:**
```javascript
async function fetchData(url) {
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    console.error('Fetch error:', error);
    return null;
  }
}
```

**Explanation:** This prompt is effective because it asks Copilot to add error handling and logging, making the function more robust and easier to debug.

## Exception Handling Patterns

### Custom Exception Classes in Java

**Use Case:** Creating custom exception classes for better error handling in Java.

**The Prompt:**
```java
// Create a custom exception class for invalid user input
// Use it in a function that parses user age from a string
```

**Example Output:**
```java
public class InvalidUserInputException extends Exception {
    public InvalidUserInputException(String message) {
        super(message);
    }
}

public int parseUserAge(String input) throws InvalidUserInputException {
    try {
        int age = Integer.parseInt(input);
        if (age < 0) {
            throw new InvalidUserInputException("Age cannot be negative");
        }
        return age;
    } catch (NumberFormatException e) {
        throw new InvalidUserInputException("Invalid age format");
    }
}
```

**Explanation:** This prompt is effective because it asks Copilot to create a custom exception and use it in a practical scenario, improving error handling and code clarity.
