# Code Refactoring Prompts

Effective prompts for improving code quality, performance, and maintainability.

## Code Simplification

### Simplify Complex Conditionals
```
[Additional Information]
- Code to refactor:
[paste code]
- Improvements needed:
  - Use early returns and guard clauses.
  - Eliminate deep nesting.
  - Extract complex conditions into meaningful variable names.
  - Consider using strategy/state patterns for complex logic.
- Constraints: Maintain the same functionality.

[Directive]
Refactor this complex conditional structure to be more readable and add clear comments explaining the new logic.
```

### Extract Functions/Methods
```
[Additional Information]
- Code to refactor:
[paste code]
- Guidelines:
  - Identify code blocks that can become separate functions.
  - Create meaningful function names that describe their purpose.
  - Reduce function length to under [X] lines.
  - Eliminate code duplication.
  - Maintain the single responsibility principle.
  - Add appropriate parameters and return values.

[Directive]
Refactor this code by extracting functions to improve its readability.
```

### Eliminate Code Duplication
```
[Additional Information]
- Code to refactor:
[paste code]
- Requirements:
  - Identify repeated code patterns.
  - Create reusable functions, methods, or classes.
  - Parameterize differences between duplicated code.
  - Ensure the abstraction is logical and not over-engineered.
- Constraints: Maintain existing functionality.

[Directive]
Remove code duplication from this codebase and update all call sites to use the new shared code.
```

## Performance Optimization

### Optimize Loops and Iterations
```
[Additional Information]
- Code to optimize:
[paste code]
- Focus areas:
  - Reduce time complexity.
  - Eliminate unnecessary iterations.
  - Use more efficient data structures.
  - Cache repeated calculations.
  - Consider early exit conditions.
  - Batch operations where applicable.
- Constraints: Maintain the correctness of the results.

[Directive]
Optimize the performance of this code.
```

### Database Query Optimization
```
[Additional Information]
- Code to optimize:
[paste code]
- Improvements needed:
  - Reduce the number of database calls.
  - Use appropriate indexes.
  - Implement batch operations.
  - Add connection pooling.
  - Use prepared statements.
  - Consider caching strategies.
- Constraints: Maintain data consistency.

[Directive]
Optimize these database operations for better performance.
```

### Memory Usage Optimization
```
[Additional Information]
- Code to optimize:
[paste code]
- Strategies:
  - Use generators/iterators instead of loading all data into memory.
  - Implement streaming for large datasets.
  - Remove unnecessary object retention.
  - Use memory-efficient data structures.
  - Consider lazy loading.
- Process: Profile memory usage before and after to verify the improvement.

[Directive]
Reduce the memory usage in this code.
```

## Architecture Improvements

### Apply Design Patterns
```
[Role]
You are a senior software architect.

[Additional Information]
- Code to refactor:
[paste code]
- Current issues: [describe problems with current design]
- Suggested patterns: [specify patterns to consider, e.g., Factory, Singleton, Observer]
- Requirements:
  - Improve separation of concerns.
  - Reduce coupling between components.
  - Increase code reusability.
  - Make the code more testable.
  - Follow SOLID principles.
  - Add clear interfaces/abstractions.

[Directive]
Refactor this code to use appropriate design patterns.
```

### Improve Error Handling
```
[Additional Information]
- Code to improve:
[paste code]
- Improvements needed:
  - Add comprehensive try-catch blocks.
  - Create custom exception classes where appropriate.
  - Implement proper error logging.
  - Provide meaningful error messages.
  - Handle different error scenarios appropriately.
  - Add input validation.
  - Implement graceful degradation.

[Directive]
Enhance the error handling in this code.
```

### Modernize Legacy Code
```
[Additional Information]
- Code to modernize:
[paste code]
- Context:
  - Language/Framework: From [specify current version] to [specify target version]
- Updates needed:
  - Use modern language features and syntax.
  - Replace deprecated methods/functions.
  - Improve type safety with type hints/annotations.
  - Use current best practices and conventions.
  - Update dependencies to current versions.
- Constraints: Maintain backward compatibility where needed.

[Directive]
Modernize this legacy code.
```

## Code Organization

### Restructure Classes
```
[Additional Information]
- Class to refactor:
[paste code]
- Issues to address:
  - Class has too many responsibilities (violates SRP).
  - Methods are too long or complex.
  - Poor encapsulation of data.
  - Unclear or inconsistent naming.
  - Missing or inadequate documentation.
- Principles to apply:
  - Single Responsibility Principle
  - Proper encapsulation
  - Clear method and property names
  - Appropriate visibility modifiers

[Directive]
Refactor this class to improve its design.
```

### Organize Module Structure
```
[Additional Information]
- Code to reorganize:
[paste code]
- Current issues: [describe current organization problems, e.g., circular dependencies, poor cohesion]
- Improvements needed:
  - Group related functionality together.
  - Create clear module boundaries.
  - Implement proper import/export structure.
  - Reduce circular dependencies.
  - Follow language-specific conventions.
  - Add module-level documentation.

[Directive]
Reorganize this code into a better module structure.
```

## Security Improvements

### Fix Security Vulnerabilities
```
[Role]
You are a cybersecurity expert.

[Additional Information]
- Code to review:
[paste code]
- Security concerns to address:
  - Input validation and sanitization
  - SQL injection prevention
  - Cross-site scripting (XSS) protection
  - Authentication and authorization flaws
  - Secure data handling
  - Improper error message disclosure
  - Use of secure coding practices

[Directive]
Review and fix the security issues in this code.
```

### Implement Safe Data Handling
```
[Role]
You are a security engineer.

[Additional Information]
- Code to refactor:
[paste code]
- Security improvements:
  - Validate all inputs.
  - Sanitize data before processing.
  - Use parameterized queries for database interactions.
  - Implement proper access controls.
  - Add audit logging for sensitive operations.
  - Handle sensitive data appropriately.
  - Use encryption where needed.

[Directive]
Refactor this data handling code for security.
```

## Testability Improvements

### Make Code More Testable
```
[Additional Information]
- Code to refactor:
[paste code]
- Changes needed:
  - Remove hard-coded dependencies.
  - Implement dependency injection.
  - Create mockable interfaces.
  - Reduce static method usage.
  - Separate business logic from infrastructure concerns.
  - Make functions pure where possible.
  - Add clear input/output contracts.

[Directive]
Refactor this code to improve its testability.
```

### Add Test-Friendly Abstractions
```
[Additional Information]
- Code to refactor:
[paste code]
- Requirements:
  - Extract external dependencies behind interfaces.
  - Create seams for test doubles (mocks, stubs).
  - Make time-dependent code testable (e.g., by injecting a clock).
  - Add configuration points for test scenarios.
  - Ensure deterministic behavior.
- Output: Provide test utilities and helpers.

[Directive]
Add abstractions to this code to make it easier to test.
```

## Language-Specific Refactoring

### Python Refactoring
```
[Role]
You are an expert Python developer.

[Additional Information]
- Code to refactor:
[paste code]
- "Pythonic" improvements:
  - Use list/dict comprehensions appropriately.
  - Implement proper exception handling.
  - Use context managers for resource handling (`with` statements).
  - Follow PEP 8 style guidelines.
  - Use type hints.
  - Leverage Python's built-in functions.
  - Use dataclasses or named tuples where appropriate.

[Directive]
Refactor this Python code to be more Pythonic.
```

### JavaScript/TypeScript Refactoring
```
[Role]
You are a senior frontend/backend JavaScript developer.

[Additional Information]
- Code to refactor:
[paste code]
- Target: ES6+ / TypeScript
- Changes needed:
  - Use arrow functions, destructuring, and template literals.
  - Implement proper async/await patterns.
  - Add TypeScript type annotations if applicable.
  - Use modern array methods (map, filter, reduce).
  - Implement proper module imports/exports.
  - Use `const` and `let` instead of `var`.
  - Add proper error boundaries.

[Directive]
Modernize this JavaScript code.
```

### Java Refactoring
```
[Role]
You are a seasoned Java architect.

[Additional Information]
- Code to refactor:
[paste code]
- Java version: Target Java [specify target version, e.g., 11, 17]
- Improvements:
  - Use Streams and lambda expressions.
  - Implement proper exception handling.
  - Use `Optional` for nullable values.
  - Apply the Builder pattern for complex objects.
  - Use generics appropriately.
  - Follow Java naming conventions.
  - Add proper annotations.

[Directive]
Refactor this Java code to use modern practices.
```

## API Design Improvements

### RESTful API Refactoring
```
[Additional Information]
- API design to improve:
[paste code or API description]
- Areas to improve:
  - Follow REST conventions for URLs and HTTP methods.
  - Implement proper status codes.
  - Add a consistent error response format.
  - Improve the request/response data structure.
  - Add proper validation and sanitization.
  - Implement pagination for list endpoints.
  - Add an API versioning strategy.

[Directive]
Improve this API design.
```

### GraphQL Schema Improvements
```
[Additional Information]
- Schema and resolvers to optimize:
[paste code]
- Improvements:
  - Eliminate N+1 query problems.
  - Implement proper batching and caching (e.g., using DataLoader).
  - Add input validation.
  - Optimize resolver efficiency.
  - Add proper error handling.
  - Implement field-level security.
  - Add schema documentation.

[Directive]
Optimize this GraphQL schema and its resolvers.
``` 