# Testing Prompts

Effective prompts for generating comprehensive tests, test strategies, and testing utilities.

## Unit Testing

### Basic Unit Tests
```
[Additional Information]
- Function to test:
[paste function code]
- Test framework: [Jest/pytest/JUnit/etc]
- Requirements:
  - Test all happy path scenarios.
  - Cover edge cases and boundary conditions.
  - Test error conditions and exception handling.
  - Include null, undefined, and empty input tests.
  - Add descriptive test names and assertions.
- Goal: Achieve close to 100% code coverage.

[Directive]
Write comprehensive unit tests for this function.
```

### Class Testing
```
[Additional Information]
- Class to test:
[paste class code]
- Testing approach:
  - Test all public methods.
  - Mock external dependencies.
  - Test state changes and side effects.
  - Verify method interactions.
  - Test error scenarios for each method.
  - Include setup and teardown methods.
  - Use dependency injection for testability.

[Directive]
Generate unit tests for this class.
```

### Property-Based Testing
```
[Additional Information]
- Function to test:
[paste function code]
- Framework: [Hypothesis/QuickCheck/JSVerify]
- Properties to test:
  - [describe mathematical properties or invariants, e.g., "reversing a list twice returns the original list"]
  - Input/output relationships that should always hold.
  - Behavior that should be consistent across a wide range of inputs.
  - Inverse operations (if applicable).
  - Idempotent operations (if applicable).
- Data generation: Generate meaningful test data ranges.

[Directive]
Create property-based tests for this function.
```

## Integration Testing

### API Integration Tests
```
[Additional Information]
- API endpoint to test:
[paste API code or description]
- Test scenarios:
  - Successful requests with valid data.
  - Invalid input data handling.
  - Authentication and authorization flows.
  - Rate limiting behavior.
  - Database interactions and data integrity.
  - External service integrations.
  - Correct error response formats.
  - Performance under load.

[Directive]
Write integration tests for this API endpoint.
```

### Database Integration Tests
```
[Additional Information]
- Database interaction code to test:
[paste database interaction code]
- Test coverage needed:
  - CRUD operations for all entities.
  - Transaction behavior and rollbacks.
  - Constraint violations and error handling.
  - Data integrity and relationships.
  - Query performance and optimization.
  - Connection pooling and timeout handling.
  - Migration and schema changes.

[Directive]
Create database integration tests for this code.
```

### Service Integration Tests
```
[Additional Information]
- Interacting services to test:
[describe services and their interactions]
- Test scenarios:
  - End-to-end user workflows.
  - Service communication protocols (e.g., REST, gRPC).
  - Data consistency across services.
  - Failure handling and retry logic.
  - Circuit breaker behavior.
  - Service discovery and load balancing.
  - Correct propagation of authentication tokens.

[Directive]
Design integration tests for these interacting services.
```

## End-to-End Testing

### Web Application E2E Tests
```
[Additional Information]
- Web application feature to test:
[describe feature or user story, e.g., "user checkout process"]
- Testing framework: [Cypress/Playwright/Selenium]
- Test cases:
  - Complete user workflows from start to finish.
  - Cross-browser compatibility.
  - Mobile responsiveness.
  - Form submissions and validations.
  - Navigation and routing.
  - Authentication flows (login, logout, session expiry).
  - Error handling and user feedback.
  - Performance and loading times.

[Directive]
Create end-to-end tests for this web application feature.
```

### Mobile App E2E Tests
```
[Additional Information]
- Mobile app functionality to test:
[describe mobile app feature]
- Framework: [Appium/Detox/Espresso]
- Test scenarios:
  - User registration and login flows.
  - Core feature functionality.
  - Offline behavior and data synchronization.
  - Push notification handling.
  - Different device sizes and orientations.
  - Network connectivity changes (e.g., switching from WiFi to cellular).
  - App state management (background/foreground).
  - Integration with device features (camera, GPS, contacts).

[Directive]
Design E2E tests for this mobile app functionality.
```

## Performance Testing

### Load Testing
```
[Role]
You are a Performance Engineer.

[Additional Information]
- System to test:
[describe system or application]
- Testing goals:
  - Define expected load patterns and user behavior.
  - Identify performance bottlenecks.
  - Test scalability limits.
  - Measure response times under load.
  - Monitor resource utilization (CPU, memory, network).
  - Test auto-scaling behavior.
  - Verify system stability under sustained load.
  - Create realistic test data and scenarios.

[Directive]
Create a load testing strategy for this system.
```

### Stress Testing
```
[Role]
You are a Quality Assurance Engineer specializing in reliability.

[Additional Information]
- System components to test:
[describe system components]
- Stress scenarios to simulate:
  - Gradually increase load beyond normal capacity to find breaking points.
  - Test resource exhaustion (memory, CPU, disk).
  - Simulate network latency and failures.
  - Test concurrent user limits.
  - Test database connection pool exhaustion.
  - Test file system and storage limits.
- Goal: Determine recovery behavior after failures.

[Directive]
Design stress tests to find the breaking points of this system.
```

## Security Testing

### Input Validation Testing
```
[Role]
You are a penetration tester.

[Additional Information]
- Code to test:
[paste code that handles user input]
- Security test cases:
  - SQL injection attempts
  - Cross-site scripting (XSS) payloads
  - Command injection attacks
  - Path traversal attempts
  - Buffer overflow inputs
  - Malformed data and edge cases
  - Unicode and encoding attacks
  - File upload vulnerabilities (e.g., unrestricted file types)

[Directive]
Create security tests for input validation.
```

### Authentication Testing
```
[Role]
You are a security analyst.

[Additional Information]
- Authentication system to test:
[describe authentication system]
- Test scenarios:
  - Password policy enforcement (length, complexity).
  - Account lockout mechanisms after failed attempts.
  - Session management security (e.g., cookie flags, session invalidation on logout).
  - Token expiration and refresh logic.
  - Multi-factor authentication flows.
  - Password reset security (e.g., token leakage).
  - Brute force attack protection.
  - Session hijacking prevention.

[Directive]
Design authentication security tests.
```

## Test Automation

### Test Data Management
```
[Additional Information]
- Application data requirements:
[describe application data requirements]
- Approach:
  - Generate realistic test data.
  - Create data factories or builders.
  - Implement data cleanup strategies (before/after tests).
  - Handle sensitive data securely in tests (e.g., using fake data).
  - Create reusable test datasets.
  - Manage test data across different environments.
  - Implement data versioning for tests.

[Directive]
Create a test data management strategy.
```

### Test Utilities and Helpers
```
[Additional Information]
- Application structure:
[describe application structure]
- Utilities needed:
  - Common setup and teardown functions.
  - Mock data generators.
  - Custom assertion helpers for complex objects.
  - Database seeding and cleanup utilities.
  - API test helpers for standard requests/responses.
  - File system test utilities (e.g., creating temp files).
  - Time manipulation helpers for tests (e.g., freezing time).

[Directive]
Build test utilities for this codebase.
```

## Test-Driven Development

### TDD Red-Green-Refactor
```
[Additional Information]
- Feature requirement:
[describe feature requirement]
- TDD Steps:
  1. Write a failing test that describes the desired behavior (Red).
  2. Write the minimal amount of code to make the test pass (Green).
  3. Refactor the code while keeping the tests green.
  4. Repeat for each small increment of functionality.
- Goal: Ensure comprehensive test coverage and a simple, clean design.

[Directive]
Follow the TDD approach to implement this requirement.
```

### Behavior-Driven Development
```
[Additional Information]
- User story or feature:
[describe user story or feature]
- BDD format (Given-When-Then):
  - **Given** [initial context and preconditions]
  - **When** [action or event occurs]
  - **Then** [expected outcome]
- Scenarios:
  - Include multiple scenarios covering different paths.
  - Use business-friendly language.
  - Cover both positive and negative cases.

[Directive]
Write BDD scenarios for this feature.
```

## Testing Strategies

### Test Pyramid Strategy
```
[Additional Information]
- Application architecture:
[describe application architecture, e.g., microservices, monolith]
- Test levels and distribution:
  - **Unit tests (70%):** Fast, isolated, comprehensive code coverage.
  - **Integration tests (20%):** Test service interactions, database connections, API contracts.
  - **E2E tests (10%):** Focus only on critical user journeys.
- Goals:
  - Define testing responsibilities for each level.
  - Identify potential overlaps and gaps in coverage.
  - Balance speed, reliability, and maintenance costs.

[Directive]
Design a testing strategy following the test pyramid model.
```

### Testing in CI/CD
```
[Additional Information]
- Deployment pipeline:
[describe deployment pipeline, e.g., using GitHub Actions, Jenkins]
- Pipeline stages:
  - Pre-commit hooks with linting and basic tests.
  - Unit tests on every commit.
  - Integration tests on pull requests.
  - E2E tests on staging deployment.
  - Performance tests before production release.
- Automation:
  - Implement automated rollback triggers on failure.
  - Configure test result reporting and notifications.

[Directive]
Create a testing pipeline for CI/CD.
```

## Code Quality Testing

### Code Coverage Analysis
```
[Additional Information]
- Codebase to analyze:
[describe codebase]
- Coverage strategy:
  - Set meaningful coverage thresholds (e.g., 80%).
  - Identify uncovered critical code paths.
  - Configure coverage reporting tools.
  - Exclude appropriate files from coverage (e.g., config files, generated code).
  - Monitor coverage trends over time.
- Goal: Balance coverage percentage with overall test quality.

[Directive]
Set up a code coverage analysis strategy.
```

### Mutation Testing
```
[Additional Information]
- Critical code to test:
[paste critical business logic sections]
- Mutation testing approach:
  - Identify critical logic for mutation testing.
  - Configure a mutation testing framework (e.g., Stryker, PITest).
  - Define acceptable mutation score thresholds.
  - Focus on high-value code paths.
  - Use results to improve test quality by writing tests that kill surviving mutants.
- Goal: Balance execution time with the benefit of increased test robustness.

[Directive]
Implement mutation testing for this code.
``` 