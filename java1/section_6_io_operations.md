# I/O Operations

## Overview

Java provides classic stream APIs in `java.io` and modern path/file APIs in `java.nio.file`. Prefer `Path` and `Files` for most file-system work in Java 11.

## Paths and files

```java
Path config = Path.of("config", "app.properties");
if (Files.exists(config)) {
    String text = Files.readString(config);
    System.out.println(text);
}
```

`Path` is an abstraction over file-system paths. Avoid string concatenation for paths; use `Path.of` and `resolve`.

## Reading and writing text

Specify character sets when external compatibility matters.

```java
Path output = Path.of("report.txt");
Files.writeString(output, "status=ok\n", StandardCharsets.UTF_8,
        StandardOpenOption.CREATE, StandardOpenOption.TRUNCATE_EXISTING);
```

## Streaming large files

Do not load huge files into memory. Process them line-by-line.

```java
try (Stream<String> lines = Files.lines(Path.of("access.log"), StandardCharsets.UTF_8)) {
    long errors = lines.filter(line -> line.contains("ERROR")).count();
    System.out.println(errors);
}
```

The stream must be closed, so use try-with-resources.

## Binary I/O

Use byte streams for binary data.

```java
byte[] bytes = Files.readAllBytes(Path.of("image.bin"));
Files.write(Path.of("copy.bin"), bytes);
```

For very large binary files, use buffered streams or `Files.copy`.

## Serialization warning

Java object serialization is risky for untrusted data and tightly couples serialized form to implementation details. Prefer explicit formats such as JSON, Protocol Buffers, or database records for application data exchange.

## File walking

```java
try (Stream<Path> paths = Files.walk(Path.of("src"))) {
    paths.filter(Files::isRegularFile)
         .filter(path -> path.toString().endsWith(".java"))
         .forEach(System.out::println);
}
```

## Exercises

1. Write a program that counts words in a UTF-8 text file.
2. Copy a directory tree while preserving relative paths.
3. Watch a directory for create/modify/delete events using `WatchService`.
