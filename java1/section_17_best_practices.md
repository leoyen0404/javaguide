# Best Practices

## Overview

Professional Java code is readable, testable, secure, observable, and maintainable. Best practices are trade-offs; apply them to improve clarity and reduce risk.

## Code organization

- Use packages by feature or domain, not only by technical layer.
- Keep public APIs small and stable.
- Prefer immutable value objects for data that should not change.
- Keep constructors simple; move complex creation into factories/builders.

## Naming and style

- Classes and interfaces: nouns or noun phrases (`Invoice`, `PaymentService`).
- Methods: verbs or verb phrases (`calculateTotal`, `sendReceipt`).
- Constants: `UPPER_SNAKE_CASE`.
- Avoid abbreviations unless they are standard in the domain.

## Null handling

Use clear contracts. Prefer required constructor parameters, validation, and empty collections. Use `Optional` for return values that may be absent.

## Immutability

```java
final class CustomerName {
    private final String value;

    CustomerName(String value) {
        this.value = Objects.requireNonNull(value);
    }

    String value() {
        return value;
    }
}
```

Immutable objects are easier to share, test, and reason about.

## Logging

Log meaningful events with context, but avoid secrets and excessive noise. Use appropriate levels:

- `ERROR` for failures requiring attention.
- `WARN` for unexpected but recoverable conditions.
- `INFO` for important lifecycle events.
- `DEBUG` for diagnostic detail.

## Performance

Start with correct code, measure, then optimize. Use profilers and benchmarks; do not rely on intuition for micro-optimizations.

## API design

- Make invalid states unrepresentable where practical.
- Use domain-specific types instead of passing many raw strings or numbers.
- Document thread-safety and ownership rules.
- Preserve backward compatibility for public APIs.

## Review checklist

- Are names clear?
- Are edge cases tested?
- Are resources closed?
- Are errors handled at the right layer?
- Are secrets protected?
- Is concurrency either avoided or explicitly controlled?

## Exercises

1. Refactor a mutable DTO into an immutable value object.
2. Add validation and tests to a public service method.
3. Review a small class using the checklist above and record findings.
