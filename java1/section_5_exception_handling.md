# Exception Handling

## Overview

Exceptions model failures that prevent normal progress. Good exception handling makes failures visible, preserves diagnostic context, and lets callers choose a recovery strategy.

## Exception hierarchy

- `Throwable` is the root type.
- `Error` usually represents serious JVM or environment failures; application code rarely catches it.
- `Exception` covers recoverable or application-level failures.
- Checked exceptions must be caught or declared.
- Runtime exceptions usually indicate programming errors, invalid arguments, or violated state.

```java
void load(Path path) throws IOException {
    Files.readString(path);
}
```

## Choosing exception types

Use standard exceptions when they communicate the problem clearly:

- `IllegalArgumentException` for invalid method arguments.
- `IllegalStateException` for invalid object state.
- `NullPointerException` rarely thrown manually; prefer `Objects.requireNonNull` for required parameters.
- `IOException` for file, network, or stream failures.
- Domain exceptions for business failures callers may handle.

## Try-with-resources

Use try-with-resources for objects that implement `AutoCloseable`.

```java
try (BufferedReader reader = Files.newBufferedReader(Path.of("input.txt"))) {
    return reader.readLine();
}
```

Resources close in reverse declaration order. Suppressed exceptions are attached to the primary exception.

## Wrapping and preserving causes

When translating exceptions between layers, keep the original cause.

```java
try {
    repository.save(order);
} catch (SQLException e) {
    throw new OrderPersistenceException("Could not save order " + order.id(), e);
}
```

Do not swallow exceptions silently. If a failure is intentionally ignored, document why.

## Logging and rethrowing

Log where the exception is handled, not at every layer. Logging and rethrowing repeatedly creates noisy duplicate stack traces.

## Best practices

- Fail fast at boundaries with clear messages.
- Keep catch blocks specific.
- Never use exceptions for normal loop control.
- Avoid broad `catch (Exception e)` unless at process boundaries.
- Do not return `null` to signal errors when an exception or `Optional` is clearer.

## Exercises

1. Convert manual stream closing code to try-with-resources.
2. Design a checked exception and an unchecked exception for a payment module; explain the choice.
3. Refactor a broad catch block into specific recovery paths.
