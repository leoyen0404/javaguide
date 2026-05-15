# Java SE 11 Cheat Sheets

## Compilation and execution

```bash
javac Example.java
java Example
java Example.java          # single-file source launch in Java 11
javap -c Example           # inspect bytecode
```

## Common syntax

```java
class Example {
    private final String name;

    Example(String name) {
        this.name = Objects.requireNonNull(name);
    }

    String name() {
        return name;
    }
}
```

## Collections quick choice

| Need | Use |
| --- | --- |
| Ordered duplicates | `ArrayList` |
| Unique elements | `HashSet` |
| Unique elements in insertion order | `LinkedHashSet` |
| Sorted elements | `TreeSet` |
| Key-value lookup | `HashMap` |
| Predictable map order | `LinkedHashMap` |
| Queue/deque | `ArrayDeque` |
| Concurrent map | `ConcurrentHashMap` |

## Generics

```java
class Box<T> { }
<T> T identity(T value) { return value; }
void read(Collection<? extends Number> source) { }
void write(Collection<? super Integer> target) { }
```

Remember PECS: producer extends, consumer super.

## Lambdas and streams

```java
Predicate<String> nonBlank = s -> !s.isBlank();
Function<String, Integer> length = String::length;

List<String> names = items.stream()
        .filter(nonBlank)
        .map(String::trim)
        .sorted()
        .collect(Collectors.toList());
```

## Date/time selection

| Concept | Type |
| --- | --- |
| Machine timestamp | `Instant` |
| Date without time | `LocalDate` |
| Time without date | `LocalTime` |
| Local date and time | `LocalDateTime` |
| Zoned real-world event | `ZonedDateTime` |
| Time amount | `Duration` |
| Date amount | `Period` |

## Exception patterns

```java
try (BufferedReader reader = Files.newBufferedReader(path)) {
    return reader.readLine();
} catch (IOException e) {
    throw new UncheckedIOException("Could not read " + path, e);
}
```

## JDBC essentials

```java
try (PreparedStatement ps = connection.prepareStatement(
        "select id from users where email = ?")) {
    ps.setString(1, email);
    try (ResultSet rs = ps.executeQuery()) {
        while (rs.next()) {
            System.out.println(rs.getLong("id"));
        }
    }
}
```

## Concurrency essentials

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
try {
    Future<String> future = executor.submit(() -> "done");
    System.out.println(future.get());
} finally {
    executor.shutdown();
}
```

## Secure coding reminders

- Validate untrusted input.
- Use `PreparedStatement` for SQL parameters.
- Never log secrets.
- Avoid Java deserialization for untrusted data.
- Normalize paths before file access.
- Use `SecureRandom` for security-sensitive randomness.
