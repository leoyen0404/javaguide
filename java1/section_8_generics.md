# Generics

## Overview

Generics let classes and methods operate on types while preserving compile-time type safety. They remove many casts and make APIs more expressive.

## Generic classes

```java
final class Box<T> {
    private final T value;

    Box(T value) {
        this.value = value;
    }

    T value() {
        return value;
    }
}
```

`T` is a type parameter. Common names include `T` for type, `E` for element, `K` for key, and `V` for value.

## Generic methods

```java
static <T> T first(List<T> items) {
    if (items.isEmpty()) throw new IllegalArgumentException("empty list");
    return items.get(0);
}
```

The type parameter is declared before the return type.

## Bounds

Bounds restrict type parameters to types with required capabilities.

```java
static <T extends Comparable<? super T>> T max(List<T> values) {
    return values.stream().max(Comparator.naturalOrder()).orElseThrow();
}
```

## Wildcards and PECS

PECS means **Producer Extends, Consumer Super**.

```java
static double total(Collection<? extends Number> numbers) {
    double sum = 0;
    for (Number number : numbers) sum += number.doubleValue();
    return sum;
}

static void addDefaults(Collection<? super Integer> target) {
    target.add(1);
    target.add(2);
}
```

Use `? extends T` when reading produced values as `T`. Use `? super T` when writing `T` values into a consumer.

## Type erasure

Generics are mostly compile-time. At runtime, many generic type details are erased. Consequences include:

- You cannot create `new T()` directly.
- You cannot create generic arrays like `new List<String>[10]` safely.
- Overloads cannot differ only by generic type arguments after erasure.

## Raw types

Raw types disable generic checks and should be avoided except when interoperating with legacy APIs.

## Exercises

1. Create a generic `Repository<ID, T>` interface.
2. Write a method that copies elements from `List<? extends T>` to `List<? super T>`.
3. Explain why `List<String>` is not a subtype of `List<Object>`.
