# Real-World Examples

These examples show how chapters combine in small applications. They are intentionally framework-light so the Java SE concepts remain visible.

## Example 1: Command-line expense tracker

### Requirements

- Add expenses with category, amount, and date.
- Save records to a UTF-8 CSV file.
- Summarize totals by category.
- Reject invalid amounts and malformed dates.

### Concepts used

- Core Java classes and validation.
- `java.time.LocalDate` for dates.
- `Path` and `Files` for storage.
- Collections and streams for grouping.
- Exceptions for input and I/O failures.

### Sketch

```java
final class Expense {
    private final LocalDate date;
    private final String category;
    private final long cents;

    Expense(LocalDate date, String category, long cents) {
        if (cents <= 0) throw new IllegalArgumentException("amount must be positive");
        this.date = Objects.requireNonNull(date);
        this.category = Objects.requireNonNull(category);
        this.cents = cents;
    }

    String toCsv() {
        return date + "," + category + "," + cents;
    }
}
```

### Extension tasks

1. Add unit tests for parsing and validation.
2. Support importing existing CSV data.
3. Add a monthly summary command.

## Example 2: Concurrent log analyzer

### Requirements

- Read many log files.
- Count errors by error code.
- Process files concurrently.
- Produce deterministic output.

### Concepts used

- `ExecutorService` for parallel file work.
- `ConcurrentHashMap` or result merging for aggregation.
- `Files.lines` for streaming large files.
- Clear exception handling for unreadable files.

### Design note

Prefer returning per-file maps and merging them in one thread unless profiling proves concurrent mutation is needed. Simpler designs are easier to test.

## Example 3: JDBC-backed user repository

### Requirements

- Create users.
- Find users by ID or email.
- Update status in a transaction.
- Avoid SQL injection.

### Concepts used

- JDBC prepared statements.
- Domain objects and repositories.
- Transactions and rollback.
- Unit tests with fake repositories and integration tests with a test database.

### Repository contract

```java
interface UserRepository {
    Optional<User> findById(long id) throws RepositoryException;
    long create(User user) throws RepositoryException;
}
```

## Example 4: Annotation-driven command runner

### Requirements

- Mark command methods with an annotation.
- Discover commands at startup.
- Invoke matching commands by name.

### Concepts used

- Custom annotations.
- Reflection.
- Exception handling.
- Security limits for reflective invocation.

### Warning

Keep reflection behind a small, tested boundary. Normal application logic should call typed methods directly.
