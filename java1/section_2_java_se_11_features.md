# Java SE 11 Features

## Why Java 11 matters

Java 11 is a long-term-support release that consolidated platform changes introduced in Java 9, 10, and 11. To use Java 11 well, you should know the module system, `var` for local variables, new standard APIs, HTTP client support, and launch/runtime changes.

## Module system

The Java Platform Module System lets applications explicitly declare dependencies and exported packages.

```java
module com.example.app {
    requires java.net.http;
    exports com.example.app.api;
}
```

Use modules when you need strong encapsulation, reliable dependency boundaries, or smaller custom runtimes. Classpath-based applications remain valid and common.

## Local-variable type inference

`var` can be used for local variables when the initializer makes the type obvious.

```java
var names = new ArrayList<String>();
names.add("Ada");
```

Good uses:

- Long generic types where the right side is clear.
- Loop variables in stream or collection processing.

Avoid `var` when it hides important domain meaning or produces surprising inferred types.

## Standard HTTP client

Java 11 standardizes an asynchronous and synchronous HTTP client in `java.net.http`.

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder(URI.create("https://example.com"))
        .GET()
        .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.statusCode());
```

Use timeouts, handle interruptions correctly, and avoid hard-coding external endpoints in tests.

## String and collection conveniences

Java 11 adds helpful `String` methods:

```java
System.out.println("  ".isBlank());
System.out.println("Java\nGuide".lines().count());
System.out.println(" hi ".strip());
System.out.println("ha".repeat(3));
```

Java 9 added collection factory methods that are commonly used in Java 11 code:

```java
List<String> roles = List.of("admin", "reader");
Map<String, Integer> scores = Map.of("alice", 10, "bob", 8);
```

The returned collections are unmodifiable and reject `null` elements.

## Optional, streams, and predicates

Java 9-11 added conveniences such as `Optional.isEmpty`, stream factories, and predicate negation.

```java
Optional<String> value = Optional.empty();
if (value.isEmpty()) {
    System.out.println("missing");
}

Stream.ofNullable(null).forEach(System.out::println);
List<String> nonBlank = List.of("a", " ", "b").stream()
        .filter(Predicate.not(String::isBlank))
        .collect(Collectors.toList());
```

## Single-file source-code launch

Java 11 can run a single source file directly, useful for demos and scripts.

```bash
java Hello.java
```

This is not a replacement for builds in production projects, but it is convenient for learning.

## Removed and deprecated technologies

Java 11 removed Java EE and CORBA modules from the JDK. Applications that used JAXB, JAX-WS, or CORBA from the JDK need external dependencies.

## Practical checklist

- Use `var` only when readability improves.
- Prefer `List.of`, `Set.of`, and `Map.of` for small immutable constants.
- Use the standard HTTP client for simple HTTP integrations.
- Understand whether your project runs on the classpath or module path.
- Do not use post-Java-11 syntax in Java 11-targeted source.

## Exercises

1. Convert a small classpath program into a module with `module-info.java`.
2. Rewrite verbose local declarations using `var`, then revert any that reduce clarity.
3. Write a Java 11 HTTP request with a timeout and a clear error-handling path.
