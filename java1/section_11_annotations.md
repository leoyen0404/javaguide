# Annotations

## Overview

Annotations attach metadata to code. The compiler, tools, frameworks, and runtime reflection can inspect that metadata to enforce rules or generate behavior.

## Built-in annotations

Common annotations include:

- `@Override` verifies that a method overrides or implements a supertype method.
- `@Deprecated` marks APIs that should no longer be used.
- `@SuppressWarnings` suppresses specific compiler warnings in the narrowest possible scope.
- `@FunctionalInterface` verifies a single abstract method contract.

## Defining annotations

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Audited {
    String value() default "";
}
```

Important meta-annotations:

- `@Retention` controls whether metadata is available in source, class files, or runtime.
- `@Target` restricts where the annotation can appear.
- `@Documented` includes the annotation in generated documentation.
- `@Inherited` applies only to class annotations and superclass inheritance.

## Annotation elements

Element values may be primitives, `String`, `Class`, enums, annotations, or arrays of those types.

```java
public @interface Retryable {
    int attempts() default 3;
    Class<? extends Throwable>[] retryOn() default { RuntimeException.class };
}
```

## Runtime processing

```java
if (method.isAnnotationPresent(Audited.class)) {
    Audited audited = method.getAnnotation(Audited.class);
    System.out.println(audited.value());
}
```

Runtime annotation processing often uses reflection and can affect startup time. Cache reflective lookups where appropriate.

## Compile-time processing

Annotation processors can generate code or validate rules during compilation. This is how many frameworks generate metadata, builders, or dependency-injection code.

## Exercises

1. Create an annotation for marking commands and inspect it at runtime.
2. Compare `RetentionPolicy.CLASS` and `RetentionPolicy.RUNTIME`.
3. Design an annotation that can be applied only to fields.
