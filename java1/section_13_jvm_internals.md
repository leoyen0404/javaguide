# JVM Internals

## Overview

The Java Virtual Machine executes bytecode, manages memory, loads classes, performs just-in-time compilation, and provides diagnostics. Understanding the JVM helps you debug performance and production issues.

## Compilation pipeline

`javac` compiles `.java` source into `.class` bytecode. The JVM loads bytecode, verifies it, interprets it initially, and may compile hot methods to native code with the JIT compiler.

```bash
javac Example.java
javap -c Example
```

## Class loading

Class loading generally follows loading, linking, and initialization. Class loaders form a delegation hierarchy and define class identity together with the class name.

## Memory areas

- Heap: objects and arrays.
- Thread stacks: frames for method calls and local variables.
- Metaspace: class metadata.
- Code cache: compiled native code.
- Direct memory: off-heap buffers used by APIs such as NIO.

## Garbage collection

Garbage collectors reclaim unreachable objects. Java 11 commonly uses G1 as the default collector in many distributions, but exact defaults can vary by runtime build and options.

Good GC hygiene:

- Avoid unnecessary object retention.
- Close resources that hold native handles.
- Measure allocation rate before optimizing.
- Use JVM logs and profilers instead of guessing.

## Diagnostics

Useful tools include:

- `jps` to list Java processes.
- `jcmd` to request diagnostic commands.
- `jstack` for thread dumps.
- `jmap` and heap dumps for memory analysis.
- Java Flight Recorder for low-overhead runtime profiling.

## Common symptoms

| Symptom | Possible causes |
| --- | --- |
| High CPU | Busy loops, excessive GC, inefficient algorithms, lock contention. |
| Growing heap | Memory leak, unbounded cache, retained collections. |
| Deadlock | Inconsistent lock ordering or blocking while holding locks. |
| Slow startup | Classpath scanning, reflection, dependency initialization. |

## Exercises

1. Compile a class and inspect bytecode with `javap -c`.
2. Capture a thread dump from a running Java process.
3. Explain the difference between stack, heap, and metaspace.
