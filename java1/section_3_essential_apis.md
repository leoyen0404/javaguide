# Essential APIs

## Overview

The Java standard library is large, but everyday Java development depends on a core set of APIs: `Object`, `String`, wrappers, `Optional`, date/time, regex, streams, math, and utility classes. Mastering these APIs prevents unnecessary dependencies and reduces bugs.

## `Object`, equality, and hashing

Every class extends `Object`. If instances need logical equality, override `equals` and `hashCode` together.

```java
final class UserId {
    private final String value;

    UserId(String value) {
        this.value = Objects.requireNonNull(value);
    }

    @Override public boolean equals(Object other) {
        if (this == other) return true;
        if (!(other instanceof UserId)) return false;
        UserId that = (UserId) other;
        return value.equals(that.value);
    }

    @Override public int hashCode() {
        return value.hashCode();
    }
}
```

## Strings and text

`String` is immutable. Use `StringBuilder` for repeated mutation in loops.

```java
String normalized = " Java ".strip().toLowerCase(Locale.ROOT);
String joined = String.join(", ", "red", "green", "blue");
```

Use `Locale.ROOT` for machine-oriented case conversion, not the default user locale.

## Wrappers, boxing, and numbers

Primitive wrappers such as `Integer` and `Long` are objects. Autoboxing is convenient but can hide allocations and null risks.

```java
Integer maybe = null;
// int value = maybe; // NullPointerException from unboxing
```

For exact decimal arithmetic, use `BigDecimal` created from strings or integer cents.

## `Optional`

`Optional<T>` represents a possibly missing return value. It is usually a return type, not a field or parameter type.

```java
Optional<String> email = findEmail(userId);
String label = email.map(String::toLowerCase).orElse("unknown");
```

Avoid calling `get()` without checking presence.

## Date and time

Use `java.time`, not legacy `Date` and `Calendar`, for new code.

```java
LocalDate dueDate = LocalDate.now().plusDays(30);
Instant timestamp = Instant.now();
ZonedDateTime meeting = ZonedDateTime.of(2026, 5, 14, 9, 0, 0, 0, ZoneId.of("UTC"));
```

Choose the right type:

- `Instant` for machine timestamps.
- `LocalDate` for date-only business concepts.
- `LocalDateTime` for date/time without a zone.
- `ZonedDateTime` for real-world scheduled events.
- `Duration` for time-based amounts and `Period` for date-based amounts.

## Regular expressions

Use `Pattern` when matching repeatedly.

```java
Pattern emailLike = Pattern.compile("^[^@]+@[^@]+\\.[^@]+$");
boolean ok = emailLike.matcher("dev@example.com").matches();
```

Validate with domain-specific rules when correctness matters; regex alone rarely proves real-world validity.

## Streams

Streams process sequences declaratively. They are best for transformations, filtering, grouping, and aggregation.

```java
Map<String, Long> counts = List.of("java", "jvm", "java").stream()
        .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
```

Do not mutate shared state from a stream pipeline, especially in parallel streams.

## Utility classes

Useful APIs include:

- `Objects` for null checks and equality helpers.
- `Arrays` for array sorting, searching, and conversion.
- `Collections` for collection algorithms and wrappers.
- `Comparator` for composable ordering.
- `Base64` for encoding binary data as text.

## Exercises

1. Implement a value object with correct `equals`, `hashCode`, and `toString`.
2. Parse and format an ISO-8601 date using `java.time`.
3. Use streams to group orders by customer and sum totals.
