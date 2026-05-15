# Collections Framework

## Overview

Collections store groups of objects. Choosing the right collection affects correctness, performance, ordering, duplicates, and thread-safety.

## Core interfaces

| Interface | Purpose | Common implementations |
| --- | --- | --- |
| `List` | Ordered sequence, duplicates allowed | `ArrayList`, `LinkedList` |
| `Set` | Unique elements | `HashSet`, `LinkedHashSet`, `TreeSet` |
| `Queue` | Processing order | `ArrayDeque`, `PriorityQueue` |
| `Map` | Key-value lookup | `HashMap`, `LinkedHashMap`, `TreeMap` |

## Choosing collections

- Use `ArrayList` as the default list.
- Use `HashSet` for uniqueness without ordering.
- Use `LinkedHashMap` when predictable insertion order matters.
- Use `TreeMap` or `TreeSet` for sorted keys/elements.
- Use `ArrayDeque` for stack/queue behavior instead of `Stack`.

## Equality and maps/sets

Hash-based collections rely on `equals` and `hashCode`. Mutating an object after adding it to a `HashSet` can make it unreachable inside the set.

```java
Set<String> tags = new HashSet<>();
tags.add("java");
tags.add("java");
System.out.println(tags.size()); // 1
```

## Iteration and modification

Use an iterator's `remove` method or collection methods such as `removeIf` instead of modifying a collection directly during enhanced-for iteration.

```java
List<String> names = new ArrayList<>(List.of("Ada", "", "Grace"));
names.removeIf(String::isBlank);
```

## Sorting

```java
List<Person> people = new ArrayList<>();
people.sort(Comparator.comparing(Person::lastName).thenComparing(Person::firstName));
```

Use `Comparable` for natural ordering and `Comparator` for alternative orderings.

## Unmodifiable collections

`List.of`, `Set.of`, and `Map.of` create unmodifiable collections that reject `null`.

```java
List<String> priorities = List.of("high", "medium", "low");
```

## Exercises

1. Count word frequencies with `Map<String, Integer>`.
2. Remove duplicate records while preserving first-seen order.
3. Benchmark lookup in a `List` versus a `HashSet` for a large dataset.
