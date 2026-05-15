# Lambdas and Streams

## Overview

Lambdas let you pass behavior as data when a target type is a functional interface. Streams use lambdas to describe data transformations and aggregation.

## Functional interfaces

A functional interface has exactly one abstract method.

```java
@FunctionalInterface
interface Rule<T> {
    boolean test(T value);
}
```

Common standard interfaces include `Predicate<T>`, `Function<T, R>`, `Consumer<T>`, `Supplier<T>`, `UnaryOperator<T>`, and `BiFunction<T, U, R>`.

## Lambda syntax

```java
Predicate<String> nonBlank = text -> !text.isBlank();
Comparator<String> byLength = (a, b) -> Integer.compare(a.length(), b.length());
```

A lambda can capture local variables only if they are final or effectively final.

## Method references

```java
List<String> names = List.of("Ada", "Grace");
names.forEach(System.out::println);
```

Method references are clearer when they directly name the intended behavior. Use a lambda when argument transformation makes the method reference hard to read.

## Stream pipeline anatomy

A stream pipeline has a source, zero or more intermediate operations, and one terminal operation.

```java
List<String> result = names.stream()
        .filter(name -> name.length() > 3)
        .map(String::toUpperCase)
        .sorted()
        .collect(Collectors.toList());
```

Intermediate operations are lazy; work begins only when a terminal operation runs.

## Collectors

```java
Map<Integer, List<String>> byLength = names.stream()
        .collect(Collectors.groupingBy(String::length));
```

Use collectors for grouping, partitioning, joining, reducing, and mapping results.

## Pitfalls

- Reusing a stream after a terminal operation causes `IllegalStateException`.
- Side effects in stream operations make behavior harder to reason about.
- Parallel streams require independent, stateless operations to be safe.
- `Optional` from stream operations should be handled explicitly.

## Exercises

1. Convert a loop that filters and maps values into a stream pipeline.
2. Group transactions by account and sum amounts.
3. Rewrite a complex method reference as a readable lambda and compare clarity.
