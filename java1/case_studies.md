# Case Studies

## Case Study 1: Library management system

### Problem

A library needs to manage books, members, loans, due dates, and overdue fees.

### Design

- `BookCopy` represents a physical copy, not just a title.
- `Member` owns borrowing permissions and contact information.
- `Loan` records checkout date, due date, return date, and status.
- `LoanRepository` hides persistence details.
- `FinePolicy` is a strategy so fee rules can change.

### Trade-offs

A simple in-memory implementation is ideal for learning collections and tests. A JDBC implementation is better for persistence but requires transaction boundaries around checkout and return operations.

### Lessons

- Domain types prevent primitive obsession.
- Strategies keep business rules replaceable.
- Tests should cover overdue edge cases by injecting `Clock`.

## Case Study 2: Order processing service

### Problem

An order service validates orders, reserves inventory, charges payment, and emits a receipt.

### Design

- Validate input at the service boundary.
- Use immutable order request objects.
- Wrap external failures in domain exceptions.
- Use transactions only around database state that must commit atomically.
- Avoid holding database transactions open during slow remote calls.

### Lessons

- Exception translation keeps infrastructure details out of the domain.
- Idempotency matters when retries are possible.
- Logging should include correlation IDs but never full payment secrets.

## Case Study 3: High-volume metrics collector

### Problem

A metrics collector receives frequent counter updates from multiple worker threads.

### Design

- Use `LongAdder` or `AtomicLong` for high-frequency counters.
- Snapshot metrics periodically.
- Store metric names in immutable value objects.
- Avoid synchronized global maps on hot paths.

### Lessons

- Thread-safety and performance must be measured.
- Concurrent collections reduce contention but do not remove all design risks.
- Unbounded metric names can create memory leaks.

## Case Study 4: Plugin-style command application

### Problem

A CLI application loads commands contributed by different modules.

### Design

- Define a small `Command` interface.
- Use a registry rather than scanning all classes by default.
- Optionally use annotations for metadata such as name and description.
- Keep reflective discovery optional and constrained.

### Lessons

- Interfaces provide safer extension points than arbitrary reflection.
- Modules can make dependencies explicit.
- Clear error messages are part of user experience.
