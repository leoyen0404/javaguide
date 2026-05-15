# Concurrency

## Overview

Concurrency lets a program make progress on multiple tasks, but it also introduces race conditions, deadlocks, visibility problems, and testing difficulty. In Java, prefer high-level concurrency utilities over manually managing raw threads.

## Threads and tasks

A `Thread` executes a `Runnable`, but application code usually submits tasks to an `ExecutorService`.

```java
ExecutorService pool = Executors.newFixedThreadPool(4);
try {
    Future<Integer> result = pool.submit(() -> 40 + 2);
    System.out.println(result.get());
} finally {
    pool.shutdown();
}
```

Always shut down executors you create.

## Shared state and synchronization

Race conditions occur when multiple threads access shared mutable state and at least one access writes.

```java
class Counter {
    private int value;

    synchronized void increment() {
        value++;
    }

    synchronized int get() {
        return value;
    }
}
```

` synchronized` provides mutual exclusion and establishes visibility guarantees. Keep synchronized sections short.

## Locks and atomics

`ReentrantLock` gives explicit lock control, while atomic classes provide lock-free operations for simple state.

```java
AtomicInteger count = new AtomicInteger();
count.incrementAndGet();
```

Use atomics for independent counters or flags. Use locks when updating related state together.

## Concurrent collections

Use purpose-built collections instead of wrapping ordinary collections manually.

- `ConcurrentHashMap` for high-throughput concurrent maps.
- `CopyOnWriteArrayList` for read-mostly listener lists.
- `BlockingQueue` for producer/consumer handoff.

```java
BlockingQueue<String> queue = new LinkedBlockingQueue<>();
queue.put("job");
String job = queue.take();
```

## Futures and completable futures

`CompletableFuture` composes asynchronous work.

```java
CompletableFuture<String> greeting = CompletableFuture
        .supplyAsync(() -> "hello")
        .thenApply(String::toUpperCase);
```

Handle exceptions explicitly with `exceptionally`, `handle`, or completion checks.

## Deadlock and liveness

Deadlock can happen when threads acquire locks in inconsistent order. Liveness problems also include starvation and livelock.

Prevention techniques:

- Acquire locks in a consistent global order.
- Avoid calling external code while holding a lock.
- Prefer immutable objects and message passing.
- Use timeouts where blocking is unavoidable.

## Parallel streams

Parallel streams can help CPU-bound, independent operations on large datasets, but they use the common fork-join pool by default. Avoid parallel streams for blocking I/O or operations with side effects.

## Exercises

1. Implement a producer/consumer workflow with `BlockingQueue`.
2. Replace a synchronized counter with `AtomicInteger`; explain when the replacement is safe.
3. Write a `CompletableFuture` pipeline that recovers from a failed remote call.
