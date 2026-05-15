# Practice Questions

Use these questions after each chapter. Write answers in your own words, then verify by compiling small examples.

## Core Java

1. What is the difference between a primitive variable and a reference variable?
2. Why does `==` behave differently for primitives and objects?
3. When should a class override `equals` and `hashCode`?
4. Explain overload resolution for `print(int)`, `print(long)`, and `print(Integer)`.
5. Why should fields usually be private?

## Java SE 11 features

1. When does `var` improve readability, and when does it hide intent?
2. What is the difference between classpath and module path execution?
3. Why are `List.of` results different from `new ArrayList<>()`?
4. What Java 11 `String` methods help with whitespace processing?
5. What changed when Java EE modules were removed from the JDK?

## Essential APIs

1. Which `java.time` type should you use for a database creation timestamp?
2. Why is `BigDecimal` preferred over `double` for currency?
3. What are the risks of unboxing wrapper values?
4. Why is `Optional.get()` usually a smell?
5. When should a regex be precompiled as a `Pattern`?

## Concurrency

1. What race condition can occur in `count++`?
2. Why should executors be shut down?
3. Compare `synchronized`, `ReentrantLock`, and `AtomicInteger`.
4. What makes a stream pipeline unsafe for parallel execution?
5. How can lock ordering prevent deadlock?

## Exceptions and I/O

1. What is the difference between checked and unchecked exceptions?
2. Why should wrapped exceptions keep the original cause?
3. What does try-with-resources do when closing fails?
4. Why is `Files.lines` usually used in try-with-resources?
5. What is path traversal and how can it be prevented?

## Collections, generics, and lambdas

1. Choose a collection for unique ordered insertion and explain why.
2. Why must map keys be stable with respect to `equals` and `hashCode`?
3. Explain PECS using a method that copies values between lists.
4. Why can `List<String>` not be assigned to `List<Object>`?
5. What is the difference between `map` and `flatMap` in streams?

## JDBC and advanced runtime topics

1. Why are prepared statements safer than string-built SQL?
2. What should happen if the second step of a two-step transaction fails?
3. When are annotations better than naming conventions?
4. What risks does reflection introduce?
5. What information can a thread dump reveal?

## Testing, security, and design

1. What makes a unit test deterministic?
2. Why should time be injected with `Clock` in tests?
3. Name three kinds of secrets that must not be committed.
4. When does a strategy pattern improve design?
5. What should be checked during a Java code review?

## Answer guidance

Strong answers should include a rule, a reason, and a small example. For coding questions, prefer runnable snippets over abstract descriptions.
